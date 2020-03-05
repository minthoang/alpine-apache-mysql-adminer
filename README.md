# alpine-apache-mysql-adminer
* version: '3'

services:

  adminer:
    build:
      context: ./adminer
      dockerfile: Dockerfile
    restart: always
    depends_on:
      - db
    ports:
      - "8080:8080"

  apache: 
    hostname: $HOSTNAME
    build:
      context: ./apache
      dockerfile: Dockerfile
    restart: always
    depends_on:
      - db
    ports: 
      - "80:80"
      - "443:443"
    volumes: 
      - "./data:/usr/local/apache2/htdocs/"

  db:
    build:
      context: ./mysql
      dockerfile: Dockerfile
    restart: always
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: indochinaedu
