# Verificar configurações do container:
$ sudo docker container inspect nome_container

# Entrar no container:
$ sudo docker container attach nome_container

# Cria um processo de terminal no container:
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




