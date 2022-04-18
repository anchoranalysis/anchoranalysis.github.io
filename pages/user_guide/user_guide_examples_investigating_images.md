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

- **a file extension** not included in the [default search](https://github.com/anchoranalysis/anchor/blob/master/anchor-core/src/main/java/org/anchoranalysis/core/format/ImageFileFormat.java): `-i .zvi` *(recursively)*
- **a narrower range with a [wildcard](/user_guide_examples_investigating_images.html#filtering-with-wildcards)**: `-i foo*bar` *(non-recursively)* or `-i "**.jpg"` *(recursively)*
- **a different directory**: `-i path_to_directory`
- as *advanced usage*, **a file with [BeanXML](/user_guide_bean_xml.html)** describing inputs: `-i path_to_bean.xml`

#### Filtering with a file extension

When anchor sees a leading period (e.g. `-i .jpg`) it searches for the particular file extension *recursively*.

{% include tip.html content="This is often the <b>preferred search approach</b> due to inconsistent wildcard behavior (*see below!*)." %}


Multiple extensions may be searched for by including multiple `-i .someExtension` options, or combining with commas.

When combined, the leading period must only exist at the beginning, but it must exist - otherwise Anchor will mistake it as a path to a directory or BeanXML.

e.g. all of the following are valid (and equivalent!):

```bash
anchor -i .jpg,png,bmp			# search for either of the three extensions
anchor -i .jpg,png,.bmp
anchor -i ".jpg, png, .bmp"
anchor -i .jpg -i .png -i .bmp
```

#### Filtering with wildcards

Including wildcards `*` or `**` with the `-i` command-line option, adds a filter to the input files.

Where possible, Anchor treats a single wildcard `*` as a **non-recursive** filter, and a double wildcard `**`
as a **recursive** e.g.

```bash
-i foo*bar		# only files in the directory root
-i foo**bar		# also files in subdirectories
-i "foo**bar"		# also files in subdirectories
```

However, behavior varies significantly across operating-systems and [shells](https://en.wikipedia.org/wiki/Shell_(computing)), and this is not always possible.

Here follows a summary of behavior observed in different contexts

Shell | Operating System | Single wildcard | Double wildcard (unquoted) | Double wildcard (quoted) |
-----|-----|-----|-----|
[PowerShell](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_wildcards?view=powershell-7.1) | Windows | non-recursive | non-recursive | non-recursive |
[CMD](https://www.makeuseof.com/tag/a-beginners-guide-to-the-windows-command-line/) | Windows | non-recursive | non-recursive | recursive |
[Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) | Linux / MacOS | non-recursive | non-recursive | recursive |
-----|-----|-----|-----|-----|


## Extracting features from images

The previous commands gave an overview of the image files **collectively** en aggregate.

It can also be useful to generate summary information **for each image individually**.

The predefined task [feature/metadata](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/metadata.xml) will create a CSV file, where each row represents an image, and each column describes a feature e.g. image width, image height, number of channels etc.

{% include tip.html content="It also provides physical measurements in microns, if included in image metadata." %}

Example usage for `feature/metadata` can be found in [extracting image features](/user_guide_examples_extracting_image_features.html#example-extracting-metadata-features).

Here follows an *example `features.csv`* from a random-sample of the [fruits dataset](/user_guide_examples_montage.html#example---fruits):

<img alt="screenshot of example features.csv" src="/images/examples/investigatingImages/csv_metadata.jpg" class="screenshotExample"/>

{% include links.html %}