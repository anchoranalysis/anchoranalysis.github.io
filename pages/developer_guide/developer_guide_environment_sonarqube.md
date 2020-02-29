---
title: "Development Environment - SonarQube"
tags: [build]
keywords: sonarqube, environment, ci, continuousintegration
sidebar: developer_guide_sidebar
permalink: developer_guide_environment_sonarqube.html
folder: developer_guide
toc: false
---

## Overview

Anchor uses [SonarQube](https://www.sonarqube.org/) for static code analysis - to search for potential bugs or style errors. After code pushes to GitHub, [Jenkins](/developer_guide_environment_jenkins.html) automatically sends the updated code to SonarQube for each anchor Java repository.

![sonarqube](/images/developer_guide/sonarqube.jpg)

{% include links.html %}