---
title: "Setup Backstage server"
date: 2023-02-06T20:04:03+01:00
draft: true
---

In this section, we'll create a Docker Compose file to launch Backstage server. Docker Compose creates all the dependencies required to run
a server. Configuration file can be found bellow:

```yaml
version: '3.8.'
services:
  mysql-db:
    image: mysql:8.0.29
    cap_add:
      - SYS_NICE
    restart: always
    environment:
      - MYSQL_DATABASE=backstagedb
      - MYSQL_ROOT_PASSWORD=root
    ports:
      - '3306:3306'
    volumes:
      - dbstore:/var/lib/mysql
      - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql
  backstage-tools:
    image: ghcr.io/bitshifted/backstage-tools:1.1.0
    privileged: true
    restart: always
    ports:
      - '3022:22'
    volumes:
      - /tmp:/tmp
  launchcode:
    image: ghcr.io/bitshifted/launchcode:1.0.1
    restart: always
    ports:
      - '2022:22'
    volumes:
      - /tmp:/tmp
volumes:
  dbstore:
    driver: local
```