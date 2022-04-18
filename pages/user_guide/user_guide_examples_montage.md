---
title: "Example - Creating a photomontage"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_montage.html
folder: user_guide
---

## Background

A [photomontage](https://en.wikipedia.org/wiki/Photomontage) (or *montage* or *collage*) is a visualization where images are tiled side-by-side. They offer:

- An **effective overview** of a set of images
- A **direct side-by-side comparison** of images.
- An attractive **summary to present to others**.

### Predefined-tasks for montages

Anchor can efficiently and easily build montages of a large number of images via three [predefined tasks](/user_guide_predefined_tasks.html):

| Task | Description |
| ---- | ----------- |
| `montage` | changes the number of images per row [to balance available space](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/montage/balance.xml). |
| `montage/balance` | equivalent to above. |
| `montage/table` | imposes a [table structure](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/montage/table.xml), resizing only within aligned cells. |
| `montage/slices` | montages all [z-slices in a 3D image](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/montage/slices.xml). |
| ---- | ----------- |

Apart from with `montage/balance`, the bottom-row exception exceptionally may not be fully filled.

Resizing only occurs, while preserving an image's [aspect-ratio](https://en.wikipedia.org/wiki/Aspect_ratio_(image)).

Each task always tries to arrange with a similar number of rows and columns (to be approximately square).

## Example - fruits

### Dataset

The [Fruits-360](https://github.com/antonnifo/fruits-360) dataset (from *Horea Muresan* and *Mihai Oltean*) contains a large number of images of fruits.

We will work from the `Training/` sub-directory, which contains 67,692 images.

{% include shell.html
command="anchor -t summarize"
response="Found 67692 inputs.
-> with uniform extension = jpg
-> with uniform size = 100x100
-> with uniform channel = 3
-> with uniform bit depth = 8
-> file-sizes range across [2 KB to 7 KB] with an average of 4 KB.
-> ${0}\${1}_100
${0} = 131 unique strings e.g. \"Grape Blue\" (984), \"Plum 3\" (900)
${1} = 1717 unique strings e.g. \"14\" (115), \"r_134\" (112), \"r_125\" (112)" %}

All images have **identical size** and bit-depth (but this isn't a prerequisite for our tasks)." %}

Note also the **pattern in the file-paths**: `fruit_name`/`id`_`100`

This pattern will determine the identifiers and labels for each image.

### Filling all available space

As that's too many images to include in a single montage, let's change into a subdirectory containing 490 inputs. Then create montage:

```bash
cd Pineapple
anchor -t montage -of jpg
```

We output as a JPEG (instead of the PNG default) using the `-of` [command-line-option](/user_guide_command_line.html#output-options).

<img alt="unshuffled montage of pineapples" src="/images/examples/montage/pineapples_unshuffled.jpg" class="screenshotExample"/>

### Randomizing image order (shuffling)

To randomize the image order, we add the `-is` [command-line-option](/user_guide_command_line.html#input-options).

```bash
anchor -is -t montage -of jpg
```

<img alt="shuffled montage of pineapples" src="/images/examples/montage/pineapples_shuffled.jpg" class="screenshotExample"/>

### Sampling images

To take a random sample, we additionally add the `-ir` [command-line-option](/user_guide_command_line.html#input-options).

Let's randomly sample 120 images from the entire dataset (not <i>just</i> pineapples!) for the montage.

```bash
cd ..
anchor -ir 120 -t montage -of jpg
```

<img alt="labelled montage of a random sample" src="/images/examples/montage/smaller_sample_labelled.jpg" class="screenshotExample"/>

### Removing labels

The montage tasks may produce two outputs `labelled` (activated by default) and `unlabelled` (unactivated by default), as displayed
at the end of the task output.

{% include shellResponseOnly.html
response="All 120 jobs completed successfully. The average execution time was 0.007 s.
----------------------------------- Outputs ------------------------------------
Enabled:        labelled, logExperiment
Disabled:       executionTime, unlabelled
--------------------------------------------------------------------------------
Experiment montage_14.11.55 completed (8s) writing to C:\Users\owen\AppData\Local\Temp\montage_14.11.55" %}

All images have the same size and bit-depth (but this isn't a prerequisite for our tasks)." %}


Labels are present in the former, and omitted in the latter.

To produce an unlabelled version only, use the `-oe` and `-od` [command-line-option](/user_guide_command_line.html#output-options):

```bash
anchor -ir 120 -t montage -of jpg -oe unlabelled -od labelled
```

<img alt="unlabelled montage of a random sample" src="/images/examples/montage/smaller_sample_unlabelled.jpg" class="screenshotExample"/>


### Specifying the size

A sensible default-size is chosen for the montaged image (scaling down the input images).

The user may specify a custom size with the `-ps` [command-line-option](/user_guide_command_line.html#task-options):

- `-ps 0.1` to scale the images to approximately `10%` of their original size in the montage.
- `-ps 2000x` to produce a montage that has exactly 2000 pixels width.

{% include warning.html content="Although the `-ps` option supports additional options for other tasks, but they unsupported when making a montage." %}

Let's create a much larger sample of very small images (scaled to `30%` of their original size).

```bash
anchor -ir 1000 -t montage -of jpg -oe unlabelled -od labelled -ps 0.3
```

<img alt="unlabelled montage of a larger random sample" src="/images/examples/montage/larger_sample_unlabelled.jpg" class="screenshotExample"/>

## Example - sports time-series

### Dataset

The previous dataset had images of constant-size. Let's try now with a dataset where:

- the images vary in size.
- the images are meaningfully ordered, as successive time-frames.

The images come from the [UCF101 video classification dataset](https://www.crcv.ucf.edu/data/UCF101.php), downloaded from [Kaggle](https://www.kaggle.com/ashuguptahere/video-classification-ucf101), but let's initially focus only on the initial 20 images (of kayaking) by appending `-il 20`. We've manipulated their sizes by cropping.

### Balancing the number of images per row

Let's make a montage, where the number of images per row is allowed vary, to try and keep the height of each row approximately uniform. This occurs via the `montage` (i.e. `montage/balance`) predefined task.

```bash
anchor -il 20 -t montage -of jpg
```

Note the image arrangement: rows with more `landscape` contain fewer images, and those with more `portrait` contain more.

The black background is part of the images, and was not introduced by the algorithm.

<img alt="first 20 sports images with balancing" src="/images/examples/montage/sporting_first_balanced.jpg" class="screenshotExample"/>


### Table structure

Let's now try a tabular structure, that inists on an identical number of images per row (apart from the last row).

```bash
anchor -il 20 -t montage/table -of jpg
```

<img alt="first 20 sports images with balancing" src="/images/examples/montage/sporting_first_table.jpg" class="screenshotExample"/>


### Sampling the entire dataset

Let's take a random sample of `0.2%` of the entire dataset, and to have `1800 pixels` width.

```bash
anchor -ir 0.002 -t montage -of jpg -ps 1800x
```

<img alt="random sample of all sports images" src="/images/examples/montage/sports_random_sample.jpg" class="screenshotExample"/>

{% include links.html %}