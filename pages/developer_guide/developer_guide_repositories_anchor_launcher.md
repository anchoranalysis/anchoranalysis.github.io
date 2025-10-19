---
title: "Source Repository - anchor-launcher"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_launcher.html
folder: developer_guide
---

## Introduction

A **Java** ([Maven](/developer_guide_environment_maven.html)) source repository on [GitHub](https://github.com/anchoranalysis/anchor-assembly). It provides:

- command-line launchers for Anchor
- references to specific versioned-plugins from [anchor-plugins](/developer_guide_repositories_anchor_plugins.html) that the launcher is designed to work with

### What belongs in the repository?

{% include tip.html content="It **should** include: command-line programs for launching and configuring anchor launcher application (entry-point application)." %}

{% include warning.html content="It should **not** include: data objects, algorithms related to image processing." %}

### Supporting libraries and tooling

- A [SonarCloud project](https://sonarcloud.io/project/overview?id=anchoranalysis_anchor-launcher) performs static code analysis.

- [Project Lombok](https://projectlombok.org/) reduces boiler-plate source code. Please see [key libraries](/developer_guide_environment_key_libraries.html) for relevant libraries and tooling.

- [Coding style](http://localhost:4000/developer_guide_architecture_coding_style.html) specifies the applicable style-guide.

- [GitHub Actions](https://github.com/anchoranalysis/anchor-launcher/actions) and [Maven](https://maven.apache.org/) for [CI/CD](https://en.wikipedia.org/wiki/CI/CD).

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-launcher](https://github.com/anchoranalysis/anchor-launcher/tree/master/anchor-launcher) | `org.anchoranalysis.launcher`<br>The **anchor** command-line application. | 52 | 2,680 |

Number of classes/code is as per *SonarQube, October 19th, 2025*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
