>pytest fixtures are designed to be explicit, modular and scalable.

`fixtures` provê contextos confiáveis para  os testes e, por isso, contitui o passo de **arrange**.

A ideia de *fixtures* está baseada no *design pattern* e visa desacoplar a dependencia entre funções. Neste caso, os testes dependem de dados salvos no banco de dados. 

Os serviços, estados e outros elementos importantes do ambiente de teste são consigurados por funções e seus argumentos. A cada *fixture* usada por uma função de teste, há um parâmetro (nomeado após a *fixture*) na definição da função.

Usamos o decorador [`@pytest.fixture`](https://docs.pytest.org/en/7.1.x/reference/reference.html#pytest.fixture "pytest.fixture") para avisar ao `pytest` que uma função em particular é uma *fixture*.

Exemplo:
```python
@pytest.fixture(scope="module") 
def db_session():
	Base.metadata.create_all(engine)
	session = Session()
	yield session
	session.rollback()
	session.close()
	
@pytest.fixture(scope="module")
def valid_author():
	valid_author = Author(
		firstname="Ezzeddin",         
		lastname="Aybak",
		email="aybak_email@gmail.com"
		)
	return valid_author`
```

Uma *fixture* é baseada num escopo (*[scope](https://docs.pytest.org/en/7.1.x/how-to/fixtures.html#scope-sharing-fixtures-across-classes-modules-packages-or-session)*). Um escopo é o que podemos usar para compartilhar *fixtures* entre *classes*, *modules*, *packages*, or *sessions*.No exemplo acima,  `db_session` e `valid_author` podem apenas ser chamados no módulo em questão.

Cada função de teste usnado a *session* receberá a mesma instância da *session*, com isso economizando tempo, de forma que a função *fixture* é invocada uma vez por cada módulo de teste.

O uso de `yield` é [recomendado](https://docs.pytest.org/en/7.1.x/how-to/fixtures.html#yield-fixtures-recommended). Após a linha `yield`, a sessão passa por um `rollback` e então é fechada, o que seria equivalente ao código *teardown*.


### Fixture [scopes](https://docs.pytest.org/en/7.1.x/how-to/fixtures.html#fixture-scopes)

*Fixtures* são criados quando requisitados por um teste e são *destruidos* com base no *scope*:

-   `function`: Escopo padrão, a *fixture* é destruida logo ao fim do teste.
-   `class`: A *fixture* é destruida durante o processo de *teardown* do último teste da classe.
-   `module`: A fixture é destruida durante o *teardown* do último módulo de teste.
-   `package`: A *fixture* é destruida durante o *teardown* do último teste do pacote.    
-   `session`: A *fixture* é destruida ao fim da última sess]ao de teste.
