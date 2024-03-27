A palavra chave `func` do SQLALchemy API é usada para gerar funções padrão do SQL implementadas nos diferentes dialetos. Essas funções podem retornar um valur único e pode ter colunas como argumento.

O objeto retornado é uma instancia da classe [`Function`](https://docs.sqlalchemy.org/en/20/core/functions.html#sqlalchemy.sql.functions.Function "sqlalchemy.sql.functions.Function"), e é orientada a um elemento SQL orientado a uma coluna.
```python
print(select(func.count(table.c.id)))
# SELECT count(sometable.id) FROM sometable
```

Qualquer nome pode ser atribuido a uma [`func`](https://docs.sqlalchemy.org/en/20/core/sqlelement.html#sqlalchemy.sql.expression.func "sqlalchemy.sql.expression.func"). Caso o nome não seja conhecido para o SQLAlchemy, o mesmo será renderizado tal qual como informado.

Para a mmaioria das funções SQL, às quais o SQLAlchemy conhece, o nome deve ser interpretado como uma _generic function_ que será compilada apropriadamente no banco de dados alvo.
