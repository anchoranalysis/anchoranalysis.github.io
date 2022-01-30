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
| -i *arg* | [Changes inputs](/user_guide.html#inputs), where *arg* = [extension](/user_guide_examples_investigating_images.html#filtering-with-a-file-extension) or [wildcards](/user_guide_examples_investigating_images.html#filtering-with-wildcards) or <span class="optionArg">input-directory path</span> or <span class="optionArg">path to BeanXML</span> |
| -t *[arg]* | [Changes the task](/user_guide.html#task), where *arg* = <span class="optionArg">[predefined-task-name](/user_guide_predefined_tasks.html)</span> or <span class="optionArg">path to BeanXML</span> |
| -o *arg* | [Changes outputs](/user_guide.html#outputs), where *arg* = <span class="optionArg">path to an output-directory</span> or <span class="optionArg">path to BeanXML</span> |
| -h | Displays help message with *all* command-line options. |

{% include tip.html content="Typing `anchor -h` will display available command-line options" %}

## Input options

Note:
 
- Each input file is assigned a *unique name*, which subsequently determines corresponding output file paths.

- By default, this is inferred from a pattern in the input filenames (e.g. an incrementing integer, varying string etc.) in a minimal way, while capturing the varying elements.

Options useful for influencing **inputting**:

| Option | Description|
|----------|------------|
| -i *arg* | [Changes inputs](/user_guide.html#inputs), where *arg* = [extension](/user_guide_examples_investigating_images.html#filtering-with-a-file-extension) or [wildcards](/user_guide_examples_investigating_images.html#filtering-with-wildcards) or <span class="optionArg">input-directory path</span> or <span class="optionArg">path to BeanXML</span> |
| -ic | [Copies any files unused as inputs](/user_guide_examples_changing_output_options.html#additionally-copying-non-input-files) (but existing within the input directory) to the output directory. |
| -ii | **Subsets the name** from the file-path pattern. Type `anchor` and look for `${0}`, `${1}` etc.<br>Zero-indexed. Negatives count backwards from the end. Can be a single index or a range.<br>e.g. `2` (third only) or `-3` (third-last) or `3:-1` (fourth to last) or `:2` (until third) or `2:` (from third). |
| -il *num* | Uses [only the initial](/user_guide_examples_anonymizing_sampling.html#subsetting-inputs) `num` inputs (when an integer), or `(num*100)%` when in interval `(0.0,1.0)` |
| -ir | Derives the name instead from the [entire relative file-path](/user_guide_examples_changing_output_options.html#disabling-the-shortened-identifiers) excluding the file extension.<br>e.g. it selects `subdir/prefix_234` rather than `234` (by default, only what varies among filenames).  |
| -is | [Shuffles](/user_guide_examples_video_from_images.html#randomizing-the-image-order) (randomizes) the order of the inputs. |

## Output options

Note: 
- tasks produce one or more outputs, with certain outputs enabled by default.
- the file-format used for any given is determined by rules in [defaultBeans.xml](/user_guide_supported_formats.html#specifying-default-readers-and-writers).

Options useful for influencing **outputting**:

| Option | Description|
|----------|------------|
| [-o](/user_guide.html#outputs) *arg* | [Changes outputs](/user_guide.html#outputs) where *arg* = <span class="optionArg">path to an output-directory</span> or <span class="optionArg">path to BeanXML</span> |
| -oa | [Enables all](/user_guide_examples_changing_output_options.html#enabling-and-disabling-outputs) outputs. |
| -oc | Disables opening the output directory in the desktop (upon experiment end). |
| -od *outputName(s)* | [Disables specific](/user_guide_examples_changing_output_options.html#enabling-and-disabling-outputs) output(s). Multiple outputs are comma-separated. |
| -oe *outputName(s)* | [Enables specific](/user_guide_examples_changing_output_options.html#enabling-and-disabling-outputs) output(s). Multiple outputs are comma-separated. |
| -of *formatExtension* | Suggests an output [image file format](/user_guide_examples_changing_output_options.html#specifying-an-alternative-image-format): e.g `-of jpg` or `-of ome.xml` |
| -on | Outputs with [an incrementing number](/user_guide_examples_changing_output_options.html#writing-outputs-as-a-sequence) instead of the input name.<br>*(useful for creating sequences of images)* |
| -oo | [Omits experiment name and version](/user_guide_examples_changing_output_options.html#outputting-to-a-specific-output-directory-avoiding-creating-a-subdirectory) when outputting. |
| -os | [Replaces directory separators](/user_guide_examples_changing_output_options.html#suppressing-directory-structure) in the output file-path with an underscore. |

{% include warning.html content="Non-standard image types (3D, neither monochrome nor RGB etc.) are unsupported by most file formats, so a suggestion with `-of` will often be ignored, in favour of a supported format." %}

## Task options

Options useful for **tasks**:

| Option | Description|
|----------|------------|
| -t *[arg]* | [Changes the task](/user_guide.html#task), where *arg* = <span class="optionArg">predefined-task-name</span> or <span class="optionArg">path to BeanXML</span> |
| -tp *number* | Suggests a [maximum number of CPU processors](/user_guide_troubleshooting.html#limiting-parallel-cpu-cores). |
| -st | Prints the names of [predefined tasks](/user_guide_predefined_tasks.html) that can be used with `-t` |
| -ps *size* | [Suggests](/user_guide_examples_resizing_images.html) <span class="optionArg">image size</span> (e.g. `1024x768`) or a <span class="optionArg">scaling factor</span> (e.g.`0.5`)<br>- The order of dimensions is always `width`x`height`<br>- No scaling in the z-dimension is supported.<br>- Omitting a dimension resizes to the width/height and <b>preserves aspect-ratio</b> e.g. `200x` or `x50`<br>- A trailing plus character <b>preserves aspect ratio</b> maximally within dimensions e.g. `1000x500+` |

The options beginning with `-p` are parameters that are optionally used only by specific tasks.

{% include tip.html content="[Predefined tasks](/user_guide_predefined_tasks.html) is an important reference for tasks that can be easily calledwith `-t`." %}

## Debug options

Options useful for **debugging**:

| Option | Description|
|----------|------------|
| -d *[string]* | Enables debug-mode: runs only the first available input [whose name contains *string*]. |
| -l *path* | Logs initial [BeanXML](/user_guide_bean_xml.html) errors in greater detail to a <span class="optionArg">file-path</span>  |
| -sa | Shows additional command-line option information, otherwise executes as normal. |

{% include tip.html content="It's best to use `-d` as the final option to avoid ambiguity about its optional argument." %}

## Application information options

Options to show general application information are:

| Option | Description|
|----------|------------|
| -h | Displays help message with *all* command-line options. |
| -v | Displays version and authorship information. |

{% include links.html %}
