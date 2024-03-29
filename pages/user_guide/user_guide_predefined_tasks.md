---
title: "Example Usage - Predefined Tasks"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_predefined_tasks.html
folder: user_guide
toc: true
---

## Introduction

Some [tasks](/user_guide_tasks.html) are included in the Anchor distribution, to be easily
[run from the command-line](/user_guide_command_line.html) with `-t taskname`, and are termed *predefined tasks*.

{% include tip.html content="See [Example Usage](/user_guide_examples.html) for step-by-step guides on using these tasks. A good starting point!" %}

### Listing available predefined tasks

To list the names of all available predefined tasks, type in a shell either:

- `anchor -st` or
- `anchor -t` (without an argument)

A user can extend the available predefined tasks, by adding [BeanXML](/user_guide_bean_xml.html) to the `/config/tasks` subdirectory in an [Anchor distribution](/developer_guide_anchor_distribution.html).

### How to run a predefined task

To run a [task](/user_guide_tasks.html), open a shell (e.g. `Command Prompt` or `Powershell` in Windows), change to a directory with images, and then:

![commandPrompt_taskName.png](/images/user_guide/commandPrompt_taskName.png)

Next, consider enabling additional outputs with [the ``-o`` options](/user_guide_command_line.html#major-options) or refining your
inputs with [the ``-i`` options](/user_guide_command_line.html#major-options).

{% include tip.html content="In Windows, [hold the shift key when right-clicking on a folder in Windows Explorer](https://www.zdnet.com/article/windows-10-tip-the-fastest-smartest-ways-to-open-a-command-prompt/) to open a Command Prompt or Powershell in that folder." %}

See some [Quick Start - Example Commands](/index.html) and the following tables for guidance.

## Image processing 

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [histogram](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/histogram.xml) | images | [extracts histograms](/user_guide_examples_histogram.html) of the intensity values an image. |
| [resize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/resize.xml) | images | [scales each image](/user_guide_examples_resizing_images.html) to fit inside fixed dimensions, preserving aspect ratio. Optionally accepts [-ps](/user_guide_command_line.html#task-options). |
| [center](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/center.xml) | images | like `resize` but uses a common output size for all images, and centers within it. Optionally accepts [-ps](/user_guide_command_line.html#task-options). |

## Image segmentation

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [segment/coco](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/segment/coco.xml) | images | instance segmentation based on 80 MSCOCO object categories. |
| [segment/text](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/segment/text.xml) | images | finds text-regions in images. |

## Feature extraction

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [feature/hog](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/hog.xml) | images | [extracts](/user_guide_examples_extracting_image_features.html) a [HOG feature descriptor](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients) for all images. |
| [feature/intensity](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/intensity.xml) | images | [extracts](/user_guide_examples_extracting_image_features.html) statistics of pixel values. |
| [feature/metadata](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/metadata.xml) | images | [extracts](/user_guide_examples_extracting_image_features.html) basic metadata as features, including dimensions. |

## Clustering

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [cluster/timestamp](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/cluster/timestamp.xml) | any files | clusters files by timestamp (from (from [EXIF](https://en.wikipedia.org/wiki/Exif), file attributes or naming). |

## File copying / conversion 

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [anonymize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/anonymize.xml) | any files | copies files, **randomizing order and hiding the original naming**. |
| [convert](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/convert.xml) | images | [converts](/user_guide_examples_converting_copying_images.html#converting-images-to-a-different-file-format) the file format** of input images. |
| [copy](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/copy.xml) | any files | [copies](/user_guide_examples_converting_copying_images.html#copying-files) files, preserving naming and subdirectory structure. |

## Montages

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [montage](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/montage.xml) | images | creates a montage that [balances available space](/user_guide_examples_montage.html#balancing-the-number-of-images-per-row). |
| [montage/balance](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/montage/balance.xml) | images | identical to above. |
| [montage/table](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/montage/table.xml) | images | creates a montage that imposes a [table structure](/user_guide_examples_montage.html#table-structure). |
| [montage/slices](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/montage/slices.xml) | images | creates a montage of all z-slices in a 3D image. |


## Summarizing inputs

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [count](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/count.xml) | any files | counts the number of input-files. |
| [list](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/list.xml) | any files | [shows](/user_guide_examples_investigating_images.html#searching-by-default) a line `inputName -> inputPath` for each input. |
| [list/names](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/list/names.xml) | any files | shows each **input's name** on a separate line. |
| [list/paths](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/list/paths.xml) | any files | shows each **input's path** on a separate line. |
| [summarize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/summarize.xml) | images | combines the [summaries](/user_guide_examples_investigating_images.html#summarizing-images) in `summarizeImages` and `summarizePaths` |
| [summarize/images](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/summarize/images.xml) | images | [summarizes](/user_guide_examples_investigating_images.html#summarizing-images) image attributes (dimensions, bit depth etc.) |
| [summarize/paths](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/summarize/paths.xml) | any files | [summarizes](/user_guide_examples_investigating_images.html#summarizing-images) file attributes (size, patterns among the file-paths etc.) |

## Projections across images

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [project/mean](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/project/mean.xml) | images | creates a [mean-intensity projection](/user_guide_examples_intensity_projections.html#mean-intensity-projection) of all inputs. |
| [project/meanResize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/project/meanResize.xml) | images | scales inputs to a constant size, then the `mean` projection. |
| [project/max](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/project/max.xml) | images | creates a [maximum-intensity projection](/user_guide_examples_intensity_projections.html#maximum-intensity-projection) of all inputs. |
| [project/maxResize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/project/maxResize.xml) | images | scales inputs to constant size, then the `max` projection. |
| [project/min](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/project/min.xml) | images | creates a [minimum-intensity projection](/user_guide_examples_intensity_projections.html#minimum-intensity-projection) of all inputs. |
| [project/minResize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/project/minResize.xml) | images | scales inputs to constant size, then the `mean` projection. |
| [project/standardDeviation](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/project/standardDeviation.xml) | images | creates a [standard-deviation projection](/user_guide_examples_intensity_projections.html#standard-deviation-intensity-projection) of all inputs. |
| [project/standardDeviationResize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/project/standardDeviationResize.xml) | images | scales inputs to constant size, then the above projection. |
{% include links.html %}