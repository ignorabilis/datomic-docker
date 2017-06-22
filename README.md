# datomic-docker

This repository contains a Dockerfile and configuration used for building a production Datomic Console and Datomic Starter DB.

## Prerequisites

* Docker and Docker Compose
* A server for the build

## Getting Started

1. Pull this repo
2. Add the `credentials.txt` files in *both* the **datomic-console** and **datomic-pro-starter** folders. The files must contain username:download-key
3. Add your Datomic Pro Starter Edition license key to the `datomic-pro-starter/config/dev-transactor.properties` file
4. Go to each folder and build using *docker build -t ignorabilis/datomic-console .* or *docker build -t ignorabilis/datomic-pro-starter .*
5. Push the resulting docker images
6. Run both images on the dedicated servers using the *docker-compose.yml*
7. The console will be available on port 9000 of your docker host's
   address. If you use Docker for (Win|Mac), it's just `localhost`.
   Ohterwise, use `echo $DOCKER_HOST` or `docker-machine env <local-docker-machine-vm-name>`to see what that is.
   E.g. [http://192.168.59.103:9000/browse](http://192.168.59.103:9000/browse)

## Load Existing Data

Have a look at restore-db.sh - it can be used with the following instruction

    docker exec dockerdatomicexample_datomicdb_1 restore-db dev

##  All rights reserved

Copyright (c) 2017 Ignorabilis Op. Ltd.
