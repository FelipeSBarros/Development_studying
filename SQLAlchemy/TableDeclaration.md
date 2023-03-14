Há duas formas de definir e criar os objetos das tabelas do banco de dados. O primeiro, criando e declarando tanto o objeto  `MetaData` como o `Table`.

## [Configurando objetos `MetaData` e `Table`](https://docs.sqlalchemy.org/en/20/tutorial/metadata.html#setting-up-metadata-with-table-objects) :

```python
# definição do metadata
from sqlalchemy import MetaData
metadata_obj = MetaData()

#definição da tabela
from sqlalchemy import Table, Column, Integer, String
user_table = Table(
    "user_account",
    metadata_obj,  # metadata ao qual pertence a tabela
    Column("id", Integer, primary_key=True),
    Column("name", String(30)),
    Column("fullname", String),
)
```
Mais informações sobte a declaração de objetos [`Table`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.Table "sqlalchemy.schema.Table") .

## [Usando forma declarativa](https://docs.sqlalchemy.org/en/20/tutorial/metadata.html#using-orm-declarative-forms-to-define-table-metadata):

O Processo de contrução de tabelas com a forma declarativa, cumpre a mesma função do método anterior. A diferença está no uso de [ORM mapped class](https://docs.sqlalchemy.org/en/20/glossary.html#term-ORM-mapped-class) (*mapped class*), que é a unidade fundacional de SQL quando usando ORM e, em um uso moderno o SQLAlchemy, pode ser efetivo para uso em abordagens *Core-centric*.

Alguns benefícios:
- Uma sintaxe sucinta e mais Pythonico de configuração das definições de tabela, onde Python *types* podem ser usadas para a definição da estrutura do banco de dados.
- A classe mapeada pode ser usada para formar  expressões SQL que, em varios casos permite o uso de *type hints* ([**PEP 484**](https://peps.python.org/pep-0484/)).
- Permite a declaração do *MetaData* da tabela e classe mapeada ORM de uma vez.

Quando usnado ORM, O processo pelo qual nós declaramos [`Table`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.Table "sqlalchemy.schema.Table") *metadata* é usualmente combinado com o processo de declaração de classes [mapped](https://docs.sqlalchemy.org/en/20/glossary.html#term-mapped). Uma *mapped class* é qualquer classe Pytthon que queiramos criar, a qual terá, então, atributos linkados a colunas numa coluna de uma tabela do banco de dados. O método declarativo, nos permite declarar nossas classes e *MetaData* de uma só vez.

O [`MetaData`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.MetaData "sqlalchemy.schema.MetaData") estará associado a **Declarative Base**, a ser criado a partir da classe [`DeclarativeBase`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.DeclarativeBase "sqlalchemy.orm.DeclarativeBase") :

```python
from sqlalchemy.orm import DeclarativeBase
class Base(DeclarativeBase):
    pass
```

No exemplo a cima, a classe `Base` é o que será usada na abordagem *Declarative Base*. Quando fazemos uma nova classe que é subclasse de `Base`, a mesma será estabelecida como uma nova classe mapeada, cada uma tipicamente (mas não exclusivamente) se referindo a um objeto [`Table`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.Table "sqlalchemy.schema.Table") em particular.

A *Declarative Base* se refere à [`MetaData`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.MetaData "sqlalchemy.schema.MetaData") que é criada automaticamente, assumindo que não estamos proporcionando uma já criada. Tal [`MetaData`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.MetaData "sqlalchemy.schema.MetaData") é acessível por [`DeclarativeBase.metadata`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.DeclarativeBase.metadata "sqlalchemy.orm.DeclarativeBase.metadata"). 

A *Declarative Base* se refere também á coleção chamada [`registry`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.registry "sqlalchemy.orm.registry"), a qual é cental na unidade de configuração do mapeamento da ORM. Assim como com *MetaData*, a forma declarativa também criou um [`registry`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.registry "sqlalchemy.orm.registry") .

## Declarando as tabelas

Com uma clase `Base` criada, podemos, agora, definir as classes mapeadas para, por exemplo`user_account` como nova classe `User`. a seguir a forma mais moderna de de declará-la, seguindo [**PEP 484**](https://peps.python.org/pep-0484/) **type annotations** usnado o [`Mapped`](https://docs.sqlalchemy.org/en/20/orm/internals.html#sqlalchemy.orm.Mapped "sqlalchemy.orm.Mapped"), que indica os atributos a serem mapeados por tipos particulares:

```python
from typing import List
from typing import Optional
from sqlalchemy.orm import Mapped
from sqlalchemy.orm import mapped_column
from sqlalchemy.orm import relationship

class User(Base):
    __tablename__ = "user_account"
    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str] = mapped_column(String(30))
    fullname: Mapped[Optional[str]]
    addresses: Mapped[List["Address"]] = relationship(back_populates="user")
    def __repr__(self) -> str:
        return f"User(id={self.id!r}, name={self.name!r}, fullname={self.fullname!r})"

class Address(Base):
    __tablename__ = "address"
    id: Mapped[int] = mapped_column(primary_key=True)
    email_address: Mapped[str]
    user_id = mapped_column(ForeignKey("user_account.id"))
    user: Mapped[User] = relationship(back_populates="addresses")
    def __repr__(self) -> str:
        return f"Address(id={self.id!r}, email_address={self.email_address!r})"
```

- Para indicar as colunas tabela, foi usado o construtor [`mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column "sqlalchemy.orm.mapped_column"), em cobminação com as *typing annotations* baseadas no [`Mapped`](https://docs.sqlalchemy.org/en/20/orm/internals.html#sqlalchemy.orm.Mapped "sqlalchemy.orm.Mapped"). Isso criará objetos [`Column`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.Column "sqlalchemy.schema.Column") que são aplicados ao construtos [`Table`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.Table "sqlalchemy.schema.Table").
- Para colunas com *datatypes* e sem outras opções, podem ser configuradas apenas com o [`Mapped`](https://docs.sqlalchemy.org/en/20/orm/internals.html#sqlalchemy.orm.Mapped "sqlalchemy.orm.Mapped") *type annotation* (`int`, para  [`Integer`](https://docs.sqlalchemy.org/en/20/core/type_basics.html#sqlalchemy.types.Integer "sqlalchemy.types.Integer"),  `str` para  [`String`](https://docs.sqlalchemy.org/en/20/core/type_basics.html#sqlalchemy.types.String "sqlalchemy.types.String")). 

> see the sections [Using Annotated Declarative Table (Type Annotated Forms for mapped_column())](https://docs.sqlalchemy.org/en/20/orm/declarative_tables.html#orm-declarative-mapped-column) and [Customizing the Type Map](https://docs.sqlalchemy.org/en/20/orm/declarative_tables.html#orm-declarative-mapped-column-type-map) for background. 

- Uma coluna pode ser declarada “nullable” ou “not null” baseada no uso do `Optional[<typ>]` *type annotation* (ou o seu equivalente, `<typ> | None` ou `Union[<typ>, None]`). O [`mapped_column.nullable`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column.params.nullable "sqlalchemy.orm.mapped_column") poderia, ainda, ser definido explícitamente:

```python
action_id: Mapped[int] = mapped_column(ForeignKey("action.id"), nullable=True)
```

:warning: O uso de *typing annotations* é complemtamente **opcional**. Pode-se, inclusive, usar o [`mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column "sqlalchemy.orm.mapped_column") sem *annotations*. Em tais casos, seria necessário ser mais explícito com objetos como [`Integer`](https://docs.sqlalchemy.org/en/20/core/type_basics.html#sqlalchemy.types.Integer "sqlalchemy.types.Integer") e [`String`](https://docs.sqlalchemy.org/en/20/core/type_basics.html#sqlalchemy.types.String "sqlalchemy.types.String") , bem como usando `nullable=False` em casa [`mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column "sqlalchemy.orm.mapped_column").    

- O atributo `User.addresses` define um tipo diferente de atributo chamado [`relationship()`](https://docs.sqlalchemy.org/en/20/orm/relationship_api.html#sqlalchemy.orm.relationship "sqlalchemy.orm.relationship"). Para discussão completa, veja: [Working with Related Objects](https://docs.sqlalchemy.org/en/20/tutorial/orm_related_objects.html#tutorial-orm-related-objects).

- A cada classe é automaticamente atributida um método `__init__()`, caso um não seja declarado. A forma padrão de dito método é aceitar todos os atributos como argumentos nomeados:

```python
sandy = User(name="sandy", fullname="Sandy Cheeks")
```
- Para automaticamente gerar um `__init__()` que proporcione arguemtnos posicionais assim como argumentos de claradso por padrão, as classes de dadso apresentadas em [Declarative Dataclass Mapping](https://docs.sqlalchemy.org/en/20/orm/dataclasses.html#orm-declarative-native-dataclasses) poderão ser usadas. Outra possibilidade é definir explicitamente um `__init__()`.

-   O método `__repr__()` é criado para que tenhamos uma representação legível da classe instanciada.

# [Table reflection](https://docs.sqlalchemy.org/en/20/tutorial/metadata.html#table-reflection)

> Table reflection refers to the process of generating [`Table`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.Table "sqlalchemy.schema.Table") and related objects by reading the current state of a database. Whereas in the previous sections we’ve been declaring [`Table`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.Table "sqlalchemy.schema.Table") objects in Python and then emitting DDL to the database, the reflection process does it in reverse.

* [[AnnotatedObject]]