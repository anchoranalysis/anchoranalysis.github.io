---
title: "User Guide - Getting started"
tags: [getting_started]
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_intro_getting_started.html
folder: user_guide
---

## Essentials of Anchor

### Experiments are inputs, task, outputs

An experiment is *roughly-speaking* the application of a task to inputs to produce outputs.

```
outputs = task(inputs)
```

Inputs are usually images (or images plus other files). Outputs can be images, text-files, CSVs, XML or any other type.

Some tasks produce no outputs, simply writing text to the console/log.

To run an experiment, these three elements must be defined, though often by defaults.

### Defining the three elements

Anchor tries to begin with sensible defaults, allowing for greater definition at a later stage.

The default-experiment:
1. reads image files (**inputs**) from the current working directory
2. prints some summary information (a **task**)
3. produces no **outputs**.

It's what occurs when you type `anchor` without arguments, e.g.:

```
Searching for inputs as per default experiment.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> All inputs have extension = jpg
-> File-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\P12109${0}.JPG
${0} = 3 unique integers between 53 and 65 inclusive
```

Each element **(inputs, task, outputs)** can be further defined using a command-line argument `-i` or `-t` or `-o` as follows:


|argument|effect|
|--------|------|
*&lt;ommitted&gt;* | **default behaviour** as per default experiment |
 path to XML file | the element is **defined in BeanXML** at this location |
 glob like `*.jpg` | defines **files for inputs** (only valid with `-i`) |
 other string | defines a **directory-location** for inputs/outputs, or the **task-name** for tasks |

Tasks range from simple operations to complex pipelines of image processing operations (defined in BeanXML). A range of default tasks accompany Anchor, that can be identified by a string e.g. `list`, `summarizeImages`, `histogram`.

Some example commands:
- `anchor -i '..\*.png' -t grayscale -o c:\Temp\GrayscaleAlbum\`
- `anchor -t summarizeImages`
- `anchor -i sunday-hike.xml -t generate_thumbnail.xml -o ../thumbnails/`

#### Defining all elements together in BeanXML

Alternatively, an entire experiment (including all three parts) can be defined in BeanXML, and simply called from
the command-line as a whole, e.g. `anchor pathToSomeExperiment.xml`.

To see the BeanXML, look at `config/defaultExperiment.xml` or `config/tasks` (for the default tasks). Under the hood, an experiment has more than three elements and parameterization aplenty, all initially hidden by defaults.

### Outputs and logs are structured

Inputs are processed in parallel if possible

## Example Usage

{% include links.html %}
