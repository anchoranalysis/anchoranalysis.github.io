---
title: "Anchor Image Analysis"
keywords: homepage anchor image analysis microscopy
tags:
sidebar:
permalink: index.html
hide_sidebar: true
toc: false
disable_editme: true
---

Anchor is a free command-line application and platform for image analysis, especially microscopy image analysis.

{% include callout.html type="danger" content="It's a Swiss-army-knife for loading, transforming, and extracting information from **sets of images**, as single-image tools are often limiting." %}

{% include tip.html content="[Download](/download.html) and [install](/installation.html). Then see [example usage](/user_guide_examples.html), the [user guide](/user_guide.html) and the [command line](/user_guide_command_line.html)." %}

## Features

<img src="/images/anchor_medium_logo.png" alt="Anchor logo" style="float:right;width:341px;height:163px;">

- Supports diverse image types and formats (photos, 2D / 3D / time-series microscopy).
- Smartly names outputs by finding patterns in filenames. Preserves directory structure.
- Reproducible pipelines defined via XML.
- Feature-extraction libraries (sets of voxels, geometric shapes) etc.
- Extensible via Java to call operations in [ImageJ](https://imagej.net/Welcome), [Icy](http://icy.bioimageanalysis.org/), [OpenCV](https://opencv.org/) etc.
- Cross-platform - Windows, Linux, Mac - with seemless switching between local and server.
- A basic pinboard-style GUI for images, segmentations and features.


{% include links.html %}

## Project Status {#projectStatus}

Anchor's source-code can be found on [GitHub](https://github.com/anchoranalysis). It is a significant project, covering 170,000 [lines-of-code](/developer_guide_repositories_overview.html#java) across 3,600 Java classes, as well as [BeanXML](/developer_guide_anchor_beans.html) analysis pipelines.

{% include callout.html type="danger" content="Effort is ongoing to create documentation and address technical debt for the first formal public release. Only a pre-alpha distribution can be [downloaded](/download.html) until then." %}

## Author

[Owen Feehan](http://www.owenfeehan.com) - developed since 2010 across employment in [ETH Zurich](https://ethz.ch/en.html), the [University of Zurich](https://www.uzh.ch/en.html) and [Hoffmann-La Roche](https://www.roche.com/). Licensed [open source](/download.html#licensing).
