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


####
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

