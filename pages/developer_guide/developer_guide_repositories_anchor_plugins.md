---
title: "Source Repository - anchor-plugins"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_plugins.html
folder: developer_guide
---

## Introduction

A **Java** ([Maven](/developer_guide_environment_maven.html)) source repository on [GitHub](https://github.com/anchoranalysis/anchor-plugins) containing the main plugins for Anchor. This includes most of the image processing algorithms.

### What belongs?

{% include tip.html content="It **should** include: algorithms, beans, data-classes and any other implementations of abstract classes in the [anchor repository](/developer_guide_repositories_anchor.html), so long as they are compatible with the MIT license." %}

{% include warning.html content="It should **not** include: GPL-licensed code, anything GUI-related, pipeline BeanXML, entry-point applications." %}

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-plugin-annotation](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-annotation) | | 36 | 1,989 |
| [anchor-plugin-ij](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-ij) | | 33 | 1,987 |
| [anchor-plugin-image](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image) | | 312 | 13,785 |
| [anchor-plugin-image-feature](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image-feature) | | 183 | 6,590 |
| [anchor-plugin-image-task](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image-task) | | 55 | 3,273 |
| [anchor-plugin-io](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-io) | | 144 | 6,665 |
| [anchor-plugin-mpp](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp) | | 113 | 6,142 |
| [anchor-plugin-mpp-experiment](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp-experiment) | | 35 | 2,641 |
| [anchor-plugin-mpp-feature](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp-feature) | | 78 | 2,875 |
| [anchor-plugin-mpp-sgmn](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp-sgmn) | | 95 | 5,056 |
| [anchor-plugin-opencv](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-opencv) | | 24 | 1,309 |
| [anchor-plugin-operator-feature](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-operator-feature) | | 35 | 1,004 |
| [anchor-plugin-points](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-points) | | 33 | 2,036 |
| [anchor-plugin-quick](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-quick) | | 28 | 2,087 |
| [anchor-test-experiment](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-test-experiment) | | 4 | 317 |
| [anchor-test-feature-plugins](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-test-feature-plugins) | | 13 | 494 |
| [anchor-test-mpp](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-test-mpp) | | - | 68 |

Number of classes/code is as per *SonarQube, June 24th, 2020*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
