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
- **a narrower range with a *wildcard*** (applied recursively if a double-wildcard): `-i foo*bar` or `-i **.jpg`
- **a different directory**: `-i path_to_directory`
- as *advanced usage*, **a file with [BeanXML](/user_guide_bean_xml.html)** describing inputs: `-i path_to_bean.xml`

{% include tip.html content="Wildcard implementations vary across shells e.g. [Windows PowerShell](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_wildcards?view=powershell-7.1), [Command Prompt](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/indexsrv/ms-dos-and-windows-wildcard-characters), [bash](https://linuxhint.com/bash_globbing_tutorial/), etc. **Placing the wildcard expression in double-quotes** can help solve problems by letting Anchor process the expression by its own rules: e.g. `-i \"foo*bar\"`" %}


## Extracting features from images

The previous commands gave an overview of the image files **collectively** en aggregate.

It can also be useful to generate summary information **for each image individually**.

The predefined task [feature/metadata](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/metadata.xml) will create a CSV file, where each row represents an image, and each column describes a feature e.g. image width, image height, number of channels etc.

{% include tip.html content="It also provides physical measurements in microns, if included in image metadata." %}

Example usage for `feature/metadata` can be found in [Extracting image features](http://localhost:4000/user_guide_examples_extracting_image_features.html#example-extracting-metadata-features).

{% include links.html %}