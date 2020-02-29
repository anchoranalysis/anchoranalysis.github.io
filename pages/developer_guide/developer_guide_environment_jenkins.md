---
title: "Development Environment - Jenkins"
tags: [build]
keywords: sonarqube, environment, ci, continuousintegration
sidebar: developer_guide_sidebar
permalink: developer_guide_environment_jenkins.html
folder: developer_guide
toc: false
---

## Overview

Anchor uses [Jenkins](https://jenkins.io/) as a continuous integration tool. After code pushes to GitHub, it:

1. builds the latest development version and runs tests
2. compiles HTML API documentation (i.e. [Javadoc](https://en.wikipedia.org/wiki/Javadoc))
3. updates [SonarQube](/developer_guide_environment_sonarqube.html)

The projects follow the *dev* branch on the respositories in GitHub.

![jenkins](/images/developer_guide/jenkins.png)

{% include links.html %}