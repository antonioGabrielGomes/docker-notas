# PARTE 1
# Volumes
Tipo bind
# docker container run -ti --mount type=bind,src=/opt/giropops,dst=/giropops debian
Opção somente leitura
# docker container run -ti --mount type=bind,src=/opt/giropops,dst=/giropops,ro debian
Criar Volume do tipo volume
# docker volume create giropops
# docker volume inspect giropops
# docker container run -ti --mount type=volume,src=giropops,dst=/giropops debian
# docker volume rm volume_id

# Exemplo de container para backup
# docker volume create teste
# docker container run -ti --mount type=volume,src=teste,dst=/teste debian *** aqui a gente precisar criar alguma coisa na pasta  /teste e depois é só sair
# docker container run -ti --mount type=volume,src=teste,dst=/data --mount type=bind,src=/opt/backup,dst=/backup debian tar  -cvf /backup/bkp-log.tar /data


#### (CAI NA PROVA)
# docker container run -ti --mount type=bind,src=/volume,dst=/volume ubuntu
# docker container run -ti --mount type=bind,src=/root/primeiro_container,dst=/volume ubuntu
# docker container run -ti --mount type=bind,src=/root/primeiro_container,dst=/volume,ro ubuntu
# docker volume create giropops
# docker volume rm giropops
# docker volume inspect giropops
# docker volume prune
# docker container run -d --mount type=volume,source=giropops,destination=/var/opa  nginx
# docker container create -v /data --name dbdados centos
# docker run -d -p 5432:5432 --name pgsql1 --volumes-from dbdados -e POSTGRESQL_USER=docker -e POSTGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql
# docker run -d -p 5433:5432 --name pgsql2 --volumes-from dbdados -e  POSTGRESQL_USER=docker -e POSTGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql
# docker run -ti --volumes-from dbdados -v $(pwd):/backup debian tar -cvf /backup/backup.tar /data
####


# PARTE 1
# Dockerfiles

# (CAI NA PROVA)
# docker container run -ti -p 8080:80
# docker container run -ti -P (porta aleatória do host) 

# docker image build -t meu_apache:1.0.0 . --no-cache
# docker image build -t meu_apache:1.0.0 .


# PARTE 2

# docker commit -m "mensagem aqui" container_id
# tag na imagem gerada
# docker image tag id_imagem ubuntu_tag:1.0


# Docker hub
# mudar nome da imagem, ex: 
# docker image tag [image_id] antonioggca000/nomeDaImagem:1.0.0
# docker login 
# docker push antonioggca000/nomeDaImage:1.0.0

# Docker Registry
# docker container run -d -p 5000:5000 --restart=always --name registry registry:2
# docker image tag [image_id] localhost:5000/nome_da_image:1.0.0
# docker image push localhost/nome_da_image:1.0.0


FROM debian

RUN apt-get update && apt-get install -y apache2 && apt-get clean
ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL description="Webserver"

VOLUME /var/www/html/
EXPOSE 80

 

FROM debian

RUN apt-get update && apt-get install -y apache2 && apt-get clean
ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_DIR="/var/run/apache2"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL description="Webserver"

VOLUME /var/www/html/
EXPOSE 80

ENTRYPOINT ["/usr/sbin/apachectl"]
CMD ["-D", "FOREGROUND"]

 

package main
import "fmt"

func main() {
	fmt.Println("GIROPOPS STRIGUS GIRUS - LINUXTIPS")
}

 

FROM golang

WORKDIR /app
ADD . /app
RUN go build -o goapp
ENTRYPOINT ./goapp

 

FROM golang AS buildando

ADD . /src
WORKDIR /src
RUN go build -o goapp


FROM alpine:3.1

WORKDIR /app
COPY --from=buildando /src/goapp /app
ENTRYPOINT ./goapp

 

ADD => Copia novos arquivos, diretórios, arquivos TAR ou arquivos remotos e os adicionam ao filesystem do container;

CMD => Executa um comando, diferente do RUN que executa o comando no momento em que está "buildando" a imagem, o CMD executa no início da execução do container;

LABEL => Adiciona metadados a imagem como versão, descrição e fabricante;

COPY => Copia novos arquivos e diretórios e os adicionam ao filesystem do container;

ENTRYPOINT => Permite você configurar um container para rodar um executável, e quando esse executável for finalizado, o container também será;

ENV => Informa variáveis de ambiente ao container;

EXPOSE => Informa qual porta o container estará ouvindo;

FROM => Indica qual imagem será utilizada como base, ela precisa ser a primeira linha do Dockerfile;

MAINTAINER => Autor da imagem; 

RUN => Executa qualquer comando em uma nova camada no topo da imagem e "commita" as alterações. Essas alterações você poderá utilizar nas próximas instruções de seu Dockerfile;

USER => Determina qual o usuário será utilizado na imagem. Por default é o root;

VOLUME => Permite a criação de um ponto de montagem no container;

WORKDIR => Responsável por mudar do diretório / (raiz) para o especificado nele;
