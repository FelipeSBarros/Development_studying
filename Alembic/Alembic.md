# Quickstart

Alembic permite a criação e gestão de mudanas de scipts para banco de dados relcionais (em teoria, noSQL, não possuem uma estrutura formalizada, o que faz carecer de um sistema como alembic), usando [[SQLAlchemy]] como motor. 

É usualmente sugerido que Alembic seja instalado no mesmo path do modulo python ou projeto alvo, de forma que o comando `alembic` ao ser executado invoque o `env.py` do projeto em questão.

## Instalação

```
poetry add alembic # pip install alembic
```

### Iniciando ambiente das *migrations*

Innicinado a estrutura básica para fazer seguimento das migrações, dentro da paste do projeto em questão:

```
alembic init <nome> # nome pode ser qualquer um. Uso migrations
```

#### Entendendo o ambiente de *migrations*

Ao inicar o `alembic`, cria-se um ambiente de migrações (a ser criado apenas uma vez): um diretório com os scripts específicos para um projeto/aplicação em particular. Esse ambiente de migrações que serrá gerido ao longo do projeto junto com o código fonte.

Após a criação do ambiente com o comando `init` os scripts deverão ser configutados para ajudar as demandas do projeto.

A estrutura desse ambiente, incluindo alguns scripts de migração, seguem o seguinte padrão:

```
yourproject/
    alembic/
        env.py
        README
        script.py.mako
        versions/
            3512b954651e_add_account.py
            2b1ae634e5cd_add_order_id.py
            3adcc9a56557_rename_username_field.py
```

-   `yourproject` - Essa é a pasta raiz do projeto.
    
-   `alembic` - Pasta interna à pasta raiz do projeto, é onde estará o ambiente de migrações. Pode ser criado com diferentes nomes, e projetos que possuem multiplos bancos de dados podem ainda ter mais de um.
    
-   `env.py` - Esse é um Python script executado sempre que a ferramentação de migração do alembic é executada. De forma geral, possui instruções de configuração e criação da `SQLAlchemy` [[Engine]].
    
    O `env.py` é parte geral do ambiente de forma que as execussões das migrações são enteiramente customizáveis. Como conectar, assim como definições de como as migrações são executadas. Esse script pode ser alterado de forma que várias `engines` possam ser operadas.
    
    Alembic inclui um conjunto de padrões de inicialização os quais permitem configuração de difernetes casos de uso.
    
-   `README` - Leia-me, documentação informativa sobre as migrações.
    
-   `script.py.mako` - Trata-se de um arquivo com padrão [Mako](http://www.makotemplates.org) usado para gerar novos scripts de migrações, que seerão armazenadas em `versions/`. É esse script que estrutura cada migração, tornando-as controláveis.
    
-   `versions/` - Diretório que armazena cada versão dos scripts de migração gerados. Tais arquivos usam um `GUID` parcial como nome. Logo, no Alembic, a ordenação da versão dos scripts são relativos a diretivas informadas internamente a cada script, permitindo a sequencia de migrações de diferentes `branches`.

### Linkando com base de dados:

Em `alembic.ini`, buscar pelo `sqlalchemy.url` e adicionar o uri à base de dados:

`sqlalchemy.url = sqlite:///gastos_dev.sqlite`

## Gerando migração a apartir de models.py

[ver live](https://www.youtube.com/live/yQtqkq9UkDA?feature=share&t=3896) 
Para relacinoar o `models.py` com o alembic, será necessário adicionar ao `.ev.py`, do alembic o [`Base.metadata`](https://www.youtube.com/live/yQtqkq9UkDA?feature=share&t=3791):

```python
# .env.py
from models import Base
...
target_metadata = Base
```

### Adicionando o url da base de dados direto pelo `Base`

[ver live](https://www.youtube.com/live/yQtqkq9UkDA?feature=share&t=5857)

Add ao `.env`:
`DB_URL='sqlite:///gastos.db'`

Add ao `alembic.ini`:
`sqlalchemy.url = none`

Add ao `.emv.py`:
```python
config.set_section_option("alembic", "sqlalchemy.url",  
                          os.environ.get("DB_URL", config.get_section_option("alembic", "sqlalchemy.url")))
```
