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

If an `experimentFile.xml` isn't specified, the [default experiment](/user_guide.html#defaultExperiment) is employed, with default *inputs*, *task*, *outputs*.

## Major options

The **most important** command-line options are:

| Option | Description|
|----------|------------|
| -i *arg* | [Changes inputs](/user_guide.html#inputs), where *arg* = <span class="optionArg"> glob</span> or <span class="optionArg">path to an input-directory</span> or <span class="optionArg">path to BeanXML</span> |
| -t *arg* | [Changes the task](/user_guide.html#task), where *arg* = <span class="optionArg">task-name</span> or <span class="optionArg">path to BeanXML</span> |
| -o *arg* | [Changes outputs](/user_guide.html#outputs), where *arg* = <span class="optionArg">path to an output-directory</span> or <span class="optionArg">path to BeanXML</span> |
| -h | Displays help message with *all* command-line options. |

{% include tip.html content="Typing `anchor -h` will display available command-line arguments" %}

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

{% include warning.html content="Non-standard image types (3D, neither monochrome nor RGB etc.) are unsupported by most file formats, so a suggestion with `-of` will often be ignored, in favour of a supported format." %}

## Task options

Options useful for **tasks**:

| Option | Description|
|----------|------------|
| -t *arg* | [Changes the task](/user_guide.html#task), where *arg* = <span class="optionArg">task-name</span> or <span class="optionArg">path to BeanXML</span> |
| -st | Prints the names of predefined tasks that can be used with `-t` |
| -tr | Suggests an <span class="optionArg">image dimensions to resize to</span> e.g. `-tr 1024x768` or a <span class="optionArg">scaling factor</span> e.g.`-tr 0.5`<br>To preserve aspect ratio, try: `200x` or `x50` to resize to a particular width/height, or `1000x500+` to resize maximally within these dimensions.<br>No scaling in the z-dimension is supported. |

Certain options like `-ts` apply only to particular tasks that employ scaling.

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
