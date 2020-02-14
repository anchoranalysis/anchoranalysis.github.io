---
title: "Building anchor"
tags: [build, maven, getting_started]
keywords: maven, settings, repository, build, release
sidebar: developer_guide_sidebar
permalink: developer_guide_intro_building_anchor.html
folder: developer_guide
---

## Maven

Anchor uses [Apache Maven](https://maven.apache.org/) as a build tool. As a prior step, Maven should be installed locally, and its binary directory should be placed in the system PATH variable.

{% include note.html content="Anchor currently uses **Maven Version 3.3.9**." %}

Tutorials on Maven are widely available. Here follows a very brief introduction.

Maven combines a build-tool (similar to Ant) with repositories for storing versioned binary-artifacts (e.g. JARs) that are created during the building process, together with dependencies.

There exists a private local maven repository (`$HOME/.m2/` sub-directory in your home-directory) where artifacts may be stored. This is typically combined with public maven repositories that provide third-party dependencies, and in our case, an organisational maven repository, called the *Anchor Maven Repository*. User-specific settings for the build can be set in `$HOME/.m2/settings.xml`.

{% include note.html content="A file `pom.xml` specifies build-related settings." %}

### Multi-module projects

Anchor uses a **multi-module** setup, where there is a hierarchy of `pom.xml` files, from the top-level directory to each nested module. The module-specific `pom.xml` inherits certain settings from the `pom.xml` in its parent-folders.
Each module pom.xml outlines an artifiactID and version, that determines how it is stored in the repository server.

Actually Anchor uses *several* multi-module projects, each in its own repository. And the pom.xml in [anchor-pom repository](https://bitbucket.org/anchorimageanalysis/anchor-pom/src/master/) provides a top-level base POM from which all other projects inherit. This is a convenient location for global settings for the build process.

## Anchor repository server

This is an organisational repository, specific to Anchor, that provides three functions:

 * It stores versioned-jars of Anchor.
 * It provides several third-party dependencies that don't have corresponding public repositories.
 * It mirrors and caches public repositories for quicker downloads of dependencies.

It is found at:
> http://maven.anchoranalysis.org:8081/nexus/

Currently, this repository requires credentials to access, either to download-from (*read*) or to deploy-to (*write*). After Anchor is publicly released, public read-only access will be provided. Please contact Owen Feehan to obtain access to the repository.
The repository also provides a web application at the same URL that provides for certain functions (search, upload).

The credentials (username/password) should be specified in your private maven settings, e.g. in *operating system home directory*/.m2/settings.xml

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd">
  <servers>
    <server>
		<id>anchor</id>
		<username>yourusername</username>
		<password>yourpassword</password>
	</server>
    <server>
		<id>anchor-releases</id>
		<username>yourusername</username>
		<password>yourpassword</password>
	</server>
       <server>
		<id>anchor-snapshots</id>
		<username>yourusername</username>
		<password>yourpassword</password>
	</server>
	<server>
		<id>anchor-thirdparty</id>
		<username>yourusername</username>
		<password>yourpassword</password>
	</server>
  </servers>

  <profiles>
	    <profile>
	      <id>anchorTestConfig</id>
	      <properties>
		     <anchor.home.test>C:\Users\SOMEUSER\Apps\anchor\</anchor.home.test>
		     <anchor.home.deploy>C:\Users\SOMEUSER\Apps\anchor\</anchor.home.deploy>
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

Replace *yourusername* and *yourpassword* appropriately, andupdate the ```anchor.home.test``` and anchor.```home.deploy``` variable to match the path where anchor is stored).


## Example commands

Maven's build process is centered around [https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html](lifecycles and phases).

To perform a build task, simply open a command-shell and change directory to where a *pom.xml* is located. Then execute maven with a phase as an argument. All necessary prior phases are also executed.

For example, the following command, executes the *deploy* phase, which builds, installs the binary output in the local maven repository, and then copies the final binaries onto the repository-server.
> mvn deploy

The following command will only execute only as far as the *install* phase.
> mvn install

The following command will delete all binary-files (a different lifecycle).
> mvn clean

These commands can be executed in the top-level directory (and thus applied to all sub-modules), or for a specific module only in the respective subdirectory.


## Assembly

The *anchor-assembly* is a special module that doesn't generate a .jar artifact, but rather assembles the output of other modules (artifacts) into an [Anchor distribution](developer_guide_intro_anchor_distribution.html).

It produces its output (after *mvn deploy*) in a sub-directory:
> anchor-assembly/target/anchor-assembly-*version*-dist/

where *version* is replaced by the current version identifier (e.g. 0.0.1-SNAPSHOT).

And as a further step, it copies this output into the path defined by ```anchor.home.deploy``` in your ```$HOME/.m2/settings.xml``` (see previously). This is a convenient place to store your primary anchor distribution on your file-system, and its **bin/** directory can be added to the System path.

## Complete build of Anchor

To completely build Anchor from scratch. Pre-conditions:

* You've learnt Maven basics.
* You've configured the ```$HOME/.m2/settings.xml``` file.
* You've cloned all necessary Anchor Java repositories from [GitHub](https://github.com/anchoranalysis/) (see below).

Then execute the command ```mvn deploy``` in the parent directory of each repository **IN THIS ORDER**.

1. `anchor-pom/`
2. `anchor/`
3. `anchor-plugins/`
4. `anchor-plugins-gpl/`
5. `anchor-gui/`
6. `anchor-assembly/`

The order is important to match the dependency structure between repositories, as viewable [here](https://bitbucket.org/anchorimageanalysis/anchor/wiki/Architecture%20of%20Anchor).

The final command will copy a distribution into ```anchor.home.deploy```.