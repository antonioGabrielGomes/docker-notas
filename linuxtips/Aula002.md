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