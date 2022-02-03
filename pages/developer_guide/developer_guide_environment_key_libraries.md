---
title: "Development Environment - Key Libraries"
tags: [build]
keywords: environment, lombok
sidebar: developer_guide_sidebar
permalink: developer_guide_environment_key_libraries.html
folder: developer_guide
toc: false
---

## Maven plugins

Anchor uses several key libaries via [Maven](/developer_guide_environment_maven.html) plugins:

* [Project Lombok](https://projectlombok.org/) to reduce boilerplate code and duplication of code. Note its [key features](https://projectlombok.org/features/all).

* [spotless](https://github.com/diffplug/spotless/tree/master/plugin-maven) to automatically restyle
Java code to match the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).

## Java libraries

* [Apache Commons](https://en.wikipedia.org/wiki/Apache_Commons) for utility functions and classes.

* [Guava](https://en.wikipedia.org/wiki/Google_Guava) for additional data structures and algorithms.

* [ONNX Runtime](https://onnxruntime.ai/) for inference of deep learning models.

* [OpenCV](https://opencv.org/) (specifically the [OpenPNP distribution for Java](https://github.com/openpnp/opencv)) for image processing and I/O.

* [Bioformats](https://www.openmicroscopy.org/bio-formats/) for image I/O.

* [ImageJ](https://imagej.net/) for image processing functions.

* [VavR](https://www.vavr.io/) for additional functional programming constructs.

* [JUnit 5](https://junit.org/junit5/) and [Mockito](https://site.mockito.org/) for testing.

## Python libraries

* [Pandas](https://pandas.pydata.org/)

* [NumPy](https://numpy.org/)

* [scikit-learn](https://scikit-learn.org/stable/) for classical [Machine Learning](https://en.wikipedia.org/wiki/Machine_learning) algorithms.

* [PyTorch](https://pytorch.org/) and [PyTorch Lightning](https://pytorch-lightning.readthedocs.io/en/latest/) for scripts to train [CNN](https://en.wikipedia.org/wiki/Convolutional_neural_network) models.

* [TensorFlow](https://www.tensorflow.org/) for exporting to [TensorBoard](https://www.tensorflow.org/tensorboard).

* [Plotly](https://plotly.com/) for data visualization.

{% include links.html %}