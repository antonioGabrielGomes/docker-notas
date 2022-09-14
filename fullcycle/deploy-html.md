sudo docker run --name nginx -d -p 8080:80 nginx
sudo docker exec nginx ls
sudo docker exec -it nginx bash

docker build -t dockerfile-golang .
docker run -d -p 8080:8080 dockerfile-golang:latest





