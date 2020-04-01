---
title: "Architecture - Overview"
tags: [architecture]
keywords: architecture, packages
sidebar: developer_guide_sidebar
permalink: developer_guide_architecture_overview.html
folder: developer_guide
---

## Code Structure

### Repositories

The Anchor platform is spread across many library components bundled together into [source repositories](/developer_guide_repositories_overview.html).
- Java repositories with most code
- BeanXML repositories with projects, pipelines and tasks.
- Various other supporting smaller projects (website, plotting and machine-learning scripts).

### Modules

Each Java source repository is sub-divided into several modules, typically each producing a JAR.  Each module is sub-divided into packages, with a naming chosen to reflect the module.

{% include tip.html content="For a breakdown of modules and namespaces in each repository, see [Java Repositories](/developer_guide_repositories_overview.html#java)" %}

## Plugins

Anchor makes heavy use of the [Dependency Inversion principle from SOLID](https://itnext.io/solid-principles-explanation-and-examples-715b975dcad4).

This means we use a lot of abstract base classes in the anchor application, which other classes rely on *but* the concrete implementations are only specified at run-time.

This run-time specification occurs via one type of module called a **plugin**, which can be easily exchanged / extended / modified without recompiling the main code-base.

{% include warning.html content="As a rule, the top-level library components should *never* depend on the plugins, only the other way around." %}

We insert plugins using [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection) via BeanXML (giving us [Inversion of Control](https://en.wikipedia.org/wiki/Inversion_of_control)).

### Steps for adding a new plugin module

Based in the root directory of a multi-module respository:

1. Create a sub-directory containing the new module in [anchor-plugins](https://github.com/anchoranalysis/anchor-plugins) or [anchor-plugins-gpl](https://github.com/anchoranalysis/anchor-plugins-gpl) depending on license.
2. Add module name to the `pom.xml` in the root directory of this repository.
3. Add a dependency in `anchor-assembly`:
    1. if it's the regular MIT license (i.e. not-GPL), then add a dependency in [/addplugins/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/addplugins/pom.xml) 
    2. if it's GPL, then add a dependency in [/anchor-assembly/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/pom.xml)

## Anchor Beans

Many classes (especially plugins) inherit from AnchorBean class. This makes the class an [Anchor Bean](/developer_guide_anchor_beans.html), which can be instantiated from XML and has other convenient properties.

## Key entry-point modules

Some particular modules to take note of (all found in the [anchor-assembly repository](https://github.com/anchoranalysis/anchor-assembly)):
* [anchor-launcher](https://github.com/anchoranalysis/anchor-assembly/tree/master/addplugins/anchor-launcher): a command-line application for running experiments. This is the typical way to use anchor!
* [anchor-browser](https://github.com/anchoranalysis/anchor-assembly/tree/master/addplugins/anchor-browser): an application for starting the AnchorGUI browser
* [anchor-assembly](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly): a maven module that packages components together to form an [Anchor distribution](https://bitbucket.org/anchorimageanalysis/anchor/wiki/Anchor%20Distribution).

{% include links.html %}
