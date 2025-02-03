
# IMPORTANTE
```
docker run --name db-container -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=universe -v mysql_data:/var/lib/mysql -d mysql:latest
```
## Instalatu
```
sudo snap install docker
```

## DockerFile
```
FROM ubuntu:latest

COPY ./file1 ./file1_en_docker

RUN echo "Se ejecuta el docker IMAGE"

ENTRYPOINT ["echo","Se ejecuta el CONTENEDOR"]

EXPOSE 80
```

## Irudia sortu
```
sudo docker build -t ”Nombre para la imangen” .
```

## Irudia sortu eta asieratu
```
sudo docker run ”Nombre de la imangen”
```

## Irudia asieratu
```
sudo docker start “contenedor”
sudo docker stop “contenedor”
```


## Docker-compose.yaml
```
version: '3'

services:

  mysql:

    container_name: mysql_compose

    image: mysql:5.7

    restart: always

    volumes:

      - ./mysql-data:/var/lib/mysql

    ports:

      - 3306:3306

    environment:

      - MYSQL_ROOT_PASSWORD=123

      - MYSQL_DATABASE=errepasoa
```

## Irudi bat deskargatu
```
sudo docker pull “imagen descargada”
```


