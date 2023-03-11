---
title: "Detailed application configuration"
date: 2023-02-17T15:36:16+01:00
draft: true
---

In this section, we'll go through detailed configuration for deploying demo application. 

## Create a deployment

To start, we'll first need to create a *deployment*. Deployment is a configuration used to create installer and update package for the application. To create new deployment, select *File -> New deployment* menu entry.

{{< figure src="img/app-config-init.png" >}}

This will open the popup window where you can configure deployment. You only need to select project directory, which is the directory where you checked out application code in the first step of this quickstart tutorial. All other fields you can leave at default values, or customize them as needed.

When you create the deplyoment, it will appear in the sidebar tree.

{{< figure src="img/deployment-tree.png" >}}

If you click on the application, you will get a property sheet where you need to select an application you configured in previous step. This will record server URL and application ID in configuration file. These are required pieces of configuration for application deployment.

To do this, you first need to select a server from combo box. Once you select it, Ignite will load a list of application configured on that server. Select your application from the list.

{{< figure src="img/ignite-deployment-info.png" >}}

**Note:** Change in any of these configuration properties will enable *Save* button, so you can save your work.

## Create basic application information

Next step is to provide somne basic application information common to all platforms. If you expand application node in the left-hand tree view and select *Application Info* node, you can set basic application configuration. This is applicable to all supported platforms:

{{< figure src="img/basic-app-info.png" >}}

You can set the following properties here:

* supported operating systems (defaults to all supported OSes)
* executable name - name of resulting executable application launcher. Defaults to project name
* license - select a file containing project license
* splash screen - select an image file containing application splash screen

**Note**: Both license and splash screen have source and target text boxes. This allows you to use different file names and locations when deploying application. Default is to use the same file name and locatio relative to project root directory.

You can further customize application info for each operating system. Expand *Application info* node and you can select additional information for each supported operating system.

## Create Windows-specific application info

Selecting *Windows* node under *Application info* node enables you to set Windows-specific application properties:

{{< figure src="img/app-info-win.png" >}}

Windows deployment supports only `x64` CPU architecture, so this setting can not be changed.

You can select application icon which will be used on Windows by clicking on *Add icon* button. Windows icon should be in `.ico` format.

## Create Mac-specific application info

Mac OS information is almost identical to Windows.

{{< figure src="img/app-info-mac.png" >}}

The only difference is that Mac deployment by default targets both `x64` and `Aarch64` CPU architectures. You can customize this based on your requirements, if you don't want to target one or the other.

Icons for Mac OS should be in `.icns` file format.

## Create Linux-specific application info

Linux-specific application info is a bit more complex. There are several options you can customize here:

{{< figure src="img/app-info-linux.png" >}}

You can set the following options:
* CPU architecture - defaults to `x64` only, but you can also target `Aarch64`
* package type - default is all supported (`.deb, .rpm, .tar.gz`)
* icons - these can be in `.png` or `.svg` file format
* menu category - category in which your application will be displayed in start menu

## Creating JVM configuration

You can specify JVM configuration for running application. Select *JVM* node under your application settings:

{{< figure src="img/jvm-config.png" >}}

You can configure the following options here:
* Java implementation - here you can choose from the list of JDKs you installed in the [initial setup]({{< ref "working-with-appforge-tools/quickstart/configure-app-ignite#install-java-runtime-on-server" >}})
* main class -your application's main class
* module name (if your application uses Java module system)
* runtime arguments to be passed to application at launch time
* JVM oprtions
* JVM system properties
* add modules - equivalent to passing `--add-modules` option when launching application. This is comma-separated list of module names
* ignored modules - list of modules ignored by `jlink` when building application runtime

## Application resources

You can specify resources (file and folders) to be included in your application resulting package. Click on *Resources* node to add resources you want.
