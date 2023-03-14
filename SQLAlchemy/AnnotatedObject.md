A declaração de tabelas apresentada em [[TableDeclaration]] usa a proposta de notação (`Annotated`) de tipo (`type`) da [**PEP 593**](https://peps.python.org/pep-0593/)  como chave em um dicionário [`registry.type_annotation_map`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.registry.params.type_annotation_map "sqlalchemy.orm.registry") . 

Dessa forma, o construtor [`mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column "sqlalchemy.orm.mapped_column") não "olha internamente" ao `Annotated` object. mas sim, apenas o usa como chave de dicionário. De qualque forma, a modelo declarativo tem a habilidade de extrair um ocnstrutor [`mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column "sqlalchemy.orm.mapped_column") de uma notação (`Annotated` ) de forma direta. Dessa fomra,podemos definir diferentes tipos de estruturas de dados SQL linkados às estruturas de dados python sem usa o dicionário [`registry.type_annotation_map`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.registry.params.type_annotation_map "sqlalchemy.orm.registry"). Pode-se, ainda configurar vários argumentos como a pemissão de valores nulos, valores padrão (*default*) e restrições (*constraints*) de forma a facilitar a sua reutilização.

É comum que um conjunto de modelos tenham alguns tipos de chave-primárias que seja comum a todas as classes mapeadas. Pode ser comum também que algumas configurações de coluna seja padronizadas, como uso de `timestamp`, com valores por padrão. é, portanto, possível compor essas configurações através de instâncias [`mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column "sqlalchemy.orm.mapped_column") , inseridas em instancias de `Annotated` que, então, podem ser usadas em qualquer declaração de classe. 

O exemplo abaixo ilusta alguns exemplos de compos pre-configurados.
* `intpk` representa uma coluna de chave primária com [`Integer`](https://docs.sqlalchemy.org/en/20/core/type_basics.html#sqlalchemy.types.Integer "sqlalchemy.types.Integer") ;
*`timestamp` representando [`DateTime`](https://docs.sqlalchemy.org/en/20/core/type_basics.html#sqlalchemy.types.DateTime "sqlalchemy.types.DateTime") com um valor padrão de `CURRENT_TIMESTAMP`, and
* `required_name` que é uma [`String`](https://docs.sqlalchemy.org/en/20/core/type_basics.html#sqlalchemy.types.String "sqlalchemy.types.String") com 30 caracteres `NOT NULL`;

```python
import datetime

from typing_extensions import Annotated

from sqlalchemy import func
from sqlalchemy import String
from sqlalchemy.orm import mapped_column

intpk = Annotated[int, mapped_column(primary_key=True)]
timestamp = Annotated[
    datetime.datetime,
    mapped_column(nullable=False, server_default=func.CURRENT_TIMESTAMP()),
]
required_name = Annotated[str, mapped_column(String(30), nullable=False)]
```

Os objetos `Annotated` poderão em seguida ser utilizados diretamente com [`Mapped`](https://docs.sqlalchemy.org/en/20/orm/internals.html#sqlalchemy.orm.Mapped "sqlalchemy.orm.Mapped"). Para mias informações sobre o uso do `func`, veja [[FunctionObject]].

```python
class Base(DeclarativeBase):
    pass


class SomeClass(Base):
    __tablename__ = "some_table"

    id: Mapped[intpk]
    name: Mapped[required_name]
    created_at: Mapped[timestamp]
```

O construtor [`mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column "sqlalchemy.orm.mapped_column") é sobreescrito quando um argumento é passado explicitamente. Logo, ao ter uma instância `Annotated` com argumentos já pré-definidos, os mesmo poderão ser "sobreescritos" por novos valores a esses argumentos

No exemplo abaixo adicionamos [`ForeignKey`](https://docs.sqlalchemy.org/en/20/core/constraints.html#sqlalchemy.schema.ForeignKey "sqlalchemy.schema.ForeignKey") à chave primária:

```python
class SomeClass(Base):
    __tablename__ = "some_table"

    # add ForeignKey to mapped_column(Integer, primary_key=True)
    id: Mapped[intpk] = mapped_column(ForeignKey("parent.id"))
```
