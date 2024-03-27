Estudando o processo de deploy do [Pretix](https://docs.pretix.eu/en/latest/admin/installation/docker_smallscale.html)

>This guide describes the installation of a **small-scale installation** of pretix using docker. By small-scale, we mean that everything is being run on one host and you don’t expect thousands of participants trying to get a ticket within a few minutes.

## Requirements

- [Docker](https://docs.docker.com/engine/installation/linux/debian/)
- A SMTP server to send out mails, e.g. [Postfix](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-postfix-as-a-send-only-smtp-server-on-ubuntu-22-04) on your machine or some third-party server you have credentials for
- A HTTP reverse proxy, e.g. [nginx](https://botleg.com/stories/https-with-lets-encrypt-and-nginx/) or Apache to allow HTTPS connections
- A [PostgreSQL](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-22-04) 12+ database server
- A [redis](https://blog.programster.org/debian-8-install-redis-server/) server

## Notes:

> All code lines prepended with a `#` symbol are commands that you need to execute on your server as `root` user; all lines prepended with a `$` symbol can also be run by an unprivileged user.

## Data-files
É necessário criar uma pasta onde o Pretix irá armazenar algunas arquivos:
```
sudo mkdir /var/pretix-data
sudo chown -R 15371:15371 /var/pretix-data
```
## Database

Vamos usar um docker com PostgreSQL:
`docker start postgres`

Confirmando server `Enconding`:
`docker exec -ti postgres psql -U postgres -c 'SHOW SERVER_ENCODING' `
 Criando usuário:
 ```
 docker exec -ti postgres psql -U postgres
 ```
no PSQL
 ```
 # PSQL 
 CREATE USER pretix WITH PASSWORD 'pretix';
 ```
Criando base de dados:
 ``` 
 create database pretix OWNER pretix;
 ```

> Make sure that your database listens on the network. If PostgreSQL on the same same host as docker, but not inside a docker container, we recommend that you just listen on the Docker interface by changing the following line in `/etc/postgresql/<version>/main/postgresql.conf`:

## REDIS

```
docker pull redis
docker images # identificar imge ID
docker run --name redis 170a1e90f843
```


# [Config-file](https://docs.pretix.eu/en/latest/admin/installation/docker_smallscale.html#config-file)
We now create a config directory and config file for pretix:
```
# mkdir /etc/pretix
# touch /etc/pretix/pretix.cfg
# chown -R 15371:15371 /etc/pretix/
# chmod 0700 /etc/pretix/pretix.cfg
```

# Pretix docker
```
docker pull pretix/standalone:stable
```
`docekr run --name pretix f92acea5ec64`