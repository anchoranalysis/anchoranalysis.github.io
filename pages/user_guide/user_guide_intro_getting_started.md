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

An experiment is *roughly-speaking* the application of a task on inputs to produce outputs.

```
outputs = task(inputs)
```

Inputs are usually images (or images plus extras). Outputs can be images, text-files, CSVs, XML or any other type.

{% include warning.html content="Some tasks produce no outputs, simply writing text to the console." %}

To run an experiment, these three elements must be defined, though often by defaults.

### Defining the three elements

Anchor offers first sensible defaults, allowing for greater definition later.

The default-experiment occurs when you type `anchor` without arguments, and:
1. reads image files (**inputs**) from the current working directory
2. prints some summary information (a **task**)
3. produces no **outputs**.

```
PS D:\Users\owen\Pictures\SomeAlbum> anchor
Searching for inputs as per default experiment.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> All inputs have extension = jpg
-> File-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\${0}.jpg
${0} = "mar" (1) | "jan" (1) | "feb" (1)
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

{% include note.html content="To see BeanXML, look in the Anchor Distribution for `config/defaultExperiment.xml` or `config/tasks/`." %}

Under the hood, an experiment has more than three elements and parameterization aplenty, all initially hidden by defaults.


### Outputs and logs are structured

Two message-logs are produced:
- one for **the experiment** as a whole - printed to the console, and often additionally to `experiment_log.txt`.
- one for **each input** - printed to `job_log.txt` but only if an error occurs processing that particular input.

Outputs are produced in **a particular location. INSERT more here**.

#### Parallelization

Inputs are processed in parallel if possible. Some tasks can be executed each input entirely independently, and so fully in parallel across cores (processors); others involve shared memory and a mixture of parallel and sequential steps.

{% include note.html content="For quick tasks that produce no outputs (i.e. log text only), the execution details are suppressed from the console. For more complicated-tasks, execution details are incrementally printed to the console. Observe if any errors occur!" %}


## Example Usage

### Generating histograms

Consider an example album, with three JPEGs:
```
PS D:\Users\owen\Pictures\SomeAlbum> anchor -t list
jan      -> D:\Users\owen\Pictures\SomeAlbum\jan.jpg
mar      -> D:\Users\owen\Pictures\SomeAlbum\mar.jpg
feb      -> D:\Users\owen\Pictures\SomeAlbum\feb.jpg
```

Let's first generate some summarization of the images (produces output **without** execution-details):

```
PS D:\Users\owen\Pictures\SomeAlbum> anchor -t summarizeImages
Found 3 inputs.
-> Inputs have diverse sizes: 5148x2992(1) 4846x3888(1) 5184x3888(1)
-> All inputs have channels = 3
-> All inputs have bit depth = 8
```

Then let's generate histograms (produces output **with** execution-details):

```
PS D:\Users\owen\Pictures\SomeAlbum> anchor -t histogram
Experiment TestDefaultCommandLineExperiment_1.0 started writing to C:\Users\owen\anchor\TestDefaultCommandLineExperiment_1.0
Using 7 processors from: 8
Job    1:       START   [  0 compl,   3 exec,   0 rem of   3]           feb  1(feb,0s), 2(jan,0s), 3(mar,0s),
Job    3:       START   [  0 compl,   3 exec,   0 rem of   3]           mar  1(feb,0s), 2(jan,0s), 3(mar,0s),
Job    2:       START   [  0 compl,   3 exec,   0 rem of   3]           jan  1(feb,0s), 2(jan,0s), 3(mar,0s),
Job    2:       END     [  1 compl,   2 exec,   0 rem of   3]   (1s)    jan  1(feb,1s), 3(mar,1s),
Job    3:       END     [  2 compl,   1 exec,   0 rem of   3]   (1s)    mar  1(feb,1s),
Job    1:       END     [  3 compl,   0 exec,   0 rem of   3]   (1s)    feb
Writing histogram for all/chnl-0 into C:\Users\owen\anchor\TestDefaultCommandLineExperiment_1.0\all
Writing histogram for all/chnl-1 into C:\Users\owen\anchor\TestDefaultCommandLineExperiment_1.0\all
Writing histogram for all/chnl-2 into C:\Users\owen\anchor\TestDefaultCommandLineExperiment_1.0\all
All 3 jobs completed successfully. The average execution time was 1.684 ms.
Experiment TestDefaultCommandLineExperiment_1.0 completed (1s)
```

Note the complex output with execution details printed on incremental lines as the three inputs are executed.
- Each time a job (for an input) starts or ends, an event line is printed, and with an updated overall status.
- The right side shows remaining jobs (and execution-time so far). For complex tasks, one can notice outlier long-executing jobs.

Files are created

**insert example output here**


{% include links.html %}
