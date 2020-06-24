---
title: "Source Repository - anchor-pom"
tags: [architecture]
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_pom.html
folder: developer_guide
---

## Introduction

A **Maven** repository on [GitHub](https://github.com/anchoranalysis/anchor-pom) containing a [Maven](/developer_guide_environment_maven.html) `pom.xml` which provides a parent POM for other Java repositories.

Its purpose is to provide shared variables and configuration across all the anchor Java repositories.

### What belongs in the repository?

{% include tip.html content="Maven `pom.xml` containing shared variables and configuration." %}

{% include warning.html content="It should **not** include any Java code." %}

{% include links.html %}
