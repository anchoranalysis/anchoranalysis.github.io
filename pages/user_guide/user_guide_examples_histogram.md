---
title: "Examples - Histogram of pixel intensities"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_histogram.html
folder: user_guide
---

## Inputs

Consider an [example album](/downloads/examples/alps.zip), with three JPEGs. Running the command from e.g. `D:\Users\owen\Pictures\SomeAlbum`:

```
$ anchor
Searching recursively for image files. CTRL+C cancels.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> with uniform extension = jpg
-> file-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\alps-${0}.jpg
${0} = 3 unique integers between 13 and 91 inclusive
```

Anchor has found 3 images in this directory (searching recursively for known image types).

It also found a pattern among the paths, from which each input infers a **name** (`78`, `91` and `13`), as seen with `-t list`:

```
$ anchor -t list
78       -> D:\Users\owen\Pictures\SomeAlbum\alps-78.jpg
91       -> D:\Users\owen\Pictures\SomeAlbum\alps-91.jpg
13       -> D:\Users\owen\Pictures\SomeAlbum\alps-13.jpg
```

{% include tip.html content="This produces output **without** execution-details" %}

Now let's generate some more detailed summarization of the images (width, height, channels, bit depth etc.):

```
$ anchor -t summarize
Found 3 inputs.
-> with uniform extension = jpg
-> with diverse sizes: 5148x2992(1) 4846x3888(1) 5184x3888(1)
-> with uniform channel = 3
-> with uniform bit depth = 8
-> file-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\alps-${0}.jpg
${0} = 3 unique integers between 13 and 91 inclusive
```

## Task

Then let's generate histograms:

{% include tip.html content="This produces output **with** execution-details" %}

```
$ anchor -t histogram -o ..
Experiment histogram_01.05.25 started writing to D:\Users\owen\Pictures\histogram_01.05.25
Using 7 processors from: 8
Job    2:       start   [  0 compl,   3 exec,   0 rem of   3]           78
Job    1:       start   [  0 compl,   3 exec,   0 rem of   3]           13
Job    3:       start   [  0 compl,   3 exec,   0 rem of   3]           91
Job    2:       end     [  1 compl,   2 exec,   0 rem of   3]   (1s)    78
Job    3:       end     [  2 compl,   1 exec,   0 rem of   3]   (1s)    91
Job    1:       end     [  3 compl,   0 exec,   0 rem of   3]   (1s)    13
Writing 3 grouped histograms into D:\Users\owen\Pictures\histogram_01.05.25\grouped
All 3 jobs completed successfully. The average execution time was 1.689 ms.
Experiment histogram_01.05.25 completed (1s) writing to D:\Users\owen\Pictures\histogram_01.05.25
```

Note the complex output with execution details printed on incremental lines as the three inputs are executed.
- Each time a job (for an input) `start`s or `end`s, an event line is printed, and with an updated overall status.
- On the right-side, the name of the input is indicated - and a job's execution time at the `end`.
- The output directory `D:\Users\owen\Pictures\histogram_01.05.25` is printed to the console at the start and end. It was calculated relative to the current working directory with `-o ..` and from the task and time.

By default, it will never replace an existing directory. If unspecified, a system temporary directory is used.

## Outputs

```
13_blue.csv   78_blue.csv   91_blue.csv   experiment_log.txt
13_green.csv  78_green.csv  91_green.csv  grouped/
13_red.csv    78_red.csv    91_red.csv
```

Many files have been created in the output directory:

- A histogram CSV for each channel of each image (`red`, `green`, `blue`).
- The output seen in the console is also logged to the file system in `experiment_log.txt`.
- Similar output for specific tasks would be saved in `91_job_log.txt` etc. **only if an error occurs**, which it didn't.
- A subdirectory exists `grouped/` with aggregated histograms across all images.

{% include links.html %}