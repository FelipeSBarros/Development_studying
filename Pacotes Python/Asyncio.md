
[Pacote python](https://docs.python.org/3/library/asyncio.html) para desenvolver código de corrotina usando sintaxe async/await.
* run()*: Execução de uma *corotina*;
**Loop de eventos** :
* `create_task`: Cria tarefas e adiciona a fila de tarefas;
* `all_task()`: Identifica a lista de tarefas registradas para execução;
* `await`: Escalonamento de tarefas; ponto onde o computador troca de tarefa para não ter que esperar pelo fim da mesma;
* `gather`: Faz com que o retorno das trefas respeitem a ordem de solicitação;