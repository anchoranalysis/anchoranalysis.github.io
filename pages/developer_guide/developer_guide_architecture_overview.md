---
title: "Developer Guide - Architecture: Overview"
tags: [getting_started, architecture]
keywords: architecture, packages
sidebar: developer_guide_sidebar
permalink: developer_guide_architecture_overview.html
folder: developer_guide
---

## Repositories

The Anchor platform is spread across many library components (Maven *modules*), each packaged into a jar. Bundles of jars are packaged into different repositories:

* [anchor](https://bitbucket.org/anchorimageanalysis/anchor/src/master/) - main libraries used by Anchor, including frequently resused classes, and key abstract base classes
* [anchor-plugins](https://bitbucket.org/anchorimageanalysis/anchor-plugins/src/master/) - specialised functionality that provides concrete implementations of algorithms, features etc. by extending the abstract base classes in *anchor*
* [anchor-plugins-gpl](https://bitbucket.org/anchorimageanalysis/anchor-plugins/src/master/) - like anchor-plugins but for any source code that relies on a GPL library
* [anchor-gui](https://bitbucket.org/anchorimageanalysis/anchor-plugins/src/master/) - the GUI application
* [anchor-assembly](https://bitbucket.org/anchorimageanalysis/anchor-assembly/src/master/) - creates a [distribution of anchor](https://bitbucket.org/anchorimageanalysis/anchor/wiki/Anchor%20Distribution), by combining JARs from the above with launcher applications
* [anchor-pom](https://bitbucket.org/anchorimageanalysis/anchor-pom/src/master/) - a parent Maven POM file used by all other anchor Java projects

Each JAR is a top-level subdirectory in each repository, as per a Maven multi-module project.

![anchorRepositories.png](https://bitbucket.org/repo/KrRXkad/images/4270249235-anchorRepositories.png)


## Plugins

Anchor makes heavy use of the [Dependency Inversion principle from SOLID](https://itnext.io/solid-principles-explanation-and-examples-715b975dcad4). This means we use a lot of abstract base classes in the main anchor application, which other classes rely on BUT the concrete implementations are only provided by **plugins**. These plugins are only specified at run-time, and can be easily exchanged/extended/modified without changing the main (Anchor) code.

As a rule, the top-level library components should NEVER depend on the plugins, only the other way around. 

An exception is allowed for testing, and library classes are allowed depend on plugins, but confined to *test* scope only.

We insert plugins using [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection) (giving us [Inversion of Control](https://en.wikipedia.org/wiki/Inversion_of_control)) using BeanXML.


## Anchor Beans

Many classes (especially plugins) inherit from AnchorBean class. This makes the class an **anchor-bean**, which can be instantiated from XML (and have other convenient properties). More on this can be found in the [anchor-bean](https://bitbucket.org/anchorimageanalysis/anchor/src/master/anchor-bean/) project.

## Particular anchor-assembly modules

Some particular modules to take note of (all found in [anchor-assembly](https://bitbucket.org/anchorimageanalysis/anchor-assembly/src/master/)):
* [anchor-launcher](https://bitbucket.org/anchorimageanalysis/anchor-assembly/src/master/addplugins/anchor-launcher/): a command-line application for running experiments. This is the typical way to use anchor!
* [anchor-browser](https://bitbucket.org/anchorimageanalysis/anchor-assembly/src/master/addplugins/anchor-browser/): an application for starting the AnchorGUI browser
* [anchor-assembly](https://bitbucket.org/anchorimageanalysis/anchor-assembly/src/master/anchor-assembly/): a maven module that packages components together to form an [Anchor distribution](https://bitbucket.org/anchorimageanalysis/anchor/wiki/Anchor%20Distribution).

{% include links.html %}
