1. Docker machine
Para fazer a instalação do Docker Machine no Linux, faça:

# curl -L https://github.com/docker/machine/releases/download/v0.16.1
/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine
# chmod +x /tmp/docker-machine 
# sudo cp /tmp/docker-machine /usr/local/bin/docker-machine


Para seguir com a instalação no macOS:

# curl -L https://github.com/docker/machine/releases/download/v0.16.1
/docker-machine-`uname -s`-`uname -m` >/usr/local/bin/docker-machine 
# chmod +x /usr/local/bin/docker-machine

Para seguir com a instalação no Windows caso esteja usando o Git bash:

# if [[ ! -d "$HOME/bin" ]]; then mkdir -p "$HOME/bin"; fi
# curl -L https://github.com/docker/machine/releases/download/v0.16.1
/docker-machine-Windows-x86_64.exe > "$HOME/bin/docker-machine.exe"
# chmod +x "$HOME/bin/docker-machine.exe"


Para verificar se ele foi instalado e qual a sua versão, faça:

# docker-machine version

# docker-machine create --driver virtualbox linuxtips

# docker-machine ls

# docker-machine env linuxtips

# eval "$(docker-machine env linuxtips)"

# docker container ls

# docker container run busybox echo "LINUXTIPS, VAIIII"

# docker-machine ip linuxtips

# docker-machine ssh linuxtips

# docker-machine inspect linuxtips

# docker-machine stop linuxtips

# docker-machine ls 

# docker-machine start linuxtips

# docker-machine rm linuxtips

# eval $(docker-machine env -u)


2. Docker swarm
Ambiente: dev1 / dev2 / dev3

--- Leader
# docker swarm --help
# docker swarm init

Caso perca o cluster:
# docker swarm init --force-new-cluster

# docker node ls 
# docker node promote host_name  :::: promover outros nodes a managers
# docker node demote host_name   :::: remover node como manager

Remover node
# docker node rm -f nome_node

caso o cluster tiver mais de uma porta de rede
# docker swarm init --advertise-addr ip_da_porta_escolhida

buscar token utilizado
# docker swarm join-token worker
# docker swarm join-token manager

# docker swarm join-token --rotate manager  :::::: mudar chave do token
# docker swarm join-token --rotate worker  :::::: mudar chave do token

--- dev2
# docker swarm leave       ::::   sair do node swarm
# docker swarm leave -f    ::::   sair do node swarm caso seja manager

----------------------------
Exemplo:
# docker service create --name webserver --replicas 3 -p 8080:80 nginx
# docker service ps webserver
----------------------------

Update:
# docker node update --availability [params] [host_name]
params: drain  - limpe o nó
        pause  - não recebe novos containers
        active - pode receber novos containers
# docker node inspect hostname_do_host
Testar novamente o scale do service:
# docker service scale webserver=10
# docker service scale webserver=3

------
------
------
# Services

# docker service create --name giropops --replicas 3 -p 8080:80 nginx
# docker service ps giropops
# docker service inspect giropops --pretty

# docker service scale giropops=10  // up
# docker service scale giropops=3  // down

#  docker service logs -f giropops

# docker service rm giropops
--------------
# ex2 volumes:

# docker volume create giropops
# cd /var/lib/docker/volumes/giropops/_data

# docker service create --name giropops --replicas 3 -p 8080:80
  --mount type=volume,src=giropops,dst=/usr/shared/nginx/html nginx

------
Maquina principal:
sync de conteudo dos volumes entre os nós

# apt-get install nfs-server

# mkdir /opt/site

# nano /etc/exports

add options in end of file:

/var/lib/docker/volumes/giropops *(rw.sync.subtree_check)
/opt/site *(rw.sync.subtree_check)

# exportfs -ar

# echo "GIROPOPS STRIGUS GIRUS" > /opt/site/_data/index.html


------
Maquina secundaria:
# apt-get install nfs-utils nfs-common

# showmount -e ip_do_host

# mount -t nfs ip_do_host:/var/lib/docker/volumes/giropops /var/lib/docker/volumes/giropops/

--
# mount ip_do_host:/opt/site /var/lib/docker/volumes/giropops
--



--------------------------------------------------------
Exemplo:

# docker service create --name giropops --replicas 3 -p 8080:80 --mount type=volume,src=giropops,dst=/usr/share/nginx/html
	-- hostname sua_mae --limit-cpu 0.25 --limit-memory 64M --env blabla=blabla --dns 8.8.8.8 nginx


---
Network
---

# docker network ls 
# docker network create -d overlay giropops
# docker network ls

# docker service create --name nginx1 -p 8080:80 nginx

# docker network ls

# docker ps 


---------------------



# docker swarm init

# docker swarm join --token \ SWMTKN-1-100_SEU_TOKEN SEU_IP_MASTER:2377

# docker node ls

# docker swarm join-token manager

# docker swarm join-token worker

# docker node inspect LINUXtips-02

# docker node promote LINUXtips-03

# docker node ls

# docker node demote LINUXtips-03

# docker swarm leave

# docker swarm leave --force

# docker node rm LINUXtips-03

# docker service create --name webserver --replicas 5 -p 8080:80  nginx

# curl QUALQUER_IP_NODES_CLUSTER:8080

# docker service ls

# docker service ps webserver

# docker service inspect webserver

# docker service logs -f webserver

# docker service rm webserver

# docker service create --name webserver --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx

# docker network create -d overlay giropops

# docker network ls

# docker network inspect giropops

# docker service scale giropops=5

# docker network rm giropops

# docker service create --name webserver --network giropops --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx

# docker service update <OPCOES> <Nome_Service> 

 



--------------------------------------------------------
dev: 192.168.0.202  
dev3: 192.168.0.203 
dev3: 192.168.0.201 
--------------------------------------------------------


curl -fsSL https://get.docker.com | bash

hostname nome_aqui