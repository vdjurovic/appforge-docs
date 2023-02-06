---
title: "How It Works?"
date: 2023-02-03T23:05:38+01:00
draft: true
---

# How AppForge generates installers and updates?

There are several components that comprise AppForge as a complete solution. These components are:

* [Ignite](https://github.com/bitshifted/ignite) - GUI tool for generating configuration files needed for the process
* [Backstage](https://github.com/bitshifted/backstage) - server-side web applications which generates installationa and update packages, and makes them available to users
* [Ignite Maven Plugin](https://github.com/bitshifted/ignite-maven-plugin) - build-time plugin which consumes configuration files created ty Ignite tool and uses them to create deployment packages

Although there are some additional components, these are the ones developers will interact with the most

Complete process for creating deployment packages can be described in the following diagram:

{{< img-figure src="img/how-it-works-diagram.svg" >}}

1. Developer creates deployment configuration file (by default, named `ignite-config.yml`). It can be either written by hand or using [Ignite](https://github.com/bitshifted/ignite) GUI tool. 
2. Configuration file is consumed by the build plugin (currently, only Maven plugin exists). Build plugin constructs deployment package with all the information and
resources needed for successful deployment
3. Build plugin sends deployment package to the build server. 
4. Server uses information from deployment package to create native installers for all requested platforms. It makes them available for download and installation.
5. Along with installers, server also creates update packages which are used for automatic updates.