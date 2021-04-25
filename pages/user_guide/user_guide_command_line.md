---
title: "User Guide - Command line"
tags: [getting_started]
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_command_line.html
folder: user_guide
---

## Introduction

Anchor can be used from the command-line as follows:

```shell
anchor [options] [experimentFile.xml]
```

If an `experimentFile.xml` isn't specified, the [default experiment](/user_guide.html#defaultExperiment) is employed, with default *inputs*, [task](/user_guide_tasks.html), *outputs*.

## Major options

The **most important** command-line options are:

| Option | Description|
|----------|------------|
| -i *arg* | [Changes inputs](/user_guide.html#inputs), where *arg* = <span class="optionArg"> glob</span> or <span class="optionArg">path to an input-directory</span> or <span class="optionArg">path to BeanXML</span> |
| -t *arg* | [Changes the task](/user_guide.html#task), where *arg* = <span class="optionArg">task-name</span> or <span class="optionArg">path to BeanXML</span> |
| -o *arg* | [Changes outputs](/user_guide.html#outputs), where *arg* = <span class="optionArg">path to an output-directory</span> or <span class="optionArg">path to BeanXML</span> |
| -h | Displays help message with *all* command-line options. |

{% include tip.html content="Typing `anchor -h` will display available command-line arguments" %}

## Input options

Note:
 
- Each input file is assigned a unique identifier, which subsequently determines corresponding output file paths.

- By default, this is inferred from a pattern in the input filenames (e.g. an incrementing integer, varying string etc.) in a minimal way, while capturing the varying elements.

Options useful for influencing **inputting**:

| Option | Description|
|----------|------------|
| -i *arg* | [Changes inputs](/user_guide.html#inputs), where *arg* = <span class="optionArg"> glob</span> or <span class="optionArg">path to an input-directory</span> or <span class="optionArg">path to BeanXML</span> |
| -ic | Copies any unused files (as inputs) in the input directory to the output directory. |
| -ir | Derives the unique identifier from the **entire relative filename or path** (excluding file extension).  |
| -is | Shuffles (randomizes) the order of the inputs.  |

## Output options

Note: 
- tasks produce one or more outputs, with certain outputs enabled by default.
- the file-format used for any given is determined by rules in [defaultBeans.xml](/user_guide_supported_formats.html#changing-the-default-driver).

Options useful for influencing **outputting**:

| Option | Description|
|----------|------------|
| -o *arg* | [Changes outputs](/user_guide.html#outputs) where *arg* = <span class="optionArg">path to an output-directory</span> or <span class="optionArg">path to BeanXML</span> |
| -oa | **Enables all** outputs. |
| -od *outputName(s)* | **Disables specific** output(s). Multiple outputs are comma-separated. |
| -oe *outputName(s)* | **Enables specific** output(s). Multiple outputs are comma-separated. |
| -of *formatExtension* | Suggests an output **image file format**: e.g `-of jpg` or `-of ome.xml` |
| -on | Outputs with **an incrementing number** instead of the input identifier.<br>*(useful for creating sequences of images)* |
| -oo | Omits experiment name and version when outputting. |
| -os | Replaces directory separators (for a file identifier) with an underscore when outputting. |

{% include warning.html content="Non-standard image types (3D, neither monochrome nor RGB etc.) are unsupported by most file formats, so a suggestion with `-of` will often be ignored, in favour of a supported format." %}

## Task options

Options useful for **tasks**:

| Option | Description|
|----------|------------|
| -t *arg* | [Changes the task](/user_guide.html#task), where *arg* = <span class="optionArg">task-name</span> or <span class="optionArg">path to BeanXML</span> |
| -tp *number* | Suggests a maximum number of CPU processors. |
| -st | Prints the names of predefined tasks that can be used with `-t` |
| -ps *size* | Suggests <span class="optionArg">image size</span> (e.g. `1024x768`) or a <span class="optionArg">scaling factor</span> (e.g.`0.5`)<br>- The order of dimensions is always `width`x`height`<br>- No scaling in the z-dimension is supported.<br>- Omitting a dimension resizes to the width/height and <b>preserves aspect-ratio</b> e.g. `200x` or `x50`<br>- A trailing plus character <b>preserves aspect ratio</b> maximally within dimensions e.g. `1000x500+` |

The options beginning with `-p` are parameters that are optionally used only by specific tasks.

## Debug options

Options useful for **debugging**:

| Option | Description|
|----------|------------|
| -d *[string]* | Enables debug-mode: runs only the first available input [whose name contains *string*]. |
| -l *path* | Logs initial [BeanXML](/user_guide_bean_xml.html) errors in greater detail to a <span class="optionArg">file-path</span>  |
| -sa | Shows additional argument information, otherwise executes as normal. |

{% include tip.html content="It's best to use `-d` as the final argument to avoid ambiguity about its optional argument." %}

## Application information options

Options to show general application information are:

| Option | Description|
|----------|------------|
| -h | Displays help message with *all* command-line options. |
| -v | Displays version and authorship information. |

{% include links.html %}
