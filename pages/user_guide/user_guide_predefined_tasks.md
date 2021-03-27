---
title: "Example Usage - Predefined Tasks"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_predefined_tasks.html
folder: user_guide
toc: true
---

## How to run a task

Some [tasks](/user_guide_tasks.html) are included in the Anchor distribution, to be easily
[run from the command-line](/user_guide_command_line.html) with `-t taskname`.  

To run a [task](/user_guide_tasks.html), open a shell (e.g. `Command Prompt` or `Powershell` in Windows), change to a directory with images, and then:

![commandPrompt_taskName.png](/images/user_guide/commandPrompt_taskName.png)

Next, consider enabling additional outputs with [the ``-o`` options](/user_guide_command_line.html#major-options) or refining your
inputs with [the ``-i`` options](/user_guide_command_line.html#major-options).

{% include tip.html content="In Windows, [hold the shift key when right-clicking on a folder in Windows Explorer](https://www.zdnet.com/article/windows-10-tip-the-fastest-smartest-ways-to-open-a-command-prompt/) to open a Command Prompt or Powershell in that folder. " %}

## Image processing 

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [histogram](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/histogram.xml) | images | **extracts histograms** of the intensity values an image. |
| [mean](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/mean.xml) | images | creates a **mean-intensity projection** of all inputs. |
| [meanResize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/meanResize.xml) | images | scales inputs to fixed dimensions, and then a mean-intensity projection. |
| [resize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/resize.xml) | images | **scales each image to fit inside fixed dimensions**, preserving aspect ratio. Optionally accepts [-pr](/user_guide_command_line.html#task-options). |
| [stack/montage](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/stack/montage.xml) | images (3D) | produces a tiled **montage of all z-slices of a 3D image** |

## Image segmentation

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [text](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/text.xml) | images | finds text-regions in images. |

## Feature extraction

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [feature/hog](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/hog.xml) | images | extracts a [HOG feature descriptor](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients) for all images. |
| [feature/metadata](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/metadata.xml) | images | extracts some basic metadata as features, including dimensions. |

## File copying / conversion 

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [anonymize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/anonymize.xml) | any files | copies files, **randomizing order and hiding the original naming**. |
| [convert](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/convert.xml) | images | **converts the file format** of input images. |
| [copy](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/copy.xml) | any files | **copies files**, preserving naming and subdirectory structure. |

## Summarizing inputs

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [countFiles](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/countFiles.xml) | any files | counts the number of input-files. |
| [list](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/list.xml) | any files | shows a line `inputName -> inputPath` for each input. |
| [listNames](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/listNames.xml) | any files | shows each **input's name** on a separate line. |
| [listPaths](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/listPaths.xml) | any files | shows each **input's path** on a separate line. |
| [summarize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/summarize.xml) | images | combines the summaries in `summarizeImages` and `summarizePaths`. |
| [summarizeImages](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/summarizeImages.xml) | images | **summarizes image attributes** (dimensions, bit depth etc.) |
| [summarizePaths](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/summarizePaths.xml) | any files | **summarizes file attributes** (size, patterns among the file-paths etc.) |


{% include links.html %}