---
title: "Example Usage - Histogram of pixel intensities"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_histogram.html
folder: user_guide
---

## Inputs

<img alt="inputs in windows explorer" src="/images/examples/histogram/inputs_windows_explorer.jpg" class="screenshot"/>

Consider an [example album](/downloads/examples/alps.zip) with three images. Running the command from e.g. `D:\Users\owen\Pictures\SomeAlbum`:

<pre>
$ <b>anchor</b>
Searching recursively for image files. CTRL+C cancels.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> with uniform extension = jpg
-> file-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\alps-${0}.jpg
${0} = 3 unique integers between 13 and 91 inclusive
</pre>

Anchor has found 3 images in this directory (searching recursively for known image types).

It also found a pattern among the paths, from which each input infers a **name** (`78`, `91` and `13`), as seen with `-t list`:

<pre>
$ <b>anchor -t list</b>
78       -> D:\Users\owen\Pictures\SomeAlbum\alps-78.jpg
91       -> D:\Users\owen\Pictures\SomeAlbum\alps-91.jpg
13       -> D:\Users\owen\Pictures\SomeAlbum\alps-13.jpg
</pre>

{% include tip.html content="This produces output **without** execution-details" %}

Now let's generate some more detailed summarization of the images (width, height, channels, bit depth etc.):

<pre>
$ <b>anchor -t summarize</b>
Found 3 inputs.
-> with uniform extension = jpg
-> with diverse sizes: 5148x2992(1) 4846x3888(1) 5184x3888(1)
-> with uniform channel = 3
-> with uniform bit depth = 8
-> file-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\alps-${0}.jpg
${0} = 3 unique integers between 13 and 91 inclusive
</pre>

## Task

Then let's generate histograms:

{% include tip.html content="This produces output **with** execution-details" %}

<pre>
$ <b>anchor -t histogram -o ..</b>
Experiment histogram_14.09.48 started writing to D:\Users\owen\Pictures\histogram_14.09.48
Using 7 processors from: 8
Job    2:       start   [  0 compl,   3 exec,   0 rem of   3]           78
Job    1:       start   [  0 compl,   3 exec,   0 rem of   3]           13
Job    3:       start   [  0 compl,   3 exec,   0 rem of   3]           91
Job    2:       end     [  1 compl,   2 exec,   0 rem of   3]   (1s)    78
Job    3:       end     [  2 compl,   1 exec,   0 rem of   3]   (1s)    91
Job    1:       end     [  3 compl,   0 exec,   0 rem of   3]   (1s)    13
Writing 3 grouped histograms into D:\Users\owen\Pictures\histogram_14.09.48\grouped
All 3 jobs completed successfully. The average execution time was 1.689 ms.
Experiment histogram_01.05.25 completed (1s) writing to D:\Users\owen\Pictures\histogram_14.09.48
</pre>

Note:
- the start/end events for each input.
- the name of the input is indicated on the right-hand side - and a job's total execution time.
- the output directory `D:\Users\owen\Pictures\histogram_14.09.48` is printed twice.

The output directory was calculated relative to the current working directory with `-o ..` and from the task and time.

## Outputs

<img alt="outputs in windows explorer" src="/images/examples/histogram/outputs_windows_explorer.jpg" class="screenshot"/>

Many files have been created in the output directory:

- A **histogram CSV** for each channel of each image (`13_red.csv`, `13_green.csv`, `13_blue.csv` etc.).
- A subdirectory `grouped/` with aggregated histograms across all images.
- `experiment_log.txt` recording the execution details (identical to the console output).
- **Only if an error occurs** (which it didn't!) then a job-specific log for `13_job_log.txt` etc.


## Next steps

Possibilities:
- The CSV files can be opened and visualized in *Excel*, *Python* ([pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)), [R](https://stat.ethz.ch/R-manual/R-devel/library/utils/html/read.table.html), [Spotfire](https://www.tibco.com/products/tibco-spotfire), [Ron's Editor](https://www.ronsplace.eu/products/ronseditor), and similar.
- The histograms can be attached to images (as *multi-inputs*) for subsequent tasks in Anchor.
- Thresholds or color models can be calculated from the CSVs (e.g. using the `grouped/` aggregates for robustness).
    - Consider [Otsu's method](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-image/src/main/java/org/anchoranalysis/plugin/image/bean/threshold/calculatelevel/Otsu.java) or anchor's [Weighted Otsu](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-image/src/main/java/org/anchoranalysis/plugin/image/bean/threshold/calculatelevel/OtsuWeighted.java).

{% include links.html %}