---
title: "Development Environment - GitHub"
tags: [build]
keywords: github, environment, ci, continuousintegration
sidebar: developer_guide_sidebar
permalink: developer_guide_environment_github.html
folder: developer_guide
toc: true
---

## Overview

Anchor uses [GitHub](https://github.com/anchoranalysis) for several purposes:

- several repositories containing **all source-code needed to build Anchor**
- **storing Anchor Distributions** in packages
- **maintaining issues** and [project task-boards](https://github.com/orgs/anchoranalysis/projects)
- source code for **the Anchor website** at `http://www.anchoranalysis.org` in the [anchoranalysis.hithub.io repository](https://github.com/anchoranalysis/anchoranalysis.github.io)

![github](/images/developer_guide/github.png)

## Source code repositories

### Repositories and dependencies

Please see [Architecture - Overview](/developer_guide_architecture_overview.html) for dependencies and repository descriptions.

| Repository | Primary code language(s) |
| --- | --- |
| [anchor](https://github.com/anchoranalysis/anchor) | Java |
| [anchor-plugins](https://github.com/anchoranalysis/anchor-plugins) | Java |
| [anchor-plugins-gpl](https://github.com/anchoranalysis/anchor-plugins-gpl) | Java |
| [anchor-gui](https://github.com/anchoranalysis/anchor-gui) | Java |
| [anchor-assembly](https://github.com/anchoranalysis/anchor-assembly) | Java, BeanXML |
| [anchor-pom](https://github.com/anchoranalysis/anchor-pom) | Maven `pom.xml` |
| [anchoranalysis.github.io](https://github.com/anchoranalysis/anchoranalysis.github.io) | Markdown, HTML - via [Jekyll](https://jekyllrb.com/) |

### Branches

The projects typically have several branches:
- **master** - corresponding to the latest stable release
- **dev** - corresponding to common state of current development
- other branches for features or bug-fixes 

{% include links.html %}