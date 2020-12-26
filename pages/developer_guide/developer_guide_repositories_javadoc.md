---
title: "Source Repository - anchor"
tags:
keywords: architecture, packages, repositories, javadoc
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_javadoc.html
folder: developer_guide
---

## Introduction

A [Maven](/developer_guide_environment_maven.html) `pom.xml` source repository on [GitHub](https://github.com/anchoranalysis/javadoc) to generate *aggregated* [Javadoc](https://en.wikipedia.org/wiki/Javadoc)
code documentation across many projects and repositories.

### What belongs?

{% include tip.html content="It **should** include: maven `pom.xml` for generating javadoc, and submodule references to repositories to be included." %}

{% include warning.html content="It should **not** include: java code." %}

## Structure

Each top-level directory refers to a Maven project for  different combinations of projects. 

On a change to the master branch, [GitHub Actions](/developer_guide_environment_github.html) will execute the `anchor-all-except-gui` project and upload it to the `gh-pages` branch of the repository. This feeds automatically into
the Anchor [website](http://www.anchoranalysis.org/javadoc/).

## Updating to latest commits

The documentation is always generated from the *master* branch of the respective repositories (via references to specific commits via [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)). To update the documentation to refer to the latest commits:

```
git submodule update --recursive --remote
```

## Manually-triggered creation of aggregated javadoc.

Execute in a project top-level directory: e.g. in `anchor-all-except-gui/`

```
mvn site javadoc:aggregate
```

and the Javadoc will be generated in `target/site/apidocs`.

{% include links.html %}
