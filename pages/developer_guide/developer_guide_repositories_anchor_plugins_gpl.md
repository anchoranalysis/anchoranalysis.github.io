---
title: "Source Repository - anchor-plugins-gpl"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_plugins_gpl.html
folder: developer_guide
---

## Introduction

A **Java** ([Maven](/developer_guide_environment_maven.html)) source repository on [GitHub](https://github.com/anchoranalysis/anchor-plugins-gpl) containing plugins for Anchor that are licensed under the [GPL license](https://opensource.org/licenses/gpl-license) (rather than the [MIT license](https://opensource.org/licenses/MIT) used by the [primary plugin repository](https://github.com/anchoranalysis/anchor-plugins)).

### What belongs?

{% include tip.html content="It **should** include: algorithms, beans, data-classes and any other implementations of abstract classes in the [anchor repository](/developer_guide_repositories_anchor.html), if they **must** be licensed under the [GPL license](https://opensource.org/licenses/gpl-license)." %}

{% include warning.html content="It should **not** include: code that can be licensed more permissively under the [MIT license](https://opensource.org/licenses/MIT), anything GUI-related, pipeline BeanXML, entry-point applications." %}

### Supporting libraries and tooling

- A [SonarCloud project](https://sonarcloud.io/project/overview?id=anchoranalysis_anchor_plugins-gpl) performs static code analysis.

- [Project Lombok](https://projectlombok.org/) reduces boiler-plate source code. Please see [key libraries](/developer_guide_environment_key_libraries.html) for relevant libraries and tooling.

- [Coding style](http://localhost:4000/developer_guide_architecture_coding_style.html) specifies the applicable style-guide.

- [GitHub Actions](https://github.com/anchoranalysis/anchor-plugins-gpl/actions) and [Maven](https://maven.apache.org/) for [CI/CD](https://en.wikipedia.org/wiki/CI/CD).

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-plugin-fiji](https://github.com/anchoranalysis/anchor-plugins-gpl/tree/master/anchor-plugin-fiji) | `org.anchoranalysis.plugin.fiji`<br>GPL-ed plugins from [Fiji](https://fiji.sc/) or [ImageJ](https://imagej.nih.gov/ij/). | 18 | 1,247 |
| [anchor-plugin-io-gpl](https://github.com/anchoranalysis/anchor-plugins-gpl/tree/master/anchor-plugin-io-gpl) | Adds [Bio-Formats](https://www.openmicroscopy.org/bio-formats/) GPL classes. | - | 58 |
| [anchor-plugin-ml](https://github.com/anchoranalysis/anchor-plugins-gpl/tree/master/anchor-plugin-ml) | `org.anchoranalysis.plugin.ml`<br>Machine-learning operations that are GPLed. | 7 | 657 |

Number of classes/code is as per *SonarQube, June 24th, 2020*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
