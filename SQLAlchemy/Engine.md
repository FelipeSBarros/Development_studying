Uma aplicação SQLAlchemy começa com um objeto chamado [`Engine`](https://docs.sqlalchemy.org/en/20/core/connections.html#sqlalchemy.engine.Engine "sqlalchemy.engine.Engine"), que atúa como uma fonte central de conexão a um banco de dados particular, provendo tanto uma fábrica quanto um *pool* de conexão ([connection pool](https://docs.sqlalchemy.org/en/20/core/pooling.html) ). *engine* é tipicamente um objeto global criado apenas uma vez para um banco de dados praticular, e é configurada usando URL string que descreve como a conexão será feita com o servidor ou backend.

Exemplo de `engine` usando um SQLite na memória:

```python
from sqlalchemy import create_engine
engine = create_engine("sqlite+pysqlite:///:memory:", echo=True)
```

No `create_ _engine` se linka com o banco de dados, a partir de um [dialect](https://docs.sqlalchemy.org/en/20/glossary.html#term-dialect): um objeto Python que represente informações e métodos que permitem o procerssamento e operações em um banco de dados particular e/ou um *driver* Python em particular (or [DBAPI](https://docs.sqlalchemy.org/en/20/glossary.html#term-DBAPI)). Os dialetos SQLAlchemy são subclasses de  [`Dialect`](https://docs.sqlalchemy.org/en/20/core/internals.html#sqlalchemy.engine.Dialect "sqlalchemy.engine.Dialect") .

O [DBAPI](https://docs.sqlalchemy.org/en/20/glossary.html#term-DBAPI) é um *driver* que SQLAlchemy usa para interagir com um banco de dados em particular. Neste caso, estamos usando o `pysqlite`,  que é um uso moderno do [sqlite3](https://docs.python.org/library/sqlite3.html) , para SQLite. Se omitido, SQLAlchemy irá usar o [DBAPI](https://docs.sqlalchemy.org/en/20/glossary.html#term-DBAPI) padrão para o banco de dados em questão.

Definimos também o parâmetro [`create_engine.echo`](https://docs.sqlalchemy.org/en/20/core/engines.html#sqlalchemy.create_engine.params.echo "sqlalchemy.create_engine"), que irá fazer com que o [`Engine`](https://docs.sqlalchemy.org/en/20/core/connections.html#sqlalchemy.engine.Engine "sqlalchemy.engine.Engine") apresente todo a consulta SQL no *standard out*

* [[DataBaseCreation]]
* [[TableDeclaration]]
