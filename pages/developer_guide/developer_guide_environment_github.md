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

- several code repositories containing **all source-code needed to build Anchor**
- **storing** [distributions of Anchor](/developer_guide_anchor_distribution.html) in packages
- **continuous integration** via [GitHub Actions](https://github.com/actions), as seen in the ```.github/workflows``` subdirectory in repositories.
- **package repository** via [GitHub Packages](https://github.com/features/packages) to store [all JARs and released distributions]((https://github.com/orgs/anchoranalysis/packages)).
- **maintaining issues** and [project task-boards](https://github.com/orgs/anchoranalysis/projects/1)
- source code for the Anchor website at `http://www.anchoranalysis.org` in the [anchoranalysis.hithub.io repository](https://github.com/anchoranalysis/anchoranalysis.github.io)

<img src="/images/developer_guide/github.png" alt="Screenshot of Anchor project on GitHub" class="screenshotExample"/>

## Source code repositories

{% include tip.html content="Please see [Source Repositories](/developer_guide_repositories_overview.html) for descriptions and inter-dependencies." %}


### Branches

The projects typically have several branches:
- **master** - corresponding to the latest stable release
- **dev** - corresponding to common state of current development
- other branches for features or bug-fixes

{% include links.html %}