# Docker Environment Local

Author: Adrian Gheorghe <adrian.gheorghe.dev@gmail.com>

[![CircleCI](https://circleci.com/gh/adrian-gheorghe/docker-setup.svg?style=svg)](https://circleci.com/gh/adrian-gheorghe/docker-setup)

### Info
This setup is the base for all other docker based images and setups created by me and should make development using docker containers a lot easier. Using this base setup you will not have to keep track of ports or hostnames when setting up a new project. Using [Traefik](https://traefik.io/ "Traefik") as a load balancer you'll be able to use port 80 to access all your web containers. Also you'll be able to use subdomains of the following form: http://container.localhost.

[Portainer](https://www.portainer.io/) is set up to make container management easier.

This base setup contains a stack of containers with
- Traefik - reverse proxy container that routes all requests to their specific hosts without the need of using other ports than 80 and 443
- Whoami - container that returns ip and request information. This is to check if traefik is working correctly
- Portainer - docker container management ui. Interface that allows you to manage local containers, networks and so on. makes it a lot easier


## Setup and Usage
Go through the following in order to be able to use this setup

### Requirements
- Docker for Mac / Docker for Win / Docker and Docker Compose on Linux
- Nothing running on port 80/443 - You will need to stop / uninstall anything running on port 80 or 443 like a local apache or nginx install
- If you want to use this on other ports than 80 or 443 just change the ports section for the traefik service to what ports you want
ports:
  - "2380:80"      # The HTTP port
  - "8443:443"

### Create Network
You need to create the traefik-local network

```bash
docker network create traefik-local
```

### Raise Containers
docker-compose up -d


### Access
After creating the network and running docker-compose up you will be able to access the containers using the following addresses. Install portainer by setting a user/pass and set it to use your local stack and you are good to go!

http://whoami.localhost/ - whoami container
http://portainer.localhost/ - portainer ui for container management
http://localhost:8080/dashboard/ - web ui for traefik

## Container setups that plug into this

List of containers that plug into this.

Go Environment - https://github.com/adrian-gheorghe/docker-go
