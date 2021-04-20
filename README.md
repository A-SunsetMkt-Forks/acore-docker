# ACore docker-compose

The docker-compose file included in this folder provides you the azerothcore ready-to-use images.
It means that you will be able to run a clean azerothcore server without installing anything but docker.

NOTE: You can re-use this docker-compose configuration inside another project to test AzerothCore together
with another application, for instance an API or a website based on docker-compose. 

## Getting started

### Pull the latest images

```Bash
docker-compose pull
```

This command will pull latest images from the docker hub

### Setup the database

```Bash
docker-compose up ac-migrate
```

It runs the db-assembler tool to import all needed sql inside the mysql container

### Start services

```Bash
docker-compose up
```

To startup your authserver and worlserver

If you need to run them in background instead you can use the following command:

```Bash
docker-compose up -d
```

### Access the worlserver console

Run the following command to get the ID of the worlserver container:

```Bash
docker-compose ps
```

You will see a list of docker services. The worlserver service will have a name that ends with `_ac-worldserver_1`
Use that name for together with the following command:

```Bash
docker attach <your-service-name>
```

Now you can use the worlserver console to run azerothcore commands, including the "account create".

NOTE: you can detach from a container and leave it running using the CTRL-p CTRL-q key sequence.

### Update your services with latest images

You just need to combine the following 2 commands:

```Bash
docker-compose pull
docker-compose up ac-migrate
```

## Dev server (Experimental)

```Bash
docker-compose up ac-dev-server [-d]
```

The ac-dev-server is a special container that provides a complete workspace that includes all the sources and dependencies to build your own server.
This image is intended to be used together with the [VSCode Docker extension](https://code.visualstudio.com/docs/containers/overview)

NOTE: This container uses the same mysql instance of the ac-authserver/worldserver, so it's not suggested to use all the services to avoid
issues with the database consistence. However, you can always extends the docker-compose to add a second database instance (read the paragraph below)

NOTE 2: This is an experimental system. For complete support we still suggest to use the docker layer of the azerothcore-wotlk repository.


## Extends the default docker-compose

With the combination of the [docker-compose.override](https://docs.docker.com/compose/extends/) and the environment variables available to configure
the AzerothCore project, you can extend this docker by adding external and shared volumes, change configurations and even add multiple realms.

Check the examples folder that contains an override file ready to be used to implement a secondary worldserver

