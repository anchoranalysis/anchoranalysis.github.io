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

{% include warning.html content="It should **not** include: GPL-licensed code, pipeline BeanXML, entry-point applications." %}

### Supporting libraries and tooling

- A [SonarCloud project](https://sonarcloud.io/project/overview?id=anchoranalysis_anchor_plugins) performs static code analysis.

- [Project Lombok](https://projectlombok.org/) reduces boiler-plate source code. Please see [key libraries](/developer_guide_environment_key_libraries.html) for relevant libraries and tooling.

- [Coding style](http://localhost:4000/developer_guide_architecture_coding_style.html) specifies the applicable style-guide.

- [GitHub Actions](https://github.com/anchoranalysis/anchor-plugins/actions) and [Maven](https://maven.apache.org/) for [CI/CD](https://en.wikipedia.org/wiki/CI/CD).

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-plugin-annotation](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-annotation) | `org.anchoranalysis.plugin.annotation`<br>Annotating images. | 36 | 1.4k |
| [anchor-plugin-image](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image) | `org.anchoranalysis.plugin.image`<br>Image-related options. | 318 | 11.6k |
| [anchor-plugin-imagej](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-imagej) | `org.anchoranalysis.plugin.imagej`<br>Operations that use [ImageJ](https://imagej.net/Welcome). | 24 | 1.6k |
| [anchor-plugin-image-feature](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image-feature) | `org.anchoranalysis.plugin.image.feature`<br>Feature-extraction from images. | 186 | 5.2k |
| [anchor-plugin-image-task](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-image-task) | `org.anchoranalysis.plugin.image.task`<br>Tasks related to images. | 96 | 5.7k |
| [anchor-plugin-io](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-io) | `org.anchoranalysis.plugin.io`<br>Input-output operations. | 189 | 7.4k |
| [anchor-plugin-mpp](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-mpp) | `org.anchoranalysis.plugin.mpp`<br>Operations related to [marked-point-processes](/user_guide_advanced_marked_point_processes.html). | 23 | 1.1k |
| [anchor-plugin-onnx](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-onnx) | `org.anchoranalysis.plugin.onnx`<br>Operations that call the [ONNX Runtime](https://onnxruntime.ai/). | 8 | 0.8k |
| [anchor-plugin-opencv](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-opencv) | `org.anchoranalysis.plugin.opencv`<br>Operations that call [OpenCV](https://opencv.org/). | 26 | 1.4k |
| [anchor-plugin-operator-feature](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-operator-feature) | `org.anchoranalysis.plugin.operator.feature`<br>Generic features working on varying input-types. | 34 | 0.8k |
| [anchor-plugin-points](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-plugin-points) | `org.anchoranalysis.plugin.points`<br>Points-fitting and other geometric operations. | 33 | 1.7k |
| [anchor-test-experiment](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-test-experiment) | `org.anchoranalysis.test.experiment`<br>Test utilities depending on [anchor-experiment](https://github.com/anchoranalysis/anchor/tree/master/anchor-experiment). | 4 | 0.5k |
| [anchor-test-feature-plugins](https://github.com/anchoranalysis/anchor-plugins/tree/master/anchor-test-feature-plugins) | `org.anchoranalysis.test.feature`<br>Helper routines for testing features. | 12 | 0.5k |

Number of classes/code is as per *SonarQube, October 19th, 2025*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
