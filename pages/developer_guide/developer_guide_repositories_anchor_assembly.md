---
title: "Source Repository - anchor-assembly"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_assembly.html
folder: developer_guide
---

## Introduction

A **Java** ([Maven](/developer_guide_environment_maven.html)) source repository on [GitHub](https://github.com/anchoranalysis/anchor-assembly). It provides:

- procedure for making an [Anchor Distribution](/developer_guide_anchor_distribution.html)
- all the [BeanXML](/user_guide_bean_xml.html) for default tasks and configuration
- references to specific versioned-plugins from [anchor-plugins-gpl](/developer_guide_repositories_anchor_plugins_gpl.html) that are included in the distribution

### What belongs in the repository?

{% include tip.html content="It **should** include: Maven directives to build an [Anchor Distribution](/developer_guide_anchor_distribution.html), any default configuration and tasks." %}

{% include warning.html content="It should **not** include: data objects, algorithms related to image processing, the launcher application." %}

### Supporting libraries and tooling

- [GitHub Actions](https://github.com/anchoranalysis/anchor-assembly/actions) and [Maven](https://maven.apache.org/) for [CI/CD](https://en.wikipedia.org/wiki/CI/CD).

## Resources

| Resource Location | Description  |
|------------|------------------|-------------:|-------------:|
| [config](https://github.com/anchoranalysis/anchor-assembly/tree/master/src/main/resources/config) | What becomes the `config/` directory in a distribution |
| [models](https://github.com/anchoranalysis/anchor-assembly/tree/master/src/main/resources/models) | What becomes the `models/` directory in a distribution |
| [helperapps](https://github.com/anchoranalysis/anchor-assembly/tree/master/src/main/resources/helperapps) | Files placed into the `bin/` directory to help start anchor correctly-configured |
| [topleveldocs](https://github.com/anchoranalysis/anchor-assembly/tree/master/src/main/resources/topleveldocs) | Documentation placed in the root directory (i.e. `/`) of a distribution |

## Key Maven configuration-files

| Resource Location | Description  |
|------------|------------------|-------------:|-------------:|
| [pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/pom.xml) | Building native-installers and launchers, and GPL-plugins listed to be included, and where non-GPL-plugins are listed to be included. |
| [Distribution XML files](https://github.com/anchoranalysis/anchor-assembly/tree/master/src/assembly) | Specifies what files are contained in a distribution. |





{% include links.html %}
