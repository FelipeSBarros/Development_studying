[`Pytest`](https://docs.pytest.org/en/7.2.x/) é um framework para criação de teste unitários de sistema.

Ele executará todos os arquivos que tenham o seguinte padrão `test_*.py` ou `*_test.py` ino diretório de trabalho ou subdiretórios; [standard test discovery rules](https://docs.pytest.org/en/7.2.x/explanation/goodpractices.html#test-discovery).

## [Anatomia do teste](https://docs.pytest.org/en/7.1.x/explanation/anatomy.html#anatomy-of-a-test)

Um teste deve inspecionar o resultado de um comportamento em específico e garantir que o resultado está alinhado com o esperado. O **comportamento** não é algo que possa ser medido de fomra emírica, o que torna o processo de produção de testess, desafiante.

**Comportamento** é a forma pela qual um sistema age em resposta a uma situação particular ou estímulo.

Pode-se dividir o processo de teste em quatro passos:

1.  **Arrange**    
2.  **Act**
3.  **Assert**
4.  **Cleanup**

**Arrange** é quando tudo é preparado para o teste. Isso pode sirgnificar preparar objetos, iniciar/terminar serviços, criar registros no bando de dados. É nessa fase que as [fixtures](obsidian://open?vault=Development_studying&file=Pyteste-fixture) são executadas.

**Act** é a fase da ação, de mudança do estado do sistema em teste (*system under test - SUT*) para que o comportamento seja testado. Tipicamente tem a forma de uma função ou método sendo chamado.

**Assert** é o passo no qual se confere se o resultado obtido está como esperado. É aonde se identificam as evidencias para saber se o comportamente alinha ou não com o esperado. O `assert` é onde se faz o julgamento da comparação entre observado e esperado.

`assert thing == "green"`.

**Cleanup** é quando o teste recolhe/organiza o ambiente para que outros testes não sejam influenciados pelo resultado do primeiro.

* [[Pyteste-fixture]]

#arrange