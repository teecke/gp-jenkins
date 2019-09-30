# Generic Platform - Jenkins Service

## Overview

Teecke Generic Platform Jenkins Service.

Docker-ompose simple configuration to bring up the Jenkins service to the Generic Platform.

## Configuration

The service is formed by one container:

- **jenkins**: based on [teecke/jenkins-dind](https://hub.docker.com/r/teecke/jenkins-dind) docker image.

Use the `docker-compose.yml.sample` file as the source for your docker-compose configuration file.

## Operation

You must create a network called "platform_services" before start the services.

```console
docker network create platform_services
```

Then you can start the service with `docker-compose up -d` and stop it with `docker-compose stop` commands.

After the first run you can configure the service pointing a browser to <http://jenkins:8080>

There are two volumes created. All data and configuration are on those volumes, so never delete they.

```console
$ docker volume ls|grep "jenkins\|VOLUME"
DRIVER              VOLUME NAME
local               jenkins_docker
local               jenkins_jenkins_home
```

There are also two tasks `cleanup` and `backup` that you can execute as stand-alone

```console
$ docker-compose exec jenkins cleanup

[...]

$ docker-compose exec jenkins backup
```

...or using [Teecke Generic Platform](https://github.com/teecke/generic-platform) project.

The backup data will be stored in the `/var/backups/gp/jenkins/` directory of the container. You can copy the backup files with a simple "docker cp" command `docker cp $(docker-compose ps -q jenkins):/var/backups/gp gp`

## Known issues

None known
