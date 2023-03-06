# Criando banco de dados e tabelas

Com o  [`MetaData.create_all()`](https://docs.sqlalchemy.org/en/20/core/metadata.html#sqlalchemy.schema.MetaData.create_all "sqlalchemy.schema.MetaData.create_all"):, *metadata* da nossa `engine`, podemos criar o `schema` no momento em que temos o nosso banco de dados como alvo.

```python
Base.metadata.create_all(engine)
```

* [[TableDeclaration]]
