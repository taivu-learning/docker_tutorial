# Docker tutorial

Ref: https://github.com/docker/getting-started

This tutorial includes basic instructions for:

- Docker basic: docker images & containers, docker volume, docker network, ... 
- Docker compose (Example: App container & DB container)

(Prerequisites: docker installed. (Can use docker desktop / for Mac))

## Run each container separately:

Open bash/Powershell to the directory of this repo, then use this command:

- Run Mysql container:

```
docker run -dp 13306:3306 --network todo-app --network-alias mysql -v todo-mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=todos mysql:5.7
```

- Run app container:

```
docker run -dp 3000:3000 -w /app -v "$(pwd):/app" --network todo-app -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=secret -e MYSQL_DB=todos node:12-alpine sh -c "
yarn install && yarn run dev"
```

## Using `docker compose` to manage containers:

Use this command only:

```
docker-compose up -d
```

## Access the application

Open your browser and access:

```
http://localhost:3000/
```