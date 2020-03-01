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

## Description

Anchor is a command-line application and platform for image analysis, especially microscopy image analysis.

{% include tip.html content="It's a Swiss-army-knife for loading, transforming, and extracting information from **sets of images**, as single-image tools are often limiting." %}

## Features
- Loading diverse image types (photos, 2D, 3D, time-series) across diverse formats, including microscopy formats via [Bio-formats](https://www.openmicroscopy.org/bio-formats/).
- Reads and writes smartly by finding patterns in image filenames and paths.
- Reproducible and extensible pipelines defined via XML for image processing - using various image processing plugins.
- Features to extract information from images and sub-regions of images (sets of voxels, geometric shapes) etc.
- Extensible via Java to call operations in [ImageJ](https://imagej.net/Welcome), [Icy](http://icy.bioimageanalysis.org/), [OpenCV](https://opencv.org/) etc.
- Cross-platform: Windows, Linux, Mac. - seemless switching between development environment and server
- A basic pinboard-style GUI for loading multiple images and processing results.


{% include links.html %}

## Project Status {#projectStatus}

Anchor's source-code can be found on [GitHub](https://github.com/anchoranalysis). It is a significant project, covering 170,000 [lines-of-code](/developer_guide_architecture_modules.html#moduleStatistics) across 3,600 Java classes, as well as [BeanXML](/developer_guide_anchor_beans.html) analysis pipelines.

{% include callout.html type="danger" content="An effort is ongoing to create documentation and address technical debt before the first formal public release. Only a pre-alpha distribution can be [downloaded](/download.html) until then." %}

## Author

[Owen Feehan](http://www.owenfeehan.com) - developed since 2010 across employment in [ETH Zurich](https://ethz.ch/en.html), the [University of Zurich](https://www.uzh.ch/en.html) and [Hoffmann-La Roche](https://www.roche.com/). Licensed [open source](/download.html#licensing).
