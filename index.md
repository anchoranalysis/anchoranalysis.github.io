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

Anchor is an open-source command-line application and platform for image analysis, especially microscopy image analysis.

{% include callout.html type="primary" content="It's a Swiss-army-knife for loading, transforming, and extracting information from **sets of images**, as tools that work only on single-images are often limiting." %}

## Features
- Loading diverse image types (photos, 2D, 3D, time-series) across diverse formats, including microscopy formats via [Bio-formats](https://www.openmicroscopy.org/bio-formats/).
- Reproducible and extensible pipelines defined via XML for image processing.
- Plugins covering classical image-processing operations.
- Features to extract information from images and sub-regions of images (sets of voxels, geometric shapes) etc.
- Extensible via Java to call operations in [ImageJ](https://imagej.net/Welcome), [Icy](http://icy.bioimageanalysis.org/) etc.
- Seamless switching between development environment (local PC or laptop, single-image, debugging) to server environment (many images in parallel).
- Cross-platform: Windows, Linux, Mac.
- A basic pinboard-style GUI for loading multiple images and processing results.

{% include links.html %}

## Author

[Owen Feehan](http://www.owenfeehan.com) - initially developed during employment in [ETH Zurich](https://ethz.ch/en.html), the [University of Zurich](https://www.uzh.ch/en.html) and [Hoffmann-La Roche](https://www.roche.com/). Licensed open-source.
