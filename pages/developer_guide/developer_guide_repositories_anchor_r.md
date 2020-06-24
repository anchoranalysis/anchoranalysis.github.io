---
title: "Source Repository - anchor-r"
tags: [architecture]
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_r.html
folder: developer_guide
---

## Introduction

A **R** source repository on [GitHub](https://github.com/anchoranalysis/anchor-r). It provides scripts for processing the outputs of Anchor to build machine learning models, and otherwise process and visualize the data.

### What belongs in the repository?

{% include tip.html content="It **should** include: R scripts for processing data produced by Anchor, or data to form an input to Anchor." %}

{% include warning.html content="It should **not** include: non-R code." %}

## Packages

| Resource Location | Description  |
|------------|------------------|-------------:|-------------:|
| [anchor-r](https://github.com/anchoranalysis/anchor-r/tree/master/anchor-r) | Very general utility functions |
| [anchor-r-features](https://github.com/anchoranalysis/anchor-r/tree/master/anchor-r-features) | Processing feature-export data (CSV) from Anchor (building classifiers, plotting etc.) |
| [anchor-r-experiment](https://github.com/anchoranalysis/anchor-r/tree/master/anchor-r-experiment) | Utilities for accessing the structured output from an Anchor experiment |
| [anchor-r-nuclei](https://github.com/anchoranalysis/anchor-r/tree/master/anchor-r-experiment) | Functions to help with nuclei segmentation pipelines. |

{% include links.html %}
