---
title: "Source Repository - anchor-plugins"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_plugins.html
folder: developer_guide
---

## Introduction

A **Java** ([Maven](/developer_guide_environment_maven.html)) source repository on [GitHub](https://github.com/anchoranalysis/anchor-plugins) containing the main plugins for Anchor. This includes most of the image processing algorithms.

### What belongs?

{% include tip.html content="It **should** include: algorithms, beans, data-classes and any other implementations of abstract classes in the [anchor repository](/developer_guide_repositories_anchor.html), so long as they are compatible with the MIT license." %}

{% include warning.html content="It should **not** include: GPL-licensed code, anything GUI-related, pipeline BeanXML, entry-point applications." %}

### Supporting libraries and tooling

- A [SonarCloud project](https://sonarcloud.io/project/overview?id=anchoranalysis_anchor_plugins) performs static code analysis.

- [Project Lombok](https://projectlombok.org/) reduces boiler-plate source code. Please see [key libraries](/developer_guide_environment_key_libraries.html) for relevant libraries and tooling.

- [Coding style](http://localhost:4000/developer_guide_architecture_coding_style.html) specifies the applicable style-guide.

- [GitHub Actions](https://github.com/anchoranalysis/anchor-plugins/actions) and [Maven](https://maven.apache.org/) for [CI/CD](https://en.wikipedia.org/wiki/CI/CD).

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-plugin-annotation](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-annotation) | `org.anchoranalysis.plugin.annotation`<br>Annotating images. | 36 | 1,989 |
| [anchor-plugin-image](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image) | `org.anchoranalysis.plugin.image`<br>Image-related options. | 312 | 13,785 |
| [anchor-plugin-imagej](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-imagej) | `org.anchoranalysis.plugin.imagej`<br>Operations that use [ImageJ](https://imagej.net/Welcome). | 33 | 1,987 |
| [anchor-plugin-image-feature](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image-feature) | `org.anchoranalysis.plugin.image.feature`<br>Feature-extraction from images. | 183 | 6,590 |
| [anchor-plugin-image-task](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image-task) | `org.anchoranalysis.plugin.image.task`<br>Tasks related to images. | 55 | 3,273 |
| [anchor-plugin-io](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-io) | `org.anchoranalysis.plugin.io`<br>Input-output operations. | 144 | 6,665 |
| [anchor-plugin-mpp](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp) | `org.anchoranalysis.plugin.mpp`<br>Operations related to [marked-point-processes](/user_guide_advanced_marked_point_processes.html). | 113 | 6,142 |
| [anchor-plugin-mpp-experiment](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp-experiment) | `org.anchoranalysis.plugin.mpp.experiment`<br>Experiments related to [marked-point-processes](/user_guide_advanced_marked_point_processes.html). | 35 | 2,641 |
| [anchor-plugin-mpp-feature](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp-feature) | `org.anchoranalysis.plugin.mpp.feature`<br>Feature-extraction with [marked-point-processes](/user_guide_advanced_marked_point_processes.html). | 78 | 2,875 |
| [anchor-plugin-mpp-segment](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp-segment) | `org.anchoranalysis.plugin.mpp.segment`<br>Segmentation involving [marked-point-processes](/user_guide_advanced_marked_point_processes.html). | 95 | 5,056 |
| [anchor-plugin-onnx](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-onnx) | `org.anchoranalysis.plugin.onnx`<br>Operations that call the [ONNX Runtime](https://onnxruntime.ai/). | 5 | 652 |
| [anchor-plugin-opencv](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-opencv) | `org.anchoranalysis.plugin.opencv`<br>Operations that call [OpenCV](https://opencv.org/). | 24 | 1,309 |
| [anchor-plugin-operator-feature](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-operator-feature) | `org.anchoranalysis.plugin.operator.feature`<br>Generic features working on varying input-types. | 35 | 1,004 |
| [anchor-plugin-points](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-points) | `org.anchoranalysis.plugin.points`<br>Points-fitting and other geometric operations. | 33 | 2,036 |
| [anchor-plugin-quick](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-quick) | `org.anchoranalysis.plugin.quick`<br>Quickly specifying experiments. | 28 | 2,087 |
| [anchor-test-experiment](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-test-experiment) | `org.anchoranalysis.test.experiment`<br>Test utilities depending on [anchor-experiment](https://github.com/anchoranalysis/anchor/tree/master/anchor-experiment). | 4 | 317 |
| [anchor-test-feature-plugins](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-test-feature-plugins) | `org.anchoranalysis.test.feature`<br>Helper routines for testing features. | 13 | 494 |
| [anchor-test-mpp](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-test-mpp) | `org.anchoranalysis.`<br>Tests for other packages involving image IO. | - | 68 |

Number of classes/code is as per *SonarQube, June 24th, 2020*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
