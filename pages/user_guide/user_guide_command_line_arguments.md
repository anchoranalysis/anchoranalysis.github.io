---
title: "User Guide - Command line arguments"
tags: [getting_started]
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_command_line_arguments.html
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
| -h | Displays help message with *all* command-line options |
| -i *arg* | [Changes inputs](/user_guide.html#inputs). *arg* = a <span class="optionArg">glob</span>, a <span class="optionArg">path to an input-directory</span>, or a <span class="optionArg">path to BeanXML</span> |
| -t *arg* | [Changes the task](/user_guide.html#task). *arg* = a <span class="optionArg">task-name</span> or a <span class="optionArg">path to BeanXML</span> |
| -o *arg* | [Changes outputs](/user_guide.html#outputs). *arg* = <span class="optionArg">path to an output-directory</span> or a <span class="optionArg">path to BeanXML</span> |
| -d [*string*] | Enables debug-mode: runs only the first available input [whose name contains *string*] |

{% include tip.html content="Typing `anchor -h` will display available command-line arguments" %}

{% include tip.html content="It's best to use `-d` as the final option to avoid ambiguity about its optional argument." %}

## Minor options

Options of **lesser importance** are:

| Option | Description|
|----------|------------|
| -v | Displays version and authorship information. |

## Debug options

Options useful for **debugging**:

| -l *path* | Logs initial [BeanXML](/user_guide_bean_xml.html) errors in greater detail to a <span class="optionArg">file-path</span>  |
| -sa | Shows additional argument information, otherwise executes as normal. |

{% include links.html %}
