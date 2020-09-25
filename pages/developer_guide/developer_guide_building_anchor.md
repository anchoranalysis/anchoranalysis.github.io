---
title: "Developer Guide - Building Anchor"
tags: [build, maven, getting_started]
keywords: maven, settings, repository, build, release
sidebar: developer_guide_sidebar
permalink: developer_guide_building_anchor.html
folder: developer_guide
---

## Maven

Anchor uses [Apache Maven](https://maven.apache.org/) as a build tool. As a prior step, Maven should be installed locally, [configured for the Anchor project](/developer_guide_environment_maven.html#install).

## Assembly

The *anchor-assembly* is a special module that doesn't generate a .jar artifact, but rather assembles the output of other modules (artifacts) into an [Anchor distribution](developer_guide_anchor_distribution.html).

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

The order is important to match the[ dependency structure between repositories](/developer_guide_architecture_overview.html#repositories).

Finally, change into `anchor-assembly/` and execute a similar command (but targetting a particular operating-system).

```
 mvn "-Djavacpp.platform=windows-x86_64" deploy
```

or with `linux-x86_64`, `macosx-x86_64` etc. for [other operating systems](https://github.com/bytedeco/javacpp-presets).

The final command will copy a distribution into ```anchor.home.deploy``` with needed native libraries for the chosen operating system.

{% include links.html %}