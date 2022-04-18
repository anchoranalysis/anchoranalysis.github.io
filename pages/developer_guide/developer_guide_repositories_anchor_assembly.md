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

- command-line launchers for Anchor
- procedure for making an [Anchor Distribution](/developer_guide_anchor_distribution.html)
- all the [BeanXML](/user_guide_bean_xml.html) for default tasks and configuration

### What belongs in the repository?

{% include tip.html content="It **should** include: command-line programs for launching and configuring anchor launcher application (entry-point application), Maven directives to build an [Anchor Distribution](/developer_guide_anchor_distribution.html), any default configuration and tasks." %}

{% include warning.html content="It should **not** include: data objects, algorithms related to image processing." %}

### Supporting libraries and tooling

- A [SonarCloud project](https://sonarcloud.io/project/overview?id=anchoranalysis_anchor-assembly) performs static code analysis.

- [Project Lombok](https://projectlombok.org/) reduces boiler-plate source code. Please see [key libraries](/developer_guide_environment_key_libraries.html) for relevant libraries and tooling.

- [Coding style](http://localhost:4000/developer_guide_architecture_coding_style.html) specifies the applicable style-guide.

- [GitHub Actions](https://github.com/anchoranalysis/anchor-assembly/actions) and [Maven](https://maven.apache.org/) for [CI/CD](https://en.wikipedia.org/wiki/CI/CD).

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-launcher](https://github.com/anchoranalysis/anchor-assembly/tree/master/addplugins/anchor-launcher) | `org.anchoranalysis.launcher`<br>The **anchor** command-line application. | 38 | 1,627 |


Number of classes/code is as per *SonarQube, June 24th, 2020*. Lines-of-code excludes whitespace and comments.

## Resources

| Resource Location | Description  |
|------------|------------------|-------------:|-------------:|
| [config](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/config) | What becomes the `config/` directory in a distribution |
| [models](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/config) | What becomes the `models/` directory in a distribution |
| [helperapps](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/helperapps) | Files placed into the `bin/` directory to help start anchor correctly-configured |
| [topleveldocs](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/topleveldocs) | Documentation placed in the root directory (i.e. `/`) of a distribution |

## Key Maven configuration-files

| Resource Location | Description  |
|------------|------------------|-------------:|-------------:|
| [addplugins/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/addplugins/pom.xml) | Where non GPL-plugins are listed to be included. |
| [anchor-assembly/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/pom.xml) | Building `.exe` launchers, and GPL-plugins listed to be included. |
| [Distribution XML files](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/assembly/) | Specifies what files are contained in a distribution. |





{% include links.html %}
