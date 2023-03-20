## Algumas observações

### `nullable`

O valor padrão do SQLAlchemy `nullable` é `True`, a menos que se trate de uma chave primária. Uma chave extrangeira é nullable por padrão. 

> Diferente do ORM DJango, onde os valores padrão são `null=False` e `blank=False`.

Contudo, esse comportamente está alinhado com o padrão SQL, onde as colunas devem ser `nullabla` até que se explicite o contrário.

### Column `default` e `server_default`

Por padrão, colunas não possuem atributos com valor padrão no processo de criação da tabela. Logo, não dependa disso, caso vá inserir registros sem usar o SQLAlchemy. 

Para definir na configuração um valor padrão à tabela, use `server_default`, onde pode-se usar `scalars` ou `functions`.

>SQLAlchemy is aware of a lot of database functions and their database-specific variants. Use [SQL function expressions generator](https://docs.sqlalchemy.org/en/14/core/sqlelement.html#sqlalchemy.sql.expression.func), available as `sqlalchemy.func`. Consult [SQL and Generic Functions](https://docs.sqlalchemy.org/en/14/core/functions.html).

### `onupdate` vs. `server_onupdate`

The same rule applies to `update` vs. `server_onupdate`.

O seguinte modelo possui atributo `created_at` e `updated_at` com dados populados pelo python;

```python
import datetime
import sqlalchemy as sa

class User(Base):
    __tablename__ = "users"
    id = sa.Column(sa.Integer, primary_key=True)
    created_at = sa.Column(
        sa.DateTime,
        nullable=False,
        default=datetime.datetime.utcnow,
    )
    updated_at = sa.Column(
        sa.DateTime,
        nullable=False,
        default=datetime.datetime.utcnow,
        onupdate=datetime.datetime.utcnow,
    )
```

O seguinte modelo insere dados em tais campos pelo SQL:

```python
import sqlalchemy as sa

class User(Base):
    __tablename__ = "users"
    id = sa.Column(sa.Integer, primary_key=True)
    created_at = sa.Column(sa.DateTime, nullable=False, server_default=sa.func.now())
    updated_at = sa.Column(
        sa.DateTime,
        nullable=False,
        server_default=sa.func.now(),
        server_onupdate=sa.func.now(),
    )
```

### Document fields of your models with `doc` and `comment`

-   Use the `doc` column attribute to document the SQLAlchemy field for future self and other developers working with the code.
-   If you plan to work with raw SQL, consider adding the `comment` attribute — it will be associated with the column on the database level and will be visible even for those who don’t use the ORM.

using doc and comment for columns

```python
import sqlalchemy as sa

class User(Base):
    id = sa.Column(sa.Integer, primary_key=True)
    name = sa.Column(sa.String, nullable=False, doc="User name", comment="User name")
```
