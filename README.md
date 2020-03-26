# Tech contra virus - Docker

This repository contains the Docker code to make deploying the code in the related repo
[https://github.com/k-monitor/techkontrawirus](https://github.com/k-monitor/techkontrawirus)
easier.

## Running

    git clone https://github.com/k-monitor/techkontrawirus-docker.git
    cd techkontrawirus-docker
    cp .env-app.example .env-app
    cp .env-db.example .env-db

Edit the files .env-app and .env-db setting the values marked by '# Set this'.

    docker-compose build
    docker-compose up

At this point, the containers `techkontrawirus-app` and `techkontrawirus-db`
will be up and running.

The first time you run them, to init & seed the DB schema, run (the second
and third commands are executed inside `techkontrawirus-app` container):

    docker exec -it techkontrawirus-app /bin/bash
    php artisan migrate
    php artisan db:seed

The application will now be available at [http://localhost:4321](http://localhost:4321).

## Notes

After running the containers for the first time, the database files will be
persisted in the directory `techkontrawirus-mariadb-volume`.
