>pytest fixtures are designed to be explicit, modular and scalable.

`fixtures` provê contextos confiáveis para  os testes e, por isso, contitui o passo de **arrange**.

Os serviços, estados e outros elementos importantes do ambiente de teste são consigurados por funções e seus argumentos. Para cada *fixture* usada. A cada *fixture* usada por uma função de teste, há um parâmetro (nomeado após a *fixture*) na definição da função.

Usamos o decorador [`@pytest.fixture`](https://docs.pytest.org/en/7.1.x/reference/reference.html#pytest.fixture "pytest.fixture") para avisar ao `pytest` que uma função em particular é uma *fixture*.

Exemplo:
```python

```