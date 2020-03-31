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

### Default experiment

Anchor offers first sensible defaults, allowing for greater definition later.

The [default-experiment](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/src/main/resources/config/defaultExperiment.xml) occurs when you type `anchor` without arguments, and:
1. reads image files (**inputs**) from the current working directory.
2. prints some summary information (a **task**).
3. produces no **outputs**.

{% include shell.html
command="anchor"
response="Searching for inputs as per default experiment.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> All inputs have extension = jpg
-> File-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\${0}.jpg
${0} = \"mar\" (1) | \"jan\" (1) | \"feb\" (1)" %}

### Overriding elements on command-line

Each element **(inputs, task, outputs)** can be overridden using a command-line argument `-i` or `-t` or `-o` as follows:

#### Changing inputs with `-i`

|`-i` argument| input |
|--------|------|
| *&lt;ommitted&gt;* | *default*: reads images recursively from **current** directory |
| `-i` path to XML file | input as defined in **BeanXML** at this path |
| `-i` glob  *(e.g. `*.jpg`)* | reads **files matching the glob** |
| `-i` other path | reads images recursively from the **specified** directory  |

#### Changing the task with `-t`

|`-t` argument| input |
|--------|------|
| *&lt;ommitted&gt;* | *default*: **summary statistics** for current inputs |
| `-t` path to XML file | task as defined in **BeanXML** at this path |
| `-t` other string | looks for a **task** in `config/tasks/` matching this name  |

#### Changing outputs with `-o`

|`-o` argument| input |
|--------|------|
| *&lt;ommitted&gt;* | *default*: writes into a **temporary directory** |
| `-o` path to XML file | output as defined in **BeanXML** at this path |
| `-o` other string | writes into the **specified** directory (creates a subdirectory)  |

#### Combining arguments

These arguments can be combined to accomplish both simple and complex pipelines (defined in BeanXML).

Some example commands:

```shell
# input from glob, task by name, output into a specific absolute directory
anchor -i '..\*.png' -t grayscale -o 'c:\Temp\GrayscaleAlbum\'

# task by name
anchor -t summarizeImages

# input and task from BeanXML, output into a specific relative directory
anchor -i sunday-hike.xml -t generate_thumbnail.xml -o ../thumbnails/
```

{% include tip.html content="Prespecified tasks can be identified simple by their **task-name** e.g. [grayscale](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/config/tasks/grayscale.xml), [summarizeImages](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/config/tasks/summarizeImages.xml)." %}

### Defining an entire experiment in BeanXML

Instead of element-wise definition on the command line (with `-i`, `-t`, `-o` etc.), an entire experiment can be defined in BeanXML, and simply called from the command-line as a whole, e.g. `anchor pathToSomeExperiment.xml`.

{% include tip.html content="To see BeanXML look in the Anchor Distribution for [config/defaultExperiment.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor-assembly/src/main/resources/config/defaultExperiment.xml) or [config/tasks/](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/config/tasks)" %}

In full reality, an experiment has more than three elements, as well as wide parameterization possibilities, all initially hidden by defaults. BeanXML provides more finely-grained definition.


### Outputs and logs are structured

Two message-logs are produced:
- `experiment_log.txt` for the **experiment as a whole** and also printed to the console.
- `job_log.txt` for **each input** but **only if an error occurs**.

Outputs are produced by default in a temporary directory, easily changed with the `-o` options.

#### Parallelization

Inputs are processed in parallel if possible. Some tasks can be executed each input entirely independently, and so fully in parallel across cores; others involve shared memory and a mixture of parallel and sequential steps.

{% include note.html content="Quick tasks that only print text to the console **suppress execution details**. Otherwise, for more complicated-tasks, **per-input execution progress** is incrementally printed to the console. Observe if any errors occur!" %}

{% include tip.html content="See [Example Usage](/user_guide_examples.html) for a practical step-by-step guide to using Anchor." %}

{% include links.html %}
