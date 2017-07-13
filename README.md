symfony-docker
===========

A dockered symfony boilerplate.

## Instalation

Clone this repo
```
git clone https://github.com/dbiagi/symfony-docker.git
```

Enter the docker folder and build the images
```
cd docker/
docker-compose build
```

Run the containers
```
docker-compose up -d
```

Run composer install
```
docker exec -it docker_php_1 composer install
```

## Images
Here are the `docker-compose` service images.

`web`: [Nginx latest](https://hub.docker.com/_/nginx/) image

`php`: [PHP7.1-FPM](https://hub.docker.com/_/php/) image

`mariadb`: [MariaDB 10.3](https://hub.docker.com/_/mariadb/) image 

## Volumes
Description of named volumes.

`database`: Stores database files

`composer_cache`: Stores composer cache