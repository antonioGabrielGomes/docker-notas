# DAY 01

# Verificar configurações do container:
$ sudo docker container inspect nome_container

# Entrar no container:
$ sudo docker container attach nome_container

# Cria um processo de terminal no container:
$ echo "TEXTO" > /usr/share/nginx/html/index.html

$ sudo docker container exec -ti nome_container bash 

# Logs do container:
$ sudo docker container logs -f nome_container

# Informações do container recurso:
$ sudo docker container stats nome_container
$ sudo docker container top nome_container

# Exemplo shell script:
$ while true; do curl localhost:8080; done

# Programa para simular stress no sistema:
$ apt-get update && apt-get install stress
$ stress --cpu 1 --vm-bytes 128M --vm 1
$ stress --vm 1 --cpu 1 --vm-bytes 64M
$ stress --vm 1 --vm-bytes 64M
$ stress --vm 1 --cpu 1 --vm-bytes 64M
$ stress --cpu 1 --vm-bytes 64M

# Verificar informações de processado no linux
$ cat /proc/cpuinfo

# Passando recursos
$ sudo docker container run -d -m 128M nginx
$ sudo docker container run -d -m 128M --cpus 0.5 nginx
### atualizando recurso da cpu e memoria
#### 0.2 em porcentagem 20% de 1 core
#### 0.6 - 60 % de 1 core
#### 2 core
#### 1 core
$ sudo docker container update --cpus 0.2 nome_container
$ sudo docker container update --cpus 0.4 --memory 64M nome_container

# Volumes tipo bind
$ mkdir /opt/giropops
$ docker container run -ti --mount type=bind,src=/opt/giropops,dst=/giropops debian
-- opção somente leitura ro
$ docker container run -ti --mount type=bind,src=/opt/giropops,dst=/giropops,ro debian


# Volumes tipo volume
$ docker volume ls
$ docker volume create giropops
$ docker volume inspect giropops

$ docker container run -ti --mount type=volume,src=giropops,dst=/giropops debian


# remover volume
$ docker volume rm giropops

# criar arquivo dentro do volume via exec
$ docker container exec -ti container_id touch /paht/name_file

#
# Data Only e Prune
$ docker volume prune
$ docker container prune


Compartilhamento de volume - APENAS DIDÁTICO:
$ docker container create -v /data --name dbdados centos

$ docker container run -d -p 5432:5432 --name pgsql1 --volumes-from dbdados -e POSTGRESQL_USER=docker -e POSTGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql

$ docker container run -d -p 5433:5432 --name pgsql2 --volumes-from dbdados -e POSTGRESQL_USER=docker -e POSTGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql


RESUMO

Comandos Utilizados:

# curl -fsSL https://get.docker.com/ | bash
# docker version
# docker container ls

 

# docker container run hello-world
# docker image ls
# docker ps
# docker container ls
# docker container ls -a
# docker container run -ti centos:7
# docker container run -ti ubuntu
# docker container -d nginx
# docker container attach [CONTAINER ID]
# docker container exec -ti [CONTAINER ID] [COMANDO]
# docker container start [CONTAINER ID]
# docker container stop [CONTAINER ID]
# docker container restart [CONTAINER ID]
# docker container pause [CONTAINER ID]
# docker container unpause [CONTAINER ID]

 

# docker container start [CONTAINER ID]
# docker container stop [CONTAINER ID]
# docker container restart [CONTAINER ID]
# docker container pause [CONTAINER ID]
# docker container unpause [CONTAINER ID]
# docker container inspect [CONTAINER ID]
# docker container logs -f [CONTAINER ID]
# docker container rm [CONTAINER ID]
# docker container attach [CONTAINER ID]
# docker container rm -f [CONTAINER ID]
# docker container exec -ti [CONTAINER ID] [COMANDO]
# docker container run -d nginx

 

# docker container stats [CONTAINER ID]
# docker container top [CONTAINER ID]
# docker container run -d -m 128M --cpus 0.5 nginx
# docker container update --memory 64M --cpus 0.4 nginx
# docker container inspect [CONTAINER ID]
# docker container stats [CONTAINER ID]
# docker container top [CONTAINER ID]

Comando executados dentro do container:

# apt-get update
# apt-get install stress
# stress --cpu 1 --vm-bytes 128M --vm1

 

# docker image build -t toskeira:1.0
# docker image ls
# docker container run -d toskeira:1.0
# docker container logs -f [CONTAINER ID]

No Dockerfile:

FROM debian 
LABEL app="Giropops" 
ENV JEFERSON="LINDO" 
RUN apt-get update && apt-get install -y stress && apt-get clean 

CMD stress --cpu 1 --vm-bytes 64M --vm1


