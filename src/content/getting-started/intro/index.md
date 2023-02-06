---
title: "Introduction"
date: 2023-02-03T15:53:00+01:00
draft: true
---

{{< toc >}}

# What is AppForge?

AppForge is a complete solution for automatic deployment and updating of cross-platform desktop applications. But, what does that actually mean? In essence,
AppForge provides the following benefits to developers:

* generates native installation packages for supported platforms (Windows, Mac OS X, Linux)
* integrates updater with the application which checks for new versions on startup
* provides a web application which users can use to download installers and which serves updates

In addition to this, AppForge provides tools for developers to easily integrate it into development workflow.

## Supported platforms

Currently, AppForge can generate installers in the following formats:

* Windows - `.exe` installer wizards, with no need for administrator level access (only `x64` CPU architecture)
* Mac OS X - `.dmg` packages, for both Intel and ARM Macs
* Linux - `.deb`, `.rpm` and `.tar.gz` packages, for Intel and ARM CPUs

{{< hint type=important title="Mac OS Packages are not signed" >}}
At this moment, there is no support for signing Mac OS X packages. This meanss that users need to explicitely allow your application to run.

Support for signing Mac OS X packages is on the roadmap.
{{< /hint >}}

{{< hint type=note title="Linux non-root install" >}}
On Linux, installing `.deb` and `.rpm` packages requires root access. Using `.tar.gz` package, any user can install the application
{{< /hint >}}

## Supported programming languages

Currently, AppForge provides support only for applications written in Java or any other JVM languages (eg. Kotlin, Scala, Clojure`). Swing and JavaFX are
supported out of the box, while other UI toolkits (like SWT) need to be configured manually.

There is no technical obstacle to support other languages and UI toolkits, and additional support is on the roadmap.

# Application features

In additiona to native installer and updates, all applications deployed by AppForge get the following features out of the box:

* native launcher for the target platform, enabling higher level of integration with the target OS
* splash screen  for visual feedback about the application startup and improves user experience
* set of icons customized for target platform, making the application appear native
* additional integration with target OS, such as file associations, URL handlers etc.

All these features are explained in detail in the rest of documentation.
