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

| Repository | Java package namespace root | Description | Modules | Functions | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------|-----------|-----------|---------------|
| [anchor](https://github.com/anchoranalysis/anchor) | `org.anchoranalysis.` | Main libraries | 28 | 8.7k | 1.6k | 66k |
| [anchor-plugins](https://github.com/anchoranalysis/anchor) | `org.anchoranalysis.plugin.` | Main plugins | 19 | 6.9k | 1.2k | 62k |
| [anchor-plugins-gpl](https://github.com/anchoranalysis/anchor-plugins-gpl)  | `org.anchoranalysis.plugin.gpl.` | GPL-licensed plugins | 3 | 0.2k | 0.03k | 3k |
| [anchor-gui](https://github.com/anchoranalysis/anchor-gui)  | `org.anchoranalysis.gui.` | GUI application | 14 | 3.7k | 0.8k | 38k |
| [anchor-assembly](https://github.com/anchoranalysis/anchor-assembly)  | `org.anchoranalysis.` | Launches anchor | 3 | 0.1k | 0.03k | 2k |

Number of classes/code is as per *SonarQube, Feb 14th, 2020*. Lines-of-code excludes whitespace and comments.

## Plugins 

### Steps for adding a new plugin module

Based in the root directory of a multi-module respository:

1. Create a sub-directory containing the new module in [anchor-plugins](https://github.com/anchoranalysis/anchor-plugins) or [anchor-plugins-gpl](https://github.com/anchoranalysis/anchor-plugins-gpl) depending on license.
2. Add module name to the `pom.xml` in the root directory of this repository.
3. Add a dependency in `anchor-assembly`:
    1. if it's the regular MIT license (i.e. not-GPL), then add a dependency in [/addplugins/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/addplugins/pom.xml) 
    2. if it's GPL, then add a dependency in [/anchor-assembly/pom.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/pom.xml)

{% include links.html %}
