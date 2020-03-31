---
title: "Architecture - Modules"
tags: [architecture]
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_architecture_modules.html
folder: developer_guide
---

## Modules

Anchor is primarily a Java project, spread across several repositories, each sub-divided into several modules, typically each producing a JAR.  Each module is sub-divided into package namespaces, with a naming chosen to reflect the module.

![anchorRepositories.png](/images/anchorRepositories.png)

## Module statistics by repository {#moduleStatistics}


Anchor's key Java repositories were introduced in [Architecture - Overview](developer_guide_architecture_overview.html), each containing many modules:

### All Java repositories

| Repository | Java Package Root and Description | Modules | Functions | Classes | Lines&#x2011;of&#x2011;Code |
|------------|-------------|-----------:|-----------:|---------------:|---------------:|
| [anchor](/developer_guide_architecture_modules.html#anchor) | `org.anchoranalysis`<br>Main libraries for Anchor platform | 28 | 8.7k | 1.6k | 66k |
| [anchor-plugins](https://github.com/anchoranalysis/anchor) | `org.anchoranalysis.plugin`<br>Main set of plugins - MIT-licensed | 19 | 6.9k | 1.2k | 62k |
| [anchor-plugins-gpl](https://github.com/anchoranalysis/anchor-plugins-gpl) | `org.anchoranalysis.plugin.gpl`<br>Additional set of GPL-licensed plugins | 3 | 0.2k | 0.03k | 3k |
| [anchor-gui](https://github.com/anchoranalysis/anchor-gui)  | `org.anchoranalysis.gui`<br>GUI application | 14 | 3.7k | 0.8k | 38k |
| [anchor-assembly](https://github.com/anchoranalysis/anchor-assembly)  | `org.anchoranalysis`<br>Launches anchor and default config | 3 | 0.1k | 0.03k | 2k |

Number of classes/code is as per *SonarQube, Feb 14th, 2020*. Lines-of-code excludes whitespace and comments.

### Repository: anchor {#anchor}

[anchor repository on GitHub](https://github.com/anchoranalysis/anchor)

| Repository | Java Package Root and Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-annotation](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation) | `org.anchoranalysis.annotation`<br>Annotating images with human-provided shapes / labels. | 5 | 191 |
| [anchor-annotation-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation-io) | `org.anchoranalysis.annotation.io`<br>Reading / writing related to `anchor-annotation` | 28 | 1,299 |
| [anchor-bean](https://github.com/anchoranalysis/anchor/tree/master/anchor-bean) | `org.anchoranalysis.bean`<br>Dependency injection framework and object-model. | 97 | 3,239 |
| [anchor-beans-shared](https://github.com/anchoranalysis/anchor/tree/master/anchor-beans-shared) | `org.anchoranalysis.bean.shared`<br>Generic reusable utility beans. | 19 | 386 |
| [anchor-core](https://github.com/anchoranalysis/anchor/tree/master/anchor-core) | `org.anchoranalysis.core`<br>Fundamental core library objects. | 165 | 4,582 |
| anchor-experiment | | 55 | 2,606 |
| anchor-feature | | 75 | 2,969 |
| anchor-feature-io | | 6 | 382 |
| anchor-feature-session | | 25 | 1,098 |
| anchor-graph | | 15 | 731 |
| anchor-image | | 257 | 14,834 |
| anchor-image-bean | | 63 | 1,950 |
| anchor-image-experiment | | 8 | 356 |
| anchor-image-feature | | 55 | 1,827 |
| anchor-image-io | | 74 | 3,691 |
| anchor-io | | 94 | 3,416 |
| anchor-io-generator | | 43 | 1,789 |
| anchor-io-manifest | | 74 | 2,253 |
| anchor-io-output | | 20 | 936 |
| anchor-math | | 14 | 668 |
| anchor-mpp | | 159 | 7,018 |
| anchor-mpp-feature | | 59 | 2,778 |
| anchor-mpp-graph | | 6 | 303 |
| anchor-mpp-io | | 43 | 2,368 |
| anchor-mpp-sgmn | | 70 | 2,407 |
| anchor-overlay | | 15 | 674 |
| anchor-test | | 3 | 175 |
| anchor-test-feature | | 1 | 49 |

Number of classes/code is as per *SonarQube, Mar 31st, 2020*. Lines-of-code excludes whitespace and comments.

## Plugins 

### Steps for adding a new plugin module

Based in the root directory of a multi-module respository:

1. Create a sub-directory containing the new module in [anchor-plugins](https://github.com/anchoranalysis/anchor-plugins) or [anchor-plugins-gpl](https://github.com/anchoranalysis/anchor-plugins-gpl) depending on license.
2. Add module name to the `pom.xml` in the root directory of this repository.
3. Add a dependency in `anchor-assembly`:
    1. if it's the regular MIT license (i.e. not-GPL), then add a dependency in [/addplugins/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/addplugins/pom.xml) 
    2. if it's GPL, then add a dependency in [/anchor-assembly/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/pom.xml)

{% include links.html %}
