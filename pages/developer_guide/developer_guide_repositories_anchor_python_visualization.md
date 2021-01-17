---
title: "Source Repository - anchor-python-visualization"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_python_visualization.html
folder: developer_guide
---

## Introduction

A **Python** source repository on [GitHub]((https://github.com/anchoranalysis/anchor-python-visualization). It provides functions for visualizing the outputs of Anchor in various ways.

### What belongs in the repository?

{% include tip.html content="It **should** include: Python scripts/packages for processing data produced by Anchor for visualization." %}

{% include warning.html content="It should **not** include: Python scripts/packages for other purposes, or non-Python code." %}

## API Documentation

[API documentation](https://github.com/anchoranalysis/anchor-python-visualization/) is automatically generated from *master* branch using Sphinx for public modules and classes.

## Code Structure

- Each entry-point script is found in the top-level directory.
- Each top-level directory contains a package, to be loaded using `from packagename import` style (see [Coding Style](/developer_guide_architecture_coding_style.html#python)).

### Entry-point scripts

| Package | Description  |
|------------|------------------|-------------:|-------------:|
| [histogram_plot.py](https://github.com/anchoranalysis/anchor-python-visualization/blob/master/histogram_plot.py) | Plots / exports a histogram from the CSVs produced by an Anchor export. |
| [visualize_features.py](https://github.com/anchoranalysis/anchor-python-visualization/blob/master/visualize_features.py) | Plots a lower-dimensionality visualization of features. |

### Packages

| Package | Description  |
|------------|------------------|-------------:|-------------:|
| [features/](https://github.com/anchoranalysis/anchor-python-visualization/tree/master/features) | Methods for loading features and determining labels. |
| [projection/](https://github.com/anchoranalysis/anchor-python-visualization/tree/master/projection) | Methods for projecting a feature space to lower dimensionality. |
| [visualize/](https://github.com/anchoranalysis/anchor-python-visualization/tree/master/visualize) | Different schemes for visualizing features or other types of data. |

{% include links.html %}
