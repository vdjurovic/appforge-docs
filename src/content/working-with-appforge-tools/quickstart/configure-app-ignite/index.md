---
title: "Create basic Ignite configuration"
date: 2023-02-14T14:33:30+01:00
draft: true
---

Configuration files are in YAML format which Ignite Maven plugin uses to construct application installers and provide updates. Being textual files, you can write them by hand, or you can use [Ignite GUI tool](https://github.com/bitshifted/ignite).

In this section, we will describe how to create configuration file using Ignite GUI.

## Installing Ignite

Keeping in line with "eating your own dog food" saying, Ignite is an application packaged and deployed using AppForge tools. It provides native installers and automatic updates. You can download the application for your platform [here](https://github.com/bitshifted/ignite).

## Configure server and project

This section deals with initial configuration of Ignite application and setting up your project.

### Configure server

Before you can continue working, you nee to configure Ignite to talk with the Backstage server (the one we just launched using Docker Compose). This needs to be done only once.

In Ignite menu, select *Configuration -> Server*, like in the image bellow:

{{< figure src="img/ignite-server-config.png" >}}

Popup window will open. Click *New Server* button, and in the popup windows that opens, enter information for your server:

{{< figure src="img/ignite-server-info.png" >}}

In this case, since server is running on your computer, and on port 8080 (configured in Compose file), enter `http://localhost:8080` as server URL. Server name can be any string (we use *my-server* in this example)

### Install Java runtime on server

Next step is to install required Java Runtime Environment on server. This is the Java runtime that we want to distribute with our application, not the one used to actually build the binary.

AppForge currently has a preconfigured Java runtimes from popular JDK vendors. You can select one of these runtimes to use with your application. This list is constantly updated to include new releases and new vendors.

To install required Java runtime, select *Configuration -> Java Platforms* from the main menu, as shown in the image bellow:

{{< figure src="img/ignite-install-java.png" >}}

New popup window will open, as shown in the image bellow. In the top combo box, select a server that you configured in previous step:

{{< figure src="img/ignite-java-list.png" >}}

When you select the server, the list of currently installed runtimes will appear. Since we currently have no installed Java runtimes, this list will be empty.

To install new Java runtime, click the *Install new JDK* button. This will load the list of JDKs available to be installed. From this list, select the version you want to install. For our example, we will install Eclipse Temurin Java 17, latest version:

{{< figure src="img/ignite-java-select.png" >}}

To install selected version, click *Install selected JDK* button. New popup message will show up, asking if you want to enable automatic updates, ie. always updating selected JDK to the latest version:

{{< figure src="img/ignite-java-auto-update.png" >}}

{{< hint type="note" >}}
Auto-update feature is currently disabled, so this selection will have no effect.
{{< /hint >}}

Final step is to confirm the installarion settings. If you are happy with the slection, just click *Yes* and  instalation will begin.

{{< figure src="img/ignite-java-confirm.png" >}}

Installation will now start. Installer will display current status as installation progresses.

{{< figure src="img/ignite-java-progress.png" >}}

Once the instalation is complete, Backstage server will have the following installed:

* Windows x64 version
* Mac OS x64 and ARM64 versions
* Linux x64 and ARM64 versions

### Create new application

Next step is to create an application entry in Backstage. It holds all the metadata for the application, like name, description, headline etc. Configuration file needs a unique ID of the application.

To create new application, select *Configuration -> Applications" menu entry:

{{< figure src="img/ignite-app-start.png" >}}

Popup window will open. On the top there's a *Servers* combo box. Here, you should select the server you configured in the first step.

Once server is selected, list box bellow will show the list of applications on server. Since we don't have any applications yet, the list will be empty. To create an application, click the *New application* button:

{{< figure src="img/ignite-app-new.png" >}}

Clicking *New application* button will open new window in which you can enter basic information for your application:

{{< figure src="img/ignite-app-info.png" >}}

The only required field in the name. Other fields are optional:

* *Headline* - short, one-sentence description or tagline (256 characters maximum)
* *Description* - more detailed description of the application (2K characters maximum)
* *Home page* - application home page URL
* *Publisher* - name of the publisher (either company or individual)
* *Publicher email* - publisher contact email

With this step, you've concluded basic Ignite configuration. In the next step, we'll configure application in more detail.
