---
title: "Source Repository - anchor"
tags: [architecture]
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor.html
folder: developer_guide
---

## Introduction

A Java (maven) source repository on [GitHub](https://github.com/anchoranalysis/anchor) containing the main libraries
used by Anchor.

### What belongs?

{% include tip.html content="It **should** include: frequently used utility classes, and key abstract base classes for plugins." %}

{% include warning.html content="It should **not** include: plugins, anything GUI-related, pipeline BeanXML, entry-point applications." %}




## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-annotation](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation) | `org.anchoranalysis.annotation`<br>Annotating images with shapes / labels. | 5 | 191 |
| [anchor-annotation-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation-io) | `org.anchoranalysis.annotation.io`<br>Reading / writing related to `anchor-annotation` | 28 | 1,299 |
| [anchor-bean](https://github.com/anchoranalysis/anchor/tree/master/anchor-bean) | `org.anchoranalysis.bean`<br>Dependency injection framework and object-model. | 97 | 3,239 |
| [anchor-beans-shared](https://github.com/anchoranalysis/anchor/tree/master/anchor-beans-shared) | `org.anchoranalysis.bean.shared`<br>Generic reusable utility beans. | 19 | 386 |
| [anchor-core](https://github.com/anchoranalysis/anchor/tree/master/anchor-core) | `org.anchoranalysis.core`<br>Fundamental core library objects. | 165 | 4,582 |
| [anchor-experiment](https://github.com/anchoranalysis/anchor/tree/master/anchor-experiment) | `org.anchoranalysis.experiment`<br>Defines an experiment and how to execute it. | 55 | 2,606 |
| [anchor-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature) | `org.anchoranalysis.feature`<br>Defines a *feature* generically and related utilities. | 75 | 2,969 |
| [anchor-feature-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature-io) | `org.anchoranalysis.feature.io`<br>Reading / writing related to `anchor-feature` | 6 | 382 |
| [anchor-feature-session](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature-session) | | 25 | 1,098 |
| [anchor-graph](https://github.com/anchoranalysis/anchor/tree/master/anchor-graph) | | 15 | 731 |
| [anchor-image](https://github.com/anchoranalysis/anchor/tree/master/anchor-image) | | 257 | 14,834 |
| [anchor-image-bean](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-bean) | | 63 | 1,950 |
| [anchor-image-experiment](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-experiment) | | 8 | 356 |
| [anchor-image-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-feature) | | 55 | 1,827 |
| [anchor-image-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-io) | | 74 | 3,691 |
| [anchor-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-io) | | 94 | 3,416 |
| [anchor-io-generator](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-generator) | | 43 | 1,789 |
| [anchor-io-manifest](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-manifest) | | 74 | 2,253 |
| [anchor-io-output](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-output) | | 20 | 936 |
| [anchor-math](https://github.com/anchoranalysis/anchor/tree/master/anchor-math) | | 14 | 668 |
| [anchor-mpp](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp) | | 159 | 7,018 |
| [anchor-mpp-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-feature) | | 59 | 2,778 |
| [anchor-mpp-graph](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-graph) | | 6 | 303 |
| [anchor-mpp-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-io) | | 43 | 2,368 |
| [anchor-mpp-sgmn](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-sgmn) | | 70 | 2,407 |
| [anchor-overlay](https://github.com/anchoranalysis/anchor/tree/master/anchor-overlay) | | 15 | 674 |
| [anchor-test](https://github.com/anchoranalysis/anchor/tree/master/anchor-test) | | 3 | 175 |
| [anchor-test-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-test-feature) | | 1 | 49 |

Number of classes/code is as per *SonarQube, Mar 31st, 2020*. Lines-of-code excludes whitespace and comments.

{% include links.html %}