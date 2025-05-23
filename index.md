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

Anchor is a free command-line application and platform for image processing and computer vision.

{% include callout.html type="danger" content="It's a Swiss-army-knife for loading, transforming, and extracting information from **sets of images**, as single-image tools are often limiting." %}

It quickly searches subdirectories of images on the file-system and processes!

{% include tip.html content="[Download](/download.html) and [install](/installation.html). Then see [example usage](/user_guide_examples.html), the [user guide](/user_guide.html) and the [command line](/user_guide_command_line.html)." %}

## Features

<img src="/images/anchor_medium_logo.png" alt="Anchor logo" style="float:right;width:341px;height:163px;">

- Supports diverse image types and formats (photos, 2D / 3D / time-series microscopy).
- Smartly names outputs by finding patterns in filenames. Preserves directory structure.
- Reproducible pipelines defined via XML.
- Feature-extraction libraries (sets of voxels, geometric shapes) etc.
- Extensible via Java to call operations in [ImageJ](https://imagej.net/Welcome), [OpenCV](https://opencv.org/) etc.
- Cross-platform - Windows, Linux, Mac.
- Deep Learning inference with the [ONNX Runtime](https://onnxruntime.ai/).


## Project Status {#projectStatus}

Anchor's source-code can be found on [GitHub](https://github.com/anchoranalysis). Please report any bug / feature request as an [issue](https://github.com/anchoranalysis/anchor/issues).


## Quick Start - Example Commands

Start a task, by opening a shell in a directory of images and typing `anchor -t <someTask>`.

By default, it will search recursively for all images in this directory (with [standard extensions](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/defaultInputExtensions.xml)).


| Command | What it does? |
|------------|------------------|
| `anchor` | searches for images *recursively* in the current directory, and derives a naming pattern. |
| `anchor -i c:\foo\bar` | like above, but searches in the specified directory (*recursively*). |
| `anchor -i .png` | like above, but searches only for `.png` in the current directory (*recursively*). |
| `anchor -h` | shows all available [command-line options](/user_guide_command_line.html) |
| `anchor -t` or `anchor -st` | shows all available [predefined tasks](/user_guide_predefined_tasks.html). |
|||
| `anchor -t summarize` | [summarizes](/user_guide_examples_investigating_images.html#searching-by-default) images into bullet points (extension, file naming patterns, size etc.). |
| `anchor -t summarize -i d:\foo\` | [summarizes](/user_guide_examples_investigating_images.html#searching-by-default) images recursively in a particular directory. |
| `anchor -t summarize -i .tif -i .png`| [summarizes](/user_guide_examples_investigating_images.html#searching-by-default) only images that end with the extensions `.tif` or `.png` (recursively) |
| `anchor -t summarize -i *match*.tif`| [summarizes](/user_guide_examples_investigating_images.html#searching-by-default) only images matching the wildcard *non-recursively* in the input directory. |
| `anchor -t summarize -i "**match**.tif"`| [summarizes](/user_guide_examples_investigating_images.html#searching-by-default) only images matching the wildcard <i>recursively</i> (unsupported on [some shells](/user_guide_examples_investigating_images.html#filtering-with-wildcards)! |
| `anchor -t list`| [lists](/user_guide_examples_investigating_images.html#searching-by-default) the paths and unique-identifier for each input. |
|||
| `anchor -t feature/metadata` | [creates a CSV](/user_guide_examples_extracting_image_features.html) with images as rows, and **image metadata** as columns. |
| `anchor -t feature/intensity` | [creates a CSV](/user_guide_examples_extracting_image_features.html) with images as rows, and **intensity statistics** as columns. |
| `anchor -t feature/hog` | [creates a CSV](/user_guide_examples_extracting_image_features.html) with images as rows, and a [HOG descriptor](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients) as columns. |
| `anchor -t feature/hog -pg -oe featuresAggregated` | like above, but adds [grouping](/user_guide_examples_extracting_image_features.html#grouping) with an aggregated CSV file.  |
|||
| `anchor -t segment/text` | finds and segments regions of texts in images |
| `anchor -t segment/coco` | finds and segments common categories of objects in images. |
|||
| `anchor -t convert -ip -of png` | [converts](/user_guide_examples_converting_copying_images.html#converting-images-to-a-different-file-format) all images to *PNG* format (or pick [another extension](/user_guide_examples_changing_output_options.html#specifying-an-alternative-image-format)!) |
| `anchor -t convert -ip -of png -ic -oo d:\foo` | [converts](/user_guide_examples_converting_copying_images.html#preserving-relative-file-paths-and-any-non-image-files) like above to a particular directory, and copies non-image files (e.g. metadata!) |
| `anchor -t copy -ip -oo d:\foo` | [copies](/user_guide_examples_converting_copying_images.html#copying-files) all images to a particular new directory. |
| `anchor -t copy -is -on` | randomizes the order of images and anonymizes the filename. |
| `anchor -t cluster/timestamp` | clusters images that are adjacent in time (from [EXIF](https://en.wikipedia.org/wiki/Exif), file attributes or naming) |
|||
| `anchor -t resize -ps 0.1`| [resizes](/user_guide_examples_resizing_images.html) each image to have a <i>tenth</i> of the width and height (try `2` to double). |
| `anchor -t resize -ps 1024x768`| [resizes](/user_guide_examples_resizing_images.html) each image to have `1024x768` size in pixels. |
| `anchor -t resize -ps 1024x768 -on`| [resizes](/user_guide_examples_resizing_images.html) like above, but outputs as an incrementing sequence (useful for creating [videos](/user_guide_examples_video_from_images.html)!) |
| `anchor -t resize -ps 1024x`| [resizes](/user_guide_examples_resizing_images.html) each image to have `1024` pixels width, otherwise preserving aspect-ratio. |
| `anchor -t center -ps 1024x`| like above, but each output image has a identical common size, centering within it. |
| `anchor -t resize -ps x768`| [resizes](/user_guide_examples_resizing_images.html) each image to have `768` pixels height, otherwise preserving aspect-ratio. |
| `anchor -t center -ps x768+`| like above, but each output image has a identical common size, centering within it. |
| `anchor -t resize -ps 1024x768+`| [resizes](/user_guide_examples_resizing_images.html) each image to maximally fit inside `1024x768` size, preserving aspect-ratio. |
| `anchor -t center -ps 1024x768+`| like above, but each output image has a identical common size, centering within it. |
|||
| `anchor -t histogram` | [creates a histogram CSV file](/user_guide_examples_histogram.html) of the pixel values of each image, and all images summed. |
|||
| `anchor -t montage` | creates a [montage of all images](/user_guide_examples_montage.html#filling-all-available-space) (recursively). |
| `anchor -t montage -il 20` | creates a montage from the [initial](/user_guide_examples_anonymizing_sampling.html#taking-the-initial-n-inputs-in-order) `20` images in order. |
| `anchor -t montage -ir 20` | creates a montage from a [random sample](/user_guide_examples_montage.html#sampling-images) of `20` images. |
| `anchor -t montage -ir 0.04` | creates a montage from a [random sample](/user_guide_examples_montage.html#sampling-images) of `4%` of all images. |
| `anchor -t montage -oe unlabelled` | creates an [unlabelled montage](/user_guide_examples_montage.html#removing-labels) (additionally). |
| `anchor -t montage -ps 2000x` | creates a montage that has `2000 pixels` [width](/user_guide_examples_montage.html#specifying-the-size). |
| `anchor -t montage -ps 0.3` | creates a montage where [image widths](/user_guide_examples_montage.html#specifying-the-size) are approximately `30%` of their original. |
| `anchor -t montage/table` | creates a montage with a [table structure](/user_guide_examples_montage.html#table-structure). |
| `anchor -t montage/slices` | creates a montage of the z-slices of a 3D image. |
|||
| `anchor -t project/mean` | projects the [mean-intensity](/user_guide_examples_intensity_projections.html#mean-intensity-projection) of all images (which *must* be identically sized!) |
| `anchor -t project/meanResize` | like above, but first resizes all images to a common size, and then calculates. |
| `anchor -t project/meanResize -pg 0` | like above, but [groups](/user_guide_examples_intensity_projections.html#grouping) by the *first* element in the identifier. |
| `anchor -t project/meanResize -pg 0:1` | like above, but [groups](/user_guide_examples_intensity_projections.html#grouping) by the *first two* elements in the identifier. |
| `anchor -t project/meanResize -pg -1` | like above, but [groups](/user_guide_examples_intensity_projections.html#grouping) by the *last* element in the identifier. |
| `anchor -t project/max` | projects the [maximum-intensity](/user_guide_examples_intensity_projections.html#maximum-intensity-projection) of all images (which *must* be identically sized!) |
| `anchor -t project/min` | projects the [minimum-intensity](/user_guide_examples_intensity_projections.html#minimum-intensity-projection) of all images (which *must* be identically sized!) |
| `anchor -t project/standardDeviation` | projects the [standard-deviation](/user_guide_examples_intensity_projections.html#standard-deviation-intensity-projection) of all images (which *must* be identically sized!) |
|||
| `anchor -t copy -ir 20` | [randomly samples](/user_guide_examples_anonymizing_sampling.html#a-random-subset) 20 inputs. |
| `anchor -t copy -ir 0.3` | [randomly samples](/user_guide_examples_anonymizing_sampling.html#a-random-subset) 30% of all inputs. |
| `anchor -t copy -ir 0.3 -on` | [randomly samples](/user_guide_examples_anonymizing_sampling.html#a-random-subset) and [anonymizes](/user_guide_examples_anonymizing_sampling.html#anonymizing) 30% of all inputs. |

Note the `-i` and `-o` command line options are [can be applied to any task](/user_guide_examples.html) to select inputs and an output path. `outputs = task(inputs)`

{% include links.html %}


## Author

[Owen Feehan](http://www.owenfeehan.com) - developed since 2010 personally and via employment in [ETH Zurich](https://ethz.ch/en.html), the [University of Zurich](https://www.uzh.ch/en.html) and [Hoffmann-La Roche](https://www.roche.com/). Licensed [open source](/download.html#licensing).
