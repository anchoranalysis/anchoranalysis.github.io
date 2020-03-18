---
title: "User Guide - Essentials"
tags: [getting_started]
keywords:
sidebar: user_guide_sidebar
permalink: user_guide.html
folder: user_guide
---

## Essentials of Anchor

### Experiments are inputs, task, outputs

An experiment is *roughly-speaking* the execution of a **task** on **inputs** to produce **outputs**.

```
outputs = task(inputs)
```

Inputs are usually images (or images plus extras). Outputs can be images, text-files, CSVs, XML or any other file-type.

{% include warning.html content="Some tasks produce no outputs, simply writing text to the console." %}

To run an experiment, these three elements must be defined, though often by defaults.

### Defining experiments

#### The default experiment

Anchor offers first sensible defaults, allowing for greater definition later.

The [default-experiment](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/src/main/resources/config/defaultExperiment.xml) occurs when you type `anchor` without arguments, and:
1. reads image files (**inputs**) from the current working directory.
2. prints some summary information (a **task**).
3. produces no **outputs**.

<pre>
PS D:\Users\owen\Pictures\SomeAlbum> <b>anchor</b>
Searching for inputs as per default experiment.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> All inputs have extension = jpg
-> File-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\${0}.jpg
${0} = "mar" (1) | "jan" (1) | "feb" (1)
</pre>

#### Overriding elements from the command-line

Each element **(inputs, task, outputs)** can be overridden using a command-line argument `-i` or `-t` or `-o` as follows:


|argument|effect|
|--------|------|
*&lt;ommitted&gt;* | **default behaviour** as per default experiment |
 path to XML file | the element is **defined in BeanXML** at this location |
 glob like `*.jpg` | defines **files for inputs** (only valid with `-i`) |
 other string | defines a **directory-location** for inputs/outputs, or the **task-name** for tasks |

#### Examples of tasks and commands

Tasks range from simple operations to complex pipelines of image processing operations (defined in BeanXML). A range of default tasks accompany Anchor that can be identified by a string e.g. `list`, `summarizeImages`, `histogram`.

Some example commands:
- `anchor -i '..\*.png' -t grayscale -o c:\Temp\GrayscaleAlbum\`
- `anchor -t summarizeImages`
- `anchor -i sunday-hike.xml -t generate_thumbnail.xml -o ../thumbnails/`

#### Defining in BeanXML

Instead of element-wise definition on the command line (with `-i`, `-t`, `-o` etc.), an entire experiment can be defined in BeanXML, and simply called from the command-line as a whole, e.g. `anchor pathToSomeExperiment.xml`.

{% include tip.html content="To see BeanXML look in the Anchor Distribution for `config/defaultExperiment.xml` or `config/tasks/`" %}

In full reality, an experiment has more than three elements, as well as wide parameterization possibilities, all initially hidden by defaults. BeanXML provides more finely-grained definition.


### Outputs and logs are structured

Two message-logs are produced:
- one for **the experiment** as a whole - printed to the console, and often additionally to `experiment_log.txt`.
- one for **each input** - printed to `job_log.txt` but only if an error occurs processing that particular input.

Outputs are produced by default in a temporary directory, easily changed with the `-o` options.

#### Parallelization

Inputs are processed in parallel if possible. Some tasks can be executed each input entirely independently, and so fully in parallel across cores (processors); others involve shared memory and a mixture of parallel and sequential steps.

{% include note.html content="For quick tasks that produce no outputs (i.e. log text only), the execution details are suppressed from the console. For more complicated-tasks, execution details are incrementally printed to the console. Observe if any errors occur!" %}


## Example Usage

Some example guides walk through executing commands:

- Generating a [histogram](/user_guide_examples_histogram.html) of pixel intensities from each channel.




{% include links.html %}
