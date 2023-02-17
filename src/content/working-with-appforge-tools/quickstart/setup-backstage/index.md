---
title: "Setup Backstage server"
date: 2023-02-06T20:04:03+01:00
draft: true
---

In this section, we'll create a Docker Compose file to launch Backstage server. Docker Compose creates all the dependencies required to run
a server. Configuration file can be found bellow:

```yaml
---
version: "3.9"
services:
  backstage-db:
    image: mysql:8.0.29
    cap_add:
      - SYS_NICE
    restart: always
    environment:
      - MYSQL_DATABASE=${DB_NAME}
      - MYSQL_USER=${DB_USER}
      - MYSQL_PASSWORD=${DB_PASSWORD}
      - MYSQL_RANDOM_ROOT_PASSWORD=yes
    healthcheck:
      test: ["CMD", "mysqladmin" ,"ping", "-h", "localhost"]
      timeout: 10s
      retries: 10
    volumes:
      - dbstore:/var/lib/mysql
    networks:
      - db-net
  launchcode:
    image: ghcr.io/bitshifted/launchcode:${LAUNCHCODE_VERSION}
    restart: always
    volumes:
      - workdir:/tmp
    networks:
      - tools-net
  backstage-tools:
    image: ghcr.io/bitshifted/backstage-tools:${BACKSTAGE_TOOLS_VERSION}
    privileged: true
    restart: always
    volumes:
      - workdir:/tmp
    networks:
      - tools-net
  backstage-server:
    image: ghcr.io/bitshifted/backstage:${BACKSTAGE_VERSION}
    restart: always
    environment:
      - BACKSTAGE_DB_NAME=${DB_NAME}
      - BACKSTAGE_DB_USER=${DB_USER}
      - BACKSTAGE_DB_PASSWORD=${DB_PASSWORD}
    depends_on:
      backstage-db:
        condition: service_healthy
      launchcode:
        condition: service_started
      backstage-tools:
        condition: service_started
    volumes:
      - workdir:/tmp
      - contentdir:/var/backstage/content
      - jdkrootdir:/var/backstage/jdk-root
      - releasedir:/var/backstage/release
    networks:
      - db-net
      - tools-net
    ports:
      - '8080:8080'
volumes:
  dbstore:
    driver: local
  workdir:
    driver: local
  contentdir:
    driver: local
  jdkrootdir:
    driver: local
  releasedir:
    driver: local
networks:
  db-net:
  tools-net:
```

On closer look, we can see that there are several containers in use here:
* `mysql` - MySQL database server used by Backstage web application
* `launchcode` - this container contains source code to build custom native launcher for deployed applications
* `backstage-tools` - external tools used to create native installer packages for supported operating systems
* `backstage` - this is Backstage web application itself

In addition to this, we need an `.env` file which contains values for variable defined in Docker Compose file:

```bash
DB_NAME=backstagedb
DB_USER=dbuser
DB_PASSWORD=dbuser-pass
LAUNCHCODE_VERSION=1.0.1
BACKSTAGE_TOOLS_VERSION=1.1.0
BACKSTAGE_VERSION=latest
```

You can customize these values to your liking.

## Launch the Backstage web application

Assuming you have written compose file as `docker-compose.yaml`, simply run:

```bash
docker compose up -d
```

This will start the application in daemon mode. It will be accessible in your host on port 8080.

If you created a file with different name, run the following command:

```bash
docker compose -f my-file-name.yaml up -d
```
