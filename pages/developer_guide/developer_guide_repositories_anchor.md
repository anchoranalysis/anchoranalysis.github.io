---
title: "Source Repository - anchor"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor.html
folder: developer_guide
---

## Introduction

A **Java** ([Maven](/developer_guide_environment_maven.html)) source repository on [GitHub](https://github.com/anchoranalysis/anchor) containing the main libraries
used by Anchor.

### What belongs?

{% include tip.html content="It **should** include: frequently used utility classes, and key abstract base classes for plugins." %}

{% include warning.html content="It should **not** include: plugins, pipeline BeanXML, entry-point applications." %}

### Supporting libraries and tooling

- A [SonarCloud project](https://sonarcloud.io/project/overview?id=anchoranalysis_anchor) performs static code analysis.

- [Project Lombok](https://projectlombok.org/) reduces boiler-plate source code. Please see [key libraries](/developer_guide_environment_key_libraries.html) for relevant libraries and tooling.

- [Coding style](http://localhost:4000/developer_guide_architecture_coding_style.html) specifies the applicable style-guide.

- [GitHub Actions](https://github.com/anchoranalysis/anchor/actions) and [Maven](https://maven.apache.org/) for [CI/CD](https://en.wikipedia.org/wiki/CI/CD).

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-annotation](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation) | `org.anchoranalysis.annotation`<br>Annotating images with shapes / labels. | 5 | 0.1k |
| [anchor-annotation-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation-io) | `org.anchoranalysis.annotation.io`<br>Reading / writing related to [anchor-annotation](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation) | 29 | 1.2k |
| [anchor-bean](https://github.com/anchoranalysis/anchor/tree/master/anchor-bean) | `org.anchoranalysis.bean`<br>Dependency injection framework and object-model. | 99 | 3.2k |
| [anchor-beans-shared](https://github.com/anchoranalysis/anchor/tree/master/anchor-beans-shared) | `org.anchoranalysis.bean.shared`<br>Generic reusable utility beans. | 32 | 0.7k |
| [anchor-core](https://github.com/anchoranalysis/anchor/tree/master/anchor-core) | `org.anchoranalysis.core`<br>Fundamental core library objects. | 134 | 3.8k |
| [anchor-experiment](https://github.com/anchoranalysis/anchor/tree/master/anchor-experiment) | `org.anchoranalysis.experiment`<br>Defines an experiment and how to execute it. | 73 | 2.8k |
| [anchor-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature) | `org.anchoranalysis.feature`<br>Defines a *feature* generically and related utilities. | 77 | 2.3k |
| [anchor-feature-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature-io) | `org.anchoranalysis.feature.io`<br>Reading / writing related to [anchor-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature) | 28 | 1k |
| [anchor-feature-session](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature-session) | `org.anchoranalysis.feature.session`<br>Sessions to calculate many features optimally. | 26 | 1.3k |
| [anchor-image-bean](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-bean) | `org.anchoranalysis.image.bean`<br>Core *(bean)* data objects for images. | 97 | 3k |
| [anchor-image-core](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-core) | `org.anchoranalysis.image.core`<br>Core *(non-bean)* data objects for images. | 87 | 4.5k |
| [anchor-image-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-feature) | `org.anchoranalysis.image.feature`<br>Feature calculation on images or parts of images. | 49 | 1.5k |
| [anchor-image-inference](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-inference) | `org.anchoranalysis.image.inference`<br>Machine learning model inference on images. | 28 | 1.3k |
| [anchor-image-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-io) | `org.anchoranalysis.image.io`<br>Reading / writing related to [anchor-image](https://github.com/anchoranalysis/anchor/tree/master/anchor-image) | 84 | 3.3k |
| [anchor-image-voxel](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-voxel) | `org.anchoranalysis.image.voxel`<br>Data objects for per-voxel manipulation of images. | 239 | 9.7k |
| [anchor-imagej](https://github.com/anchoranalysis/anchor/tree/master/anchor-imagej) | `org.anchoranalysis.io.ij`<br>Converters and IO that uses [ImageJ](https://imagej.net/Welcome). | 13 | 0.7k |
| [anchor-inference](https://github.com/anchoranalysis/anchor/tree/master/anchor-inference) | `org.anchoranalysis.inference`<br>Performing machine learning model inference. | 9 | 0.2k |
| [anchor-io-bioformats](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-bioformats) | `org.anchoranalysis.io.bioformats`<br>Input / output that uses [Bioformats](https://www.openmicroscopy.org/bio-formats/). | 59 | 2.8k |
| [anchor-io-generator](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-generator) | `org.anchoranalysis.io.generator`<br>*Generators* for producing output.  | 33 | 1.9k |
| [anchor-io-input](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-input) | `org.anchoranalysis.io.input`<br>Collecting inputs (not image specific) for tasks/experiments. | 59 | 1.9k |
| [anchor-io-output](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-output) | `org.anchoranalysis.io.output`<br>Output-manager and utilities for outputting. | 80 | 2.4k |
| [anchor-math](https://github.com/anchoranalysis/anchor/tree/master/anchor-math) | `org.anchoranalysis.math`<br>Mathematical algorithms or utility functions. | 30 | 1.1k |
| [anchor-mpp](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp) | `org.anchoranalysis.mpp`<br>Core data classes for Marked Point Processes | 112 | 4.4k |
| [anchor-mpp-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-feature) | `org.anchoranalysis.mpp.feature`<br>Feature calculation on objects in [anchor-mpp](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp) | 40 | 1.9k |
| [anchor-mpp-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-io) | `org.anchoranalysis.mpp.io`<br>Input / output related to objects in [anchor-mpp](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp) | 12 | 0.6k |
| [anchor-overlay](https://github.com/anchoranalysis/anchor/tree/master/anchor-overlay) | `org.anchoranalysis.anchor.overlay`<br>Graphics output of entities on top of a raster. | 9 | 0.3k |
| [anchor-spatial](https://github.com/anchoranalysis/anchor/tree/master/anchor-spatial) | `org.anchoranalysis.spatial`<br>Core geometry and spatial manipulation. | 55 | 2.8k |
| [anchor-test](https://github.com/anchoranalysis/anchor/tree/master/anchor-test) | `org.anchoranalysis.test`<br>Reusable test fixtures/utilities *(at highest generality)*. | 6 | 0.2k |
| [anchor-test-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-test-feature) | `org.anchoranalysis.test.feature`<br>Reusable test fixtures *related to features*. | 1 | 0.05k |
| [anchor-test-image](https://github.com/anchoranalysis/anchor/tree/master/anchor-test-image) | `org.anchoranalysis.test.image`<br>Reusable test fixtures *related to images*. | 44 | 2k |
| [anchor-test-io-output](https://github.com/anchoranalysis/anchor/tree/master/anchor-test-io-output) | `org.anchoranalysis.test.io-output`<br>Test fixtures *related to non-image outputs*. | 3 | 0.1k |

Number of classes/code is as per *SonarQube, October 19th, 2025*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
