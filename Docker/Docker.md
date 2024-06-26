# [Instalação](https://linuxize.com/post/how-to-install-docker-on-ubuntu/)

```
sudo apt install ca-certificates curl gnupg
```

Next, import the Docker repository’s GPG key to your system:

```
sudo mkdir -p /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```

Add the Docker APT repository to your system:

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list
```

`$(lsb_release -cs)` will print the Ubuntu codename. For example, if you have [Ubuntu version](https://linuxize.com/post/how-to-check-your-ubuntu-version/) 22.04 the command will print `jammy`.

Now that the Docker repository is enabled, you can install any Docker version that is available in the repositories.

To install the latest version of Docker, run the commands below. If you want to install a specific Docker version, skip this step and go to the next one.

```
sudo apt update
```

## [Enabling docker to run without `sudo`](https://docs.docker.com/engine/install/linux-postinstall/)
[source](https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/)  
To create the `docker` group and add your user:

* Create the `docker` group.
```console
sudo groupadd docker
```

- Add your user to the `docker` group.
```console
sudo usermod -aG docker $USER
```

- Log out and log back in so that your group membership is re-evaluated.
You can also run the following command to activate the changes to groups:
```console
newgrp docker
```

- Verify that you can run `docker` commands without `sudo`.
```console
docker run hello-world
```
This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

## Comandos gerais
Listar todas as imagens docker:  
  
```commandline  
docker images  
```  
  
Remover imagem docker:  
  
```commandline  
docker rmi <docker_imge> # --force  
```  
  
Listar todos os containers (apenas lista os ativos):  
  
```commandline  
docker ps  
```  

Listar todos os containers, mesmo inativos:  
  
```commandline  
docker container ls -a  
```  
  
Removendo container:  
  
```commandline  
docker rm <containerID>  
```  
  
removendo `docker volumes`:  
  
```commandline  
docker volume rm  
```  
  
Removendo `docker networks`:  
  
```commandline  
docker network rm  
```  

**Inspecionando** um container:
Primeiro, temos que identificar o ID dele:

```
docker container ls
CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS          PORTS      NAMES
596c91e63fe1   postgis/postgis   "docker-entrypoint.s…"   11 minutes ago   Up 11 minutes   5432/tcp   postgis
```
Agora usamos o **CONTAINER ID** no comando:
```
docker inspect 596c91e63fe1
```

## Executando docker  
  
```shell  
docker up -d  
```  

`-d` libera o terminal.  
  
```shell  
docker-compose ps  
```  
  
Os `docker-composes` identificados como "restarting", são aqueles que dependem de dependencias do projeto. Para instalá-los, basta acessar o bash do container da app e executar o `composer install`, que irá ler o arquivo `composer.json` com as dependencias e os instalarão.  
  
```shell  
docker-compose exec app bash  
# carlos@e8d842490502:/var/www$  
  
carlos@e8d842490502:/var/www$ composer install
```  
  
[**Composer install**](https://getcomposer.org/doc/01-basic-usage.md#installing-dependencies)  
  
> It resolves all dependencies listed in your composer.json file and writes all of the packages and their exact versions to the composer.lock file, locking the project to those specific versions.  
  
## .env e docker-compose.yml  
  
Podemos passar parâmetros do arquivo `.env` para o `docker-compose.yml`, desde que esteja no mesmo nível de pasta: ${DB_PASSWORD};
  
> Compose supports declaring default environment variables in an environment file named .env placed in the project directory.  
  
Assim como passamos ao `.env` a informação do banco de dados, usando o nome da app criada no `docker-compose.yml`:  
  
```shell  
DB_CONNECTION=mysql  
DB_HOST=mysql  
DB_PORT=3306  
DB_DATABASE=curso_laravel_9  
DB_USERNAME=root  
DB_PASSWORD=root    
```  
  
O `mysql` faz referência ao nome do container no `docker-compose.yml`:  
  
```shell  
# db mysql  
mysql:  
container_name: especializati-mysql  
image: mysql:5.7.22  
restart: unless-stopped  
environment:  
MYSQL_DATABASE: ${DB_DATABASE}  
MYSQL_ROOT_PASSWORD: ${DB_PASSWORD}  
MYSQL_PASSWORD: ${DB_PASSWORD}  
MYSQL_USER: ${DB_USERNAME}  
volumes:  
- ./.docker/mysql/dbdata:/var/lib/mysql  
ports:  
- "3388:3306"  
networks:  
- laravel-9  
```  
  
## Docker network  
  
O [network][docker-network] é o parâmetro que garante que cada container possa  
sse comunicar com o outro.  
  
[docker-network]: https://docs.docker.com/network/