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
- Cross-platform - Windows, Linux, Mac.
- Deep Learning inference with the [ONNX Runtime](https://onnxruntime.ai/).


## Project Status {#projectStatus}

Anchor's source-code can be found on [GitHub](https://github.com/anchoranalysis). Please report any bug / feature request as an [issue](https://github.com/anchoranalysis/anchor/issues).

Effort is ongoing to document and address technical debt for the first formal public release (over 120,000 lines of code!). Only a pre-release can be [downloaded](/download.html) until then.


## Quick Start - Example Commands

Start a task, by opening a shell in a directory of images and typing `anchor -t <someTask>`.

By default, it will search recursively for all images in this directory (with [standard extensions](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/defaultInputExtensions.xml)).


| Command | What it does? |
|------------|------------------|
| `anchor -h` | shows all available [command-line options](/user_guide_command_line.html) |
| `anchor -t` or `anchor -st` | shows all available [predefined tasks](/user_guide_predefined_tasks.html). |
|||
| `anchor -t summarize` | [summarizes](/user_guide_examples_investigating_images.html#searching-by-default) images into bullet points (extension, file naming patterns, size etc.). |
| `anchor -t summarize -i d:\foo\` | [summarizes](/user_guide_examples_investigating_images.html#searching-by-default) images recursively in a particular directory. |
| `anchor -t summarize -i "*.tif"`| [summarizes](/user_guide_examples_investigating_images.html#searching-by-default) only images that match a filter (the quotes are advised!) |
| `anchor -t list`| [lists](/user_guide_examples_investigating_images.html#searching-by-default) the paths and unique-identifier for each input. |
|||
| `anchor -t feature/metadata` | [creates a CSV](/user_guide_examples_extracting_image_features.html) with images as rows, and **image metadata** as columns. |
| `anchor -t feature/intensity` | [creates a CSV](/user_guide_examples_extracting_image_features.html) with images as rows, and **intensity statistics** as columns. |
| `anchor -t feature/hog` | [creates a CSV](/user_guide_examples_extracting_image_features.html) with images as rows, and a [HOG descriptor](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients) as columns. |
|||
| `anchor -t convert -ir -of png` | [converts](/user_guide_examples_converting_copying_images.html#converting-images-to-a-different-file-format) all images to *PNG* format (or pick [another extension](/user_guide_examples_changing_output_options.html#specifying-an-alternative-image-format)!) |
| `anchor -t convert -ir -of png -ic -o -oo d:\foo` | [converts](/user_guide_examples_converting_copying_images.html#preserving-relative-file-paths-and-any-non-image-files) like above to a particular directory, and copies non-image files (e.g. metadata!) |
| `anchor -t copy -ir -o -oo d:\foo` | [copies](/user_guide_examples_converting_copying_images.html#copying-files) all images to a particular new directory. |
| `anchor -t copy -is -on` | randomizes the order of images and anonymizes the filename. |
| `anchor -t cluster/timestamp` | creates clusters of images that are adjacent in time (from [EXIF](https://en.wikipedia.org/wiki/Exif), file attributes or naming) |
|||
| `anchor -t resize -ps 0.1`| [resizes](/user_guide_examples_resizing_images.html) each image to have a <i>tenth</i> of the width and height (try `2` to double). |
| `anchor -t resize -ps 1024x768`| [resizes](/user_guide_examples_resizing_images.html) each image to have 1024x768 size in pixels. |
| `anchor -t resize -ps 1024x768 -on`| [resizes](/user_guide_examples_resizing_images.html) like above, but outputs as an incrementing sequence (useful for creating [videos](/user_guide_examples_video_from_images.html)!) |
| `anchor -t resize -ps 1024x`| [resizes](/user_guide_examples_resizing_images.html) each image to have 1024 pixels width, otherwise preserving aspect-ratio. |
| `anchor -t resize -ps x768`| [resizes](/user_guide_examples_resizing_images.html) each image to have 768 pixels height, otherwise preserving aspect-ratio. |
| `anchor -t resize -ps 1024x768+`| [resizes](/user_guide_examples_resizing_images.html) each image to maximally fit inside 1024x768 size, preserving aspect-ratio. |
|||
| `anchor -t histogram` | [creates a histogram CSV file](/user_guide_examples_histogram.html) of the pixel values of each image, and all images summed. |
|||
| `anchor -t mean` | calculates the mean-intensity of all images together (which must be identically sized!) |
| `anchor -t meanResize` | like above, but first resizes all images to a common size, and then calculates. |


Note the `-i` and `-o` command line options are [can be applied to any command](/user_guide_examples.html), to select input and outputs.

{% include links.html %}


## Author

[Owen Feehan](http://www.owenfeehan.com) - developed since 2010 personally and via employment in [ETH Zurich](https://ethz.ch/en.html), the [University of Zurich](https://www.uzh.ch/en.html) and [Hoffmann-La Roche](https://www.roche.com/). Licensed [open source](/download.html#licensing).
