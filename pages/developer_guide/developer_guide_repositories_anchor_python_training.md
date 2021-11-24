---
title: "Source Repository - anchor-python-training"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_python_training.html
folder: developer_guide
---

## Introduction

A **Python** source repository on [GitHub](https://github.com/anchoranalysis/anchor-python-training/). It provides functions for training [Convolutional Neural Network (CNN)](https://en.wikipedia.org/wiki/Convolutional_neural_network) models from images.

### What belongs in the repository?

{% include tip.html content="It **should** include: Python scripts/functions/classes for training convolutional-neural-network (CNN) models from images." %}

{% include warning.html content="It should **not** include: Python scripts/functions/classes for inference, visualization or non-training purposes, or non-Python code." %}

## Documentation

[Documentation](https://www.anchoranalysis.org/anchor-python-training/) is automatically generated from *master* branch using Sphinx for public modules and classes.

## Code Structure

- Each entry-point script is found in the top-level directory.
- Each top-level directory contains a package, to be loaded using `from packagename import` style (see [Coding Style](/developer_guide_architecture_coding_style.html#python)).

### Entry-point scripts

| Package | Description  |
|------------|------------------|-------------:|-------------:|
| [train_autoencoder.py](https://github.com/anchoranalysis/anchor-python-training/blob/master/src/anchor_python_training/train_autoencoder.py) | Plots / exports a histogram from the CSVs produced by an Anchor export. |

{% include links.html %}
