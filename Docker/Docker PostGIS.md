[**POST muito bom**](https://scottogletree.com/post/docker/)

A imagem do PostGIS instala e instancia um banco de dados PostgreSQL com as seguintes extensões já instaladas:

| installed extensions | initializated |
|:---:|:---:|
| postgis | yes |
| postgis_topology | yes |
| postgis_tiger_geocoder | yes |
| postgis_raster |  |
| postgis_sfcgal ( except the alpine versions) |  |
| address_standardizer |  |
| address_standardizer_data_us |  |

## Baixando a imagem oficial:

`docker pull postgis/postgis`

## Instalando e configurando
Basta iniciar o container:

`docker run --name postgis -e POSTGRES_PASSWORD=postgres -d postgis/postgis`

* `--name` atribui um nome ao container;
* `-e` define variável a ser usada: senha;
* `-d` libera o terminal e apresenta o container ID;
* `postgis/postgis` é a imagem a ser executada;

Ainda que se trate de uma imagem `postgis`, os principais parâmetros e formas de usar estão vinculadas ao [`postgre`](https://registry.hub.docker.com/_/postgres/)

## Acessando o banco de dados pelo `psql`

```
docker exec -ti postgis psql -U postgres
```

:warning: Para conectar pelo DBeaver ou pgAdmin, é necessário usar o IP e não a string `localhost`.

Outra forma de conectar é iniciando um outro container para ser usado como instância cliente. Neste caso, pode-se usar um `network` definido por usuário para conectar ambos containers:

`docker network create some-network`

Em seguida, deve-se criar o **container server** com o parâmetro `--network`, ou aterá-lo no `.yaml`:

```docker run --name postgis --network some-network -e POSTGRES_PASSWORD=mysecretpassword -d postgis/postgis```

No caso do **container cliente**:

```docker run -it --rm --network some-network postgis/postgis psql -h some-postgis -U postgres```
