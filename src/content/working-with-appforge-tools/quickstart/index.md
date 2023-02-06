---
title: "Quickstart"
date: 2023-02-06T19:45:36+01:00
draft: true
---

In this section, we'll go trhough steps  needed to quickly setup and configure AppForge tools. Specifically, we'll go through the following:

* configure and launch [Backstage](https://github.com/bitshifted/backstage) server using Docker Compose. This gives you complete functioning server for downloading installers and serving updates
* create sample JavaFX application Maven project and configure [ignite-maven-plugin](https://github.com/bitshifted/ignite-maven-plugin)  
* create simple configuration file (using [Ignite](https://github.com/bitshifted/ignite) tool) to deploy the application and create installers
* install application, deploy update and see how automatic updates work

## Prerequisites

For this tutorial, you will need the following software:
* [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/)
* JDK version 17 or higher. Although AppForge tools support Java 8 and higher, this particular example uses Java 17
* Maven version 3.x.x