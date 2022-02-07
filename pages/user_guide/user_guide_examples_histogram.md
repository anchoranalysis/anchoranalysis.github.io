---
title: "Example - Histograms from images"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_histogram.html
folder: user_guide
---

## Background

Image histograms describe the color (pixel intensity) content of an image.

Generating histograms can be a **useful first step for image exploration and understanding**.

The histograms can be used in subsequent processing steps for normalizing operations, either against the image's histogram itself, or against an *aggregated* histogram from many related images.

With **classical image processing**, popular thresholding algorithms like [Otsu's method](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-image/src/main/java/org/anchoranalysis/plugin/image/bean/histogram/threshold/Otsu.java) use the image histogram (or histograms derived from image subregions) to determine appropriate thresholds.

With **deep learning workflows**, data normalization is also a popular step e.g. [subtracting a mean intensity value](https://stats.stackexchange.com/questions/211436/why-normalize-images-by-subtracting-datasets-image-mean-instead-of-the-current) from image channels. Here, histograms help explore and calculate appropriate normalization, including sanity checks on content.

This tutorial proceeds to show how *Anchor* can **create histograms for each channel in an image**, and derive a **summed histogram** aggregated across many images.

## Inputs

<img alt="inputs in windows explorer" src="/images/examples/histogram/inputs_windows_explorer.jpg" class="screenshotExample"/>

Consider an [example album](/downloads/examples/alps.zip) with three images. Running the command from e.g. `D:\Users\owen\Pictures\SomeAlbum`:

{% include shell.html
command="anchor"
response="Searching recursively for image files. CTRL+C cancels.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> with uniform extension = jpg
-> file-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\alps-${0}.jpg
${0} = 3 unique integers between 13 and 91 inclusive" %}

Anchor has found 3 images in this directory, as described in [Investigating image files](/user_guide_examples_investigating_images.html), and inferred names (`78`, `91` and `13`).

{% include shell.html
command="anchor -t list"
response="78       -> D:\Users\owen\Pictures\SomeAlbum\alps-78.jpg
91       -> D:\Users\owen\Pictures\SomeAlbum\alps-91.jpg
13       -> D:\Users\owen\Pictures\SomeAlbum\alps-13.jpg" %}

{% include note.html content="This produces console messages **without** [execution-details](/user_guide.html#parallelization)." %}

## Task

Then let's generate histograms:

{% include shell.html
command="anchor -t histogram -o .."
response="Experiment histogram_12.52.22 started writing to C:\Users\owen\Desktop\histogram_12.52.22
------------------------------------ Inputs ------------------------------------
The job has 3 inputs.

They are named with the pattern: ${0}
${0} = 3 unique integers between 13 and 91 inclusive
---------------------------------- Processing ----------------------------------
Preparing jobs to run with common initialization.
Using 7 processors CPUs from 8, and if needed and if possible, up to 0 simultaneous jobs using a GPU.
Job    1:       start   [  0 compl,   3 exec,   0 rem of   3]           13
Job    2:       start   [  0 compl,   3 exec,   0 rem of   3]           78
Job    3:       start   [  0 compl,   3 exec,   0 rem of   3]           91
Job    2:       end     [  1 compl,   2 exec,   0 rem of   3]   (5s)    78
Job    3:       end     [  2 compl,   1 exec,   0 rem of   3]   (6s)    91
Job    1:       end     [  3 compl,   0 exec,   0 rem of   3]   (7s)    13
All 3 jobs completed successfully. The average execution time was 6.628 ms.
----------------------------------- Outputs ------------------------------------
Enabled:        channels, logExperiment, sum
|- channels     blue, green, red
Disabled:       manifestExperiment, manifestJob
--------------------------------------------------------------------------------" %}

{% include note.html content="This produces console messages **with** [execution-details](/user_guide.html#parallelization)." %}

Consider:
- the start / end events for each input.
- the name of the input is indicated on the right-hand side - and a job's total execution time.
- the output directory `C:\Users\owen\Desktop\histogram_12.52.22` is printed twice, at the start and end.

The output directory was calculated relative to the current working directory with `-o ..` and from the task and time.

## Outputs

<img alt="outputs in windows explorer" src="/images/examples/histogram/outputs_windows_explorer.jpg" class="screenshotExample"/>

Many files have been created in the output directory:

- A **histogram CSV** for each channel of each image (`13_red.csv`, `13_green.csv`, `13_blue.csv` etc.).
- A subdirectory `sum/` with aggregated histograms across **all** images.
- `experimentLog.txt` records the console output.
- **Only if an error occurs** (which it didn't!) then a job-specific log for `13_job_log.txt` etc.

## Grouping

The tasks above created a histogram for each image, and a summation of all images (in the `sum/` subdirectory).

Instead of *all* images, separate summations can be produced for each group of inputs. Groups are derived from the input identifiers using the [`-pg` command-line option](/user_guide_command_line.html#grouping):

```bash
anchor -t histogram -pg 0		# to group by the first identifier element (directory).
anchor -t histogram -pg 0:-2		# to group by all elements, except the last.
```


## Next steps

- The [`histogram_plot.py`](/developer_guide_repositories_anchor_python_visualization.html#entry-point-scripts) script will plot the produced CSV file as a histogram.
- The CSV histogram files can be opened and processed in *Excel*, *Python* ([pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)), [R](https://stat.ethz.ch/R-manual/R-devel/library/utils/html/read.table.html), [Spotfire](https://www.tibco.com/products/tibco-spotfire), [Ron's Editor](https://www.ronsplace.eu/products/ronseditor), and similar.
- The histograms can be attached to images (as *multi-inputs*) for subsequent tasks in Anchor.
- Thresholds or color models can be calculated from the CSVs (e.g. using the `grouped/` aggregates for robustness).
    - Consider [Otsu's method](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-image/src/main/java/org/anchoranalysis/plugin/image/bean/histogram/threshold/Otsu.java) or [Weighted Otsu](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-image/src/main/java/org/anchoranalysis/plugin/image/bean/histogram/threshold/OtsuWeighted.java).

{% include links.html %}