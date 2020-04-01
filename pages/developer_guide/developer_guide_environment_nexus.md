---
title: "Dev Environment - Nexus repository server"
tags: [build]
keywords: github, environment, ci, continuousintegration
sidebar: developer_guide_sidebar
permalink: developer_guide_environment_nexus.html
folder: developer_guide
toc: true
---

## Overview

Anchor uses [Nexus Repository OSS](https://www.sonatype.com/nexus-repository-oss) as a Maven repository in several ways:

- It stores versioned-jars of Anchor - snapshots and releases.
- It provides several third-party dependencies that don't have corresponding public repositories.
- It mirrors and caches public repositories for quicker downloads of dependencies.
 
 When in use, it is found at:
> http://maven.anchoranalysis.org:8081/nexus/
 
 <img src="/images/developer_guide/nexus.png" alt="Screenshot of Nexus Repository Server for anchor" class="screenshotExample"/>

## Hosted Maven repositories

| Name | Purpose |
| ---- | ------- |
| `anchor-releases`| released JARs i.e. **without** `SNAPSHOT` in the version |
| `anchor-snapshots` | snapshot JARS i.e. **with** `SNAPSHOT` in the version |
| `anchor-thirdparty` | third-party dependency JARs manually uploaded, as elsewhere available | 
| `ImageJ` | proxy for public [ImageJ repository](http://maven.imagej.net/content/groups/public) |
| `maven-*` | proxies for general public repositories |
| `ome-*` | proxies for public [OME](https://www.openmicroscopy.org/) repositories |
| `unidata.releases` | proxy for [unidata.releases respository](https://artifacts.unidata.ucar.edu/#browse/browse:unidata-releases) |
| `anchor` | virtual repository combining all of the above |

### Credentials

See [Building Anchor](/developer_guide_building_anchor.html#mavenCredentials) to configure maven to access the repositories.

{% include links.html %}