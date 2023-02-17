---
title: "Configure Maven Project"
date: 2023-02-14T11:54:44+01:00
draft: true
---

In this section, we configure Java GUI application which uses Maven as build tool. We will use a [sample JavaFX application](https://github.com/bitshifted/ignite-maven-plugin/tree/main/samples/simple-javafx-app) used in [Ignite Maven plugin](https://github.com/bitshifted/ignite-maven-plugin). You can clone the entire Git repository or just download the source for the sample.


This application uses Java 17, so you will need this Java version in order to build it and deploy it. It also requires Maven 3.

What we need to do here is to configure Ignite Maven plugin to perform deployment of our sample application to Backstage server we configured in previous step. We just need to add the following
to POM file:

```xml
<build>
    <plugins>
        .....
        <plugin>
            <groupId>co.bitshifted.appforge</groupId>
            <artifactId>ignite-maven-plugin</artifactId>
            <version>{ current version here }</version>
            <executions>
                <execution>
                    <id>ignite</id>
                    <goals>
                        <goal>ignite</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```
This configuration will execute the plugin during deploy phase. By default, plugin expects configuration in the file `ignite-config.yml` in the current directory.

You can use different file name with configuration option `configFile`:

```xml
<plugin>
    <groupId>co.bitshifted.appforge</groupId>
    <artifactId>ignite-maven-plugin</artifactId>
    <version>{ current version here }</version>
    <executions>
        <execution>
            <id>ignite</id>
            <goals>
                <goal>ignite</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <configFile>my-config-file.yaml</configFile>
    </configuration>
</plugin>
```

Next step is to create the configuration file itself.
