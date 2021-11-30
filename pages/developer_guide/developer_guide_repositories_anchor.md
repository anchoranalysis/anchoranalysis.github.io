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

{% include warning.html content="It should **not** include: plugins, anything GUI-related, pipeline BeanXML, entry-point applications." %}




## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-annotation](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation) | `org.anchoranalysis.annotation`<br>Annotating images with shapes / labels. | 5 | 160 |
| [anchor-annotation-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation-io) | `org.anchoranalysis.annotation.io`<br>Reading / writing related to [anchor-annotation](https://github.com/anchoranalysis/anchor/tree/master/anchor-annotation) | 30 | 1,158 |
| [anchor-bean](https://github.com/anchoranalysis/anchor/tree/master/anchor-bean) | `org.anchoranalysis.bean`<br>Dependency injection framework and object-model. | 99 | 3,153 |
| [anchor-beans-shared](https://github.com/anchoranalysis/anchor/tree/master/anchor-beans-shared) | `org.anchoranalysis.bean.shared`<br>Generic reusable utility beans. | 30 | 645 |
| [anchor-core](https://github.com/anchoranalysis/anchor/tree/master/anchor-core) | `org.anchoranalysis.core`<br>Fundamental core library objects. | 166 | 4,181 |
| [anchor-experiment](https://github.com/anchoranalysis/anchor/tree/master/anchor-experiment) | `org.anchoranalysis.experiment`<br>Defines an experiment and how to execute it. | 63 | 2,300 |
| [anchor-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature) | `org.anchoranalysis.feature`<br>Defines a *feature* generically and related utilities. | 72 | 2,351 |
| [anchor-feature-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature-io) | `org.anchoranalysis.feature.io`<br>Reading / writing related to [anchor-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature) | 18 | 717 |
| [anchor-feature-session](https://github.com/anchoranalysis/anchor/tree/master/anchor-feature-session) | `org.anchoranalysis.feature.session`<br>Sessions to calculate many features optimally. | 35 | 1,479 |
| [anchor-inference](https://github.com/anchoranalysis/anchor/tree/master/anchor-inference) | `org.anchoranalysis.inference`<br>High-level classes for performing machine learning model inference. | 9 | 222 |
| [anchor-image-bean](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-bean) | `org.anchoranalysis.image.bean`<br>Core *(bean)* data objects for images. | 80 | 1,932 |
| [anchor-image-core](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-core) | `org.anchoranalysis.image.core`<br>Core *(non-bean)* data objects for images. | 117 | 5,508 |
| [anchor-image-experiment](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-experiment) | `org.anchoranalysis.image.experiment`<br>Base classes for general tasks that involve images. | 4 | 152 |
| [anchor-image-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-feature) | `org.anchoranalysis.image.feature`<br>Feature calculation on images or parts of images. | 48 | 1,445 |
| [anchor-image-inference](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-inference) | `org.anchoranalysis.image.inference`<br>Machine learning model inference on images. | 18 | 775 |
| [anchor-image-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-io) | `org.anchoranalysis.image.io`<br>Reading / writing related to [anchor-image](https://github.com/anchoranalysis/anchor/tree/master/anchor-image) | 86 | 3,716 |
| [anchor-image-voxel](https://github.com/anchoranalysis/anchor/tree/master/anchor-image-voxel) | `org.anchoranalysis.image.voxel`<br>Data objects for per-voxel manipulation of images. | 230 | 10,195 |
| [anchor-imagej](https://github.com/anchoranalysis/anchor/tree/master/anchor-imagej) | `org.anchoranalysis.io.ij`<br>Converters and IO that uses [ImageJ](https://imagej.net/Welcome). | 11 | 656 |
| [anchor-inference](https://github.com/anchoranalysis/anchor/tree/master/anchor-inference) | `org.anchoranalysis.inference`<br>Performing machine learning model inference. | 6 | 143 |
| [anchor-io-bioformats](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-bioformats) | `org.anchoranalysis.io.bioformats`<br>Input / output that uses [Bioformats](https://www.openmicroscopy.org/bio-formats/). | 37 | 1,510 |
| [anchor-io-generator](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-generator) | `org.anchoranalysis.io.generator`<br>*Generators* for producing output.  | 35 | 1,325 |
| [anchor-io-input](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-input) | `org.anchoranalysis.io.input`<br>Collecting inputs (not image specific) for tasks/experiments. | 46 | 1,372 |
| [anchor-io-manifest](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-manifest) | `org.anchoranalysis.io.manifest`<br>Manifests for recording outputs from an experiment. | 42 | 1,311 |
| [anchor-io-output](https://github.com/anchoranalysis/anchor/tree/master/anchor-io-output) | `org.anchoranalysis.io.output`<br>Output-manager and utilities for outputting. | 72 | 2,042 |
| [anchor-math](https://github.com/anchoranalysis/anchor/tree/master/anchor-math) | `org.anchoranalysis.math`<br>Mathematical algorithms or utility functions. | 11 | 855 |
| [anchor-mpp](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp) | `org.anchoranalysis.mpp`<br>Core data classes for Marked Point Processes | 133 | 5,431 |
| [anchor-mpp-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-feature) | `org.anchoranalysis.mpp.feature`<br>Feature calculation on objects in [anchor-mpp](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp) | 46 | 2,247 |
| [anchor-mpp-io](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-io) | `org.anchoranalysis.mpp.io`<br>Input / output related to objects in [anchor-mpp](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp) | 29 | 1,5152 |
| [anchor-mpp-segment](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp-segment) | `org.anchoranalysis.mpp.segment`<br>Segmentation involving objects in [anchor-mpp](https://github.com/anchoranalysis/anchor/tree/master/anchor-mpp) | 64 | 1,867 |
| [anchor-overlay](https://github.com/anchoranalysis/anchor/tree/master/anchor-overlay) | `org.anchoranalysis.anchor.overlay`<br>Graphics output of entities on top of a raster. | 17 | 710 |
| [anchor-plot](https://github.com/anchoranalysis/anchor/tree/master/anchor-plot) | `org.anchoranalysis.plot`<br>Plotting of some basic charts. | 14 | 605 |
| [anchor-spatial](https://github.com/anchoranalysis/anchor/tree/master/anchor-spatial) | `org.anchoranalysis.spatial`<br>Core geometry and spatial manipulation. | 27 | 1,178 |
| [anchor-test](https://github.com/anchoranalysis/anchor/tree/master/anchor-test) | `org.anchoranalysis.test`<br>Reusable test fixtures/utilities *(at highest generality)*. | 4 | 212 |
| [anchor-test-feature](https://github.com/anchoranalysis/anchor/tree/master/anchor-test-feature) | `org.anchoranalysis.test.feature`<br>Reusable test fixtures *related to features*. | 1 | 60 |
| [anchor-test-image](https://github.com/anchoranalysis/anchor/tree/master/anchor-test-image) | `org.anchoranalysis.test.image`<br>Reusable test fixtures *related to images*. | 34 | 1,697 |
| [anchor-test-io-output](https://github.com/anchoranalysis/anchor/tree/master/anchor-test-io-output) | `org.anchoranalysis.test.io-output`<br>Test fixtures *related to non-image outputs*. | 1 | 33 |

Number of classes/code is as per *SonarQube, October 18th, 2020*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
