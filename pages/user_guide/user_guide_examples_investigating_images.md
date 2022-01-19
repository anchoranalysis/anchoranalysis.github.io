---
title: "Example - Investigating image files"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_investigating_images.html
folder: user_guide
---

## Background

Imagine that you have **a directory containing many images**, possibly distributed among sub-directories.

Images are often stored in this form after being acquired by cameras, phones, microscopes and other  devices.

Often, **a necessary first step for processing is to understand the contents**, with questions like:

- how many images?
- what image format?
- what kind of naming scheme?
- with what image size?
- related to each other how?

This guide describes how *Anchor* can be used on the command-line to quickly answer many of these **data exploration** questions, including creating CSV files describing key image features.


## Finding files and summarizing

### Searching by default

Anchor, by default, will **search the current working directory recursively** for image files (with common [filename extensions](https://github.com/anchoranalysis/anchor/blob/master/anchor-core/src/main/java/org/anchoranalysis/core/format/ImageFileFormat.java)) and report a summary of the files in the console.

The summary describes the files <i>collectively</i> not individually.

{% include shell.html
command="anchor"
response="Searching recursively for image files. CTRL+C cancels.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> with uniform extension = jpg
-> file-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\alps-${0}.jpg
${0} = 3 unique integers between 13 and 91 inclusive" %}

Anchor has found 3 images in this directory, all with `jpg` extension.

It also found a pattern among the paths. This pattern has only one varying element `${0}` but often there will be more: `${0}`, `${1}`, `${2}` etc.

A **name** is inferred from the varying element(s) (`78`, `91` and `13`), and can be seen with `-t list`:

{% include shell.html
command="anchor -t list"
response="78       -> D:\Users\owen\Pictures\SomeAlbum\alps-78.jpg
91       -> D:\Users\owen\Pictures\SomeAlbum\alps-91.jpg
13       -> D:\Users\owen\Pictures\SomeAlbum\alps-13.jpg" %}

When processing the inputs, this *name* will be used as a **unique identifier**, and also to **determine  paths for outputs**.

### Summarizing images

Now let's request more detailed summarization of the images, not just as files, but as images with width, height, number of channels, bit depth etc.

{% include shell.html
command="anchor -t summarize"
response="Found 3 inputs.
-> with uniform extension = jpg
-> with diverse sizes: 5148x2992(1) 4846x3888(1) 5184x3888(1)
-> with uniform channel = 3
-> with uniform bit depth = 8
-> file-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\alps-${0}.jpg
${0} = 3 unique integers between 13 and 91 inclusive" %}

{% include warning.html content="The summary will take longer to run, as it considers each image file's metadata, not just the file-path and size." %}


### Further specifying the search

The [`-i` command-line option](/user_guide.html#inputs) can further specify which images we seek:

- **a file extension** not included in the [default search](https://github.com/anchoranalysis/anchor/blob/master/anchor-core/src/main/java/org/anchoranalysis/core/format/ImageFileFormat.java): `-i .zvi` or `-i *.zvi`
- **a narrower range with a *wildcard*** (applied on all filenames recursively): `-i foo*bar`
- **a different directory**: `-i path_to_directory`
- as *advanced usage*, **a file with [BeanXML](/user_guide_bean_xml.html)** describing inputs: `-i path_to_bean.xml`

{% include tip.html content="Wildcard implementations vary across shells e.g. [Windows PowerShell](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_wildcards?view=powershell-7.1), [Command Prompt](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/indexsrv/ms-dos-and-windows-wildcard-characters), [bash](https://linuxhint.com/bash_globbing_tutorial/), etc. **Placing the wildcard expression in double-quotes** can help solve problems by letting Anchor process the expression by its own rules: e.g. `-i \"foo*bar\"`" %}

### Changing the derived input name

By default, the unique name is derived only from the varying elements of the pattern found in the paths e.g. (`13`, `78` and `91`).

The [`-ir` command-line option](/user_guide_command_line.html#input-options) instead **keeps the entire file-name** (the entire file-path after the input directory), including the non-varying elements e.g. (`alps-78`, `alps-91` and `alps-13`). Note the file extension continues to be omitted.

{% include shell.html
command="anchor -ir -t list"
response="alps-13  -> alps-13.jpg
alps-78  -> alps-78.jpg
alps-91  -> alps-91.jpg" %}

If the path has **redundant varying elements** (parts of the path which vary, but are not needed for the unique identifier), then the [`-ii` command-line option](/user_guide_command_line.html#input-options) can remove the unneeded elements by subsetting them.

## Extracting features from images

The previous commands with *summary tasks* gave an overview of the image files *collectively*.

Often, it is useful to generate summary information **specifically for each image**.

We can consider this as extracting [features](https://en.wikipedia.org/wiki/Feature_(machine_learning)) from each image, in the machine learning sense of a *feature*.

Anchor has [predefined tasks](/user_guide_predefined_tasks.html#feature-extraction) to generate CSV files with different kinds of information.

### Metadata features

The predefined task [feature/metadata](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/metadata.xml) will extract features from the image header like width, height, number of channels etc. also providing physical measurements in microns, if included in image metadata.

{% include shell.html
command="anchor -t feature/metadata"
response="Experiment metadata_12.41.23 started writing to C:\Users\owen\AppData\Local\Temp\metadata_12.41.23
------------------------------------ Inputs ------------------------------------
The job has 3 inputs.

They are named with the pattern: ${0}
${0} = 3 unique integers between 13 and 91 inclusive
---------------------------------- Processing ----------------------------------
Preparing jobs to run with common initialization.
Using 7 processors CPUs from 8, and if needed and if possible, up to 0 simultaneous jobs using a GPU.
Job    2:       start   [  0 compl,   3 exec,   0 rem of   3]           78
Job    1:       start   [  0 compl,   3 exec,   0 rem of   3]           13
Job    3:       start   [  0 compl,   3 exec,   0 rem of   3]           91
Job    2:       end     [  1 compl,   2 exec,   0 rem of   3]   (5s)    78
Job    3:       end     [  2 compl,   1 exec,   0 rem of   3]   (6s)    91
Job    1:       end     [  3 compl,   0 exec,   0 rem of   3]   (7s)    13
All 3 jobs completed successfully. The average execution time was 6.700 ms.
----------------------------------- Outputs ------------------------------------
Enabled:        logExperiment, features, thumbnails
Disabled:       manifestExperiment, manifestJob
--------------------------------------------------------------------------------
Experiment metadata_12.41.23 completed (7s) writing to C:\Users\owen\AppData\Local\Temp\metadata_12.41.23" %}

{% include note.html content="This produces console messages **with** [execution-details](/user_guide.html#parallelization)." %}

Note in the console messages:
- the start / end events for each input.
- the name of the input is indicated on the right-hand side - and a job's total execution time.
- the output directory `C:\Users\owen\AppData\Local\Temp\metadata_12.41.23` is printed twice, at the start and end.

The following files are produced:

- `features.csv` where each row represents an input image, and each column an extracted feature.
- `experimentLog.txt` records the console output.
- the `thumbnails/` subdirectory, which contains a thumbnail for each row in the CSV file.
- **Only if an error occurs** (which it didn't!) then a job-specific log for `13_job_log.txt` etc.

The latter is useful for visualizing features alongside each other via derived embeddings etc. 

{% include tip.html content="The output directory can be changed with the [`-o` command-line option](/user_guide.html#outputs) e.g. `-o path_to_parent_directory`" %}

## Next steps

- After finding the right combination of `-i` parameters to find files, [tasks](/user_guide_tasks.html) ([predefined tasks](/user_guide_predefined_tasks.html) or via custom BeanXML) can be applied to these inputs. See other examples in this [Example Usage](/user_guide_examples.html) guide.

- The CSV files can be opened and visualized in *Excel*, *Python* ([pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)), [R](https://stat.ethz.ch/R-manual/R-devel/library/utils/html/read.table.html), [Spotfire](https://www.tibco.com/products/tibco-spotfire), [Ron's Editor](https://www.ronsplace.eu/products/ronseditor), and similar.

- The CSVs can be attached to images (as *multi-inputs*) for subsequent tasks in Anchor.

{% include links.html %}