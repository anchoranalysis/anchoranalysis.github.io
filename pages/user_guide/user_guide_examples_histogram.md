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
Searching for inputs as per default experiment. CTRL+C cancels.
Learn how to select inputs, outputs and tasks with 'anchor -h'.

Found 3 inputs.
-> with uniform extension = jpg
-> file-sizes range across [1 MB to 7 MB] with an average of 4 MB.
-> D:\Users\owen\Pictures\SomeAlbum\${0}.jpg
${0} = "mar" (1) | "jan" (1) | "feb" (1)
```

Anchor has found 3 images in this directory (searching recursively for known image types).

It also found a pattern among the paths, which is used to extract a **name** for each input (`jan`, `feb` and `mar`), as seen with the `list` task:

```
$ anchor -t list
jan      -> D:\Users\owen\Pictures\SomeAlbum\jan.jpg
mar      -> D:\Users\owen\Pictures\SomeAlbum\mar.jpg
feb      -> D:\Users\owen\Pictures\SomeAlbum\feb.jpg
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
-> D:\Users\owen\Pictures\SomeAlbum\${0}.jpg
${0} = "mar" (1) | "jan" (1) | "feb" (1)
```

## Task

Then let's generate histograms:

{% include tip.html content="This produces output **with** execution-details" %}

```
$ anchor -t histogram -o ..
Experiment histogram_2020.03.01 started writing to D:\Users\owen\Pictures\histogram_2020.03.01
Using 7 processors from: 8
Job    2:       start   [  0 compl,   3 exec,   0 rem of   3]           jan
Job    1:       start   [  0 compl,   3 exec,   0 rem of   3]           feb
Job    3:       start   [  0 compl,   3 exec,   0 rem of   3]           mar
Job    2:       end     [  1 compl,   2 exec,   0 rem of   3]   (1s)    jan
Job    3:       end     [  2 compl,   1 exec,   0 rem of   3]   (1s)    mar
Job    1:       end     [  3 compl,   0 exec,   0 rem of   3]   (1s)    feb
Writing 3 grouped histograms into D:\Users\owen\Pictures\histogram_2020.03.01\grouped
All 3 jobs completed successfully. The average execution time was 1.789 ms.
Experiment histogram_2020.03.01 completed (1s) writing to D:\Users\owen\Pictures\histogram_2020.03.01
```

Note the complex output with execution details printed on incremental lines as the three inputs are executed.
- Each time a job (for an input) starts or ends, an event line is printed, and with an updated overall status.
- On the right-side, the name of the input is indicated (as well as the job execution-time for `end` events).
- The output directory `D:\Users\owen\Pictures\histogram_2020.03.01.04.28` is printed to the console at the start of the experiment. It was calculated relative to the current working directory with `-o ..`

## Outputs

```
experiment_log.txt  feb_red.csv   jan_green.csv  mar_green.csv
feb_blue.csv        grouped/      jan_red.csv    mar_red.csv
feb_green.csv       jan_blue.csv  mar_blue.csv
```

Many files have been created in the output directory:

- A histogram CSV for each channel of each image (`red`, `green`, `blue`).
- The output seen in the console is also logged to the file system in `experiment_log.txt`.
- Similar output for specific tasks would be saved in `feb_job_log.txt` etc. **only if an error occurs**, which it didn't.
- A subdirectory exists `grouped/` with aggregated histograms across all images.

{% include links.html %}