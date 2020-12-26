---
title: "Development Environment - Maven"
tags: [build]
keywords: sonarqube, sonarcloud, environment, ci, continuousintegration
sidebar: developer_guide_sidebar
permalink: developer_guide_environment_maven.html
folder: developer_guide
toc: true
---

## Overview

<img src="/images/developer_guide/maven.svg" alt="Apache Maven logo" style="float: right;"/>

Anchor uses [Apache Maven](https://maven.apache.org/) as a build automation tool.

Maven combines:
- a build-tool (similar to Ant), and
- repositories for storing versioned artefacts (JARs).

{% include important.html content="Anchor currently uses **Maven Version 3.3.9**." %}

There exists a private local maven repository (`$HOME/.m2/` sub-directory in your home-directory) where artifacts may be stored, before being synchronized with the [main repository server for packages](
See [SonarCloud](/developer_guide_environment_sonarcloud.html) for the repository server that Anchor uses.).

{% include note.html content="A file `pom.xml` specifies build-related settings." %}

### Plugins

Maven's configuration combines many plugins, and some [key third-party libraries](/developer_guide_environment_key_libraries.html#maven-plugins) are integrated
via this mechanism into Anchor's build process.

### Example commands

Tutorials on Maven are widely available. Here follows a very brief introduction.

Maven's build process is centered around [https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html](lifecycles and phases).

To perform a build task, simply open a command-shell and change directory to where a *pom.xml* is located. Then execute maven with a phase as an argument. All necessary prior phases are also executed.

For example, the following command, executes the *deploy* phase, which builds, installs the binary output in the local maven repository, and then copies the final binaries onto the repository-server.

{% include shellSingleLine.html
command="mvn deploy" %}

The following command will only execute only as far as the *install* phase.

{% include shellSingleLine.html
command="mvn install" %}

The following command will delete all binary-files (a different lifecycle).

{% include shellSingleLine.html
command="mvn clean" %}

These commands can be executed in the top-level directory (and thus applied to all sub-modules), or for a specific module only in the respective subdirectory.


## Installation {#install}

1. Download from [Apache Maven](https://maven.apache.org/)

2. Add the `bin/` directory to `$PATH`

3. Setup a `.m2/settings.xml` file as outlined below to access the Anchor repositories.


### Settings file

The project uses [GitHub Packages](https://github.com/features/packages) as a repository serve (provides versioned JARs) that is needed to build Anchor.

It is found at:
> https://maven.pkg.github.com/anchoranalysis/ANCHOR-REPOSITORY-NAME

where `ANCHOR-REPOSITORY-NAME` should be substituted with the respect repository name e.g. `anchor` or `anchor-plugins` etc.

This repository requires a [token](https://docs.github.com/en/free-pro-team@latest/packages/guides/configuring-apache-maven-for-use-with-github-packages) from GitHub to read from (and **requires credentials** from Owen Feehan to write to).

The [credentials](https://docs.github.com/en/free-pro-team@latest/packages/guides/configuring-apache-maven-for-use-with-github-packages) (username/token) should be specified in your private maven settings, e.g. in `$HOME/.m2/settings.xml` where `$HOME` is the user's *home directory*`.

{% include note.html content="On Windows, a user's home directory is typically found at `C:\Users\owen\` (replace the username)." %}

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd">
    <servers>
    <server>
        <id>github</id>
        <username>YOUR_USERNAME</username>
        <password>YOUR_TOKEN</password>
    </server>  
    </servers>

    <profiles>
        <profile>
            <id>anchorTestConfig</id>
            <properties>
                <anchor.home.test>C:\SOMEDIRECTORY\Apps\anchor\</anchor.home.test>
                <anchor.home.deploy>C:\SOMEDIRECTORY\Apps\anchor\</anchor.home.deploy>
                <maven.test.skip>true</maven.test.skip>
                <maven.javadoc.skip>true</maven.javadoc.skip>
            </properties>
        </profile>
    </profiles>

    <activeProfiles>
        <activeProfile>anchorTestConfig</activeProfile>
    </activeProfiles>

</settings>
```

Replace `YOUR_USERNAME` and `YOUR_TOKEN` appropriately, and update the `anchor.home.test` and `anchor.home.deploy` variable to match the path where Anchor will be deployed to.

## Multi-module projects

Anchor uses a **multi-module** setup with a hierarchy of `pom.xml` files from the top-level directory to each nested module.

{% include tip.html content="The module-specific `pom.xml` inherits certain settings from the `pom.xml` in its parent-folders." %}

Each module pom.xml outlines an `artifiactID` and `version` that determine how it is stored in the repository server.

Actually Anchor uses **several multi-module projects**, each in its own repository. 

{% include important.html content="The pom.xml in the [anchor-pom repository](https://github.com/anchoranalysis/anchor-pom) provides a top-level base POM across repositories." %}

This is a convenient location for global settings for the build process.

### Steps for adding a new plugin module

Based in the root directory of a multi-module respository:

1. Create a sub-directory containing the new module in [anchor-plugins](https://github.com/anchoranalysis/anchor-plugins) or [anchor-plugins-gpl](https://github.com/anchoranalysis/anchor-plugins-gpl) depending on license.
2. Add module name to the `pom.xml` in the root directory of this repository.
3. Add a dependency in `anchor-assembly`:
    1. if it's the regular MIT license (i.e. not-GPL), then add a dependency in [/addplugins/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/addplugins/pom.xml) 
    2. if it's GPL, then add a dependency in [/anchor-assembly/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/pom.xml)

{% include links.html %}