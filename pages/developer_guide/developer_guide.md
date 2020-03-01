---
title: "Developer Guide - Getting started"
tags: [getting_started]
keywords: systems, nexus, jenkins, sonarqube, aws, github
sidebar: developer_guide_sidebar
permalink: developer_guide.html
folder: developer_guide
---

## Key systems

* [GitHub](/developer_guide_environment_github.html) - hosts all source code, the website, and issues and projects.
* *Amazon AWS* - provides a build server ```build.anchoranalysis.org``` (on demand - suspended when not in use).

Services running on the build-server include:

* [Nexus Repository Server](/developer_guide_environment_nexus.html) - to publish and retrieve **snapshot** JARs during building.
* [Jenkins](/developer_guide_environment_jenkins.html) - continuous integration server - running tests and other tasks when we commit changed source code, such as generting javadocs.
* [SonarQube](/developer_guide_environment_sonarqube.html) - static code analyzer to find possible poor coding practices in the Java source.

## Key documents

* [Building Anchor](/developer_guide_building_anchor.html) - how to compile source-code into a working Anchor Distribution.
* [Anchor Distribution](/developer_guide_anchor_distribution.html) - the set of files a user receives to run Anchor.
* [Anchor Beans](/developer_guide_anchor_beans.html) - what anchor-beans are and how to encode them in XML.
* [Architecture Overview](/developer_guide_architecture_overview.html) - how the different repositories and JARs relate to each other.

{% include links.html %}
