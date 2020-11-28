---
title: "Example Usage - Overview"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples.html
folder: user_guide
toc: false
---

## Step-by-step guides

- Generating a [histogram](/user_guide_examples_histogram.html) of pixel intensities from each channel.

## Predefined tasks

Some [tasks](/user_guide_tasks.html) are included in the Anchor distribution, to be easily
[run from the command-line](/user_guide_command_line.html) with `-t taskname`.  

### For image processing 

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [histogram](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/src/main/resources/config/tasks/convert.xml) | images | extracts histograms of the intensity values an image. |

### For file copying / conversion 

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [convert](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/src/main/resources/config/tasks/convert.xml) | images | converts an image into another file format. |

### For summarizing inputs

| Task Name | Input Type | Description  |
|-----------|------------|--------------|
| [countFiles](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/src/main/resources/config/tasks/countFiles.xml) | file paths | counts the number of input-files. |

{% include links.html %}