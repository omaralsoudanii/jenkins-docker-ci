# jenkins-docker-ci

Docker setup for Jenkins with docker plugin integration

![jenkins](https://user-images.githubusercontent.com/7079173/133009029-aaec7989-1c9b-433d-9fc3-60e6dfb8d9a7.png)

## Why

- If you want to learn Jenkins and try some piplines, this will save you the headache of setting it up yourself
- If you want to integrate Jenkins into your stack, this can be a starter (you just add the SSL stuff, change hostname and you're good to go)
- If you read [Installing Jenkins](https://www.jenkins.io/doc/book/installing/docker/). This is basically it but with the ease of docker-compose and the addition of a reverse proxy

## Setup

**Note:** This assumes that you have port 80 free and unused since we're using it here for HAProxy

- Clone the repo
- Run `docker-compose up --build -d`
- Verify everything is working
- Go to http://localhost
- If everything works the first page will ask for 1 time password. You can find the password through jenkins container logs
  ```bash
  docker --tail 100 -f mk-jenkins
  ```
  paste it in the browser then go through the wizard of setting up an admin user

- Most things will work, but to use Jenkins with full capabilities then using it on a production or any valid server is advised

## Features

- Full Jenkins ecosystem with docker integration (the ability for Jenkins to build by using docker)
- Lightweight, all images used are alpine based
- Safe, no containers run using root user
- Easy to setup (development and production)
- Decoupled and extendable, you can pick only the containers you need and throw the rest. Or maybe switch HAProxy with your favourite webserver
- Clean removal (see section below)


## Uninstall
- Run `docker-compose down -v` and it will remove everything related to this repo (even the volumes)
