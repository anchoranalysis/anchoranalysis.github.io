---
title: "Source Repository - anchor-r"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_r.html
folder: developer_guide
---

## Introduction

A [R](https://www.r-project.org/) source repository on [GitHub](https://github.com/anchoranalysis/anchor-r). It provides functions for processing the outputs of Anchor to build machine learning models, and otherwise process and visualize the data.

### What belongs in the repository?

{% include tip.html content="It **should** include: R functions for processing data produced by Anchor, or data to form an input to Anchor." %}

{% include warning.html content="It should **not** include: R scripts (only R functions in packages belong here!)" %}

## Packages

| Resource Location | Description  |
|------------|------------------|-------------:|-------------:|
| [anchor-r](https://github.com/anchoranalysis/anchor-r/tree/master/anchor-r) | Very general utility functions |
| [anchor-r-features](https://github.com/anchoranalysis/anchor-r/tree/master/anchor-r-features) | Processing feature-export data (CSV) from Anchor (building classifiers, plotting etc.) |
| [anchor-r-experiment](https://github.com/anchoranalysis/anchor-r/tree/master/anchor-r-experiment) | Utilities for accessing the structured output from an Anchor experiment |
| [anchor-r-nuclei](https://github.com/anchoranalysis/anchor-r/tree/master/anchor-r-experiment) | Functions to help with nuclei segmentation pipelines. |

### Code structure

- Each function is documented in its header (in the respective `R/` subdirectory)
- The `NAMESPACE` file specifies which functions are publicly-exposed
- R-package dependencies are listed in the `DESCRIPTION` file and in `NAMESPACE`

## Installation

{% include warning.html content="The packages are not on [CRAN](https://cran.r-project.org/) and thus cannot be imported through the usual R functions" %}

Before using these functions in a script elsewhere, a package must be installed locally, either:

- Use [RStudio](https://www.rstudio.com/), open each project, and select the *Build & Reload* button in the *Build* panel in the top-right, or
- Use the make script (``make.bat``/ ``make.sh``) in the packages's top-level folder (after first **adding your R executable to the system path**).

{% include links.html %}
