---
title: "Example - Converting and manipulating images"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_converting_manipulating_images.html
folder: user_guide
---

## Background

Some image processing operations are a simple function of a single image: **one image *in*, one image *out***.

*Anchor* can run these operations easily on a nested-directories of many images, supporting certain outcomes:

- Parallelizing operations among available CPU cores.
- Preserving the directory structure, naming output files identically to the input.
- Copying non-image files (metadata etc.) that may also exist alongside the images.
- Changing image format.
- Logging errors that may occur with particular images.

This guide introduces certain [predefined tasks](/user_guide_predefined_tasks.html) and command-line options to support these workflows. 

## Command line options

Various command-line options support the [predefined tasks](#predefined-tasks), introduced first here, followed by usage examples afterwards.

### Specifying image format

Anchor uses context-sensitive [rules](/user_guide_supported_formats.html#writing-images) to determine which file-format to write an image as.

The [rules](/user_guide_supported_formats.html#writing-images) are configurable in the [defaultBeans.xml](/user_guide_supported_formats.html#specifying-default-readers-and-writers) configuration file, in the `StackWriter` section.

These rules exist as **no one format is ideal for all circumstances**. Certain types of images (3D, multi-channel etc.) are unsupported by, or better suited to particular formats. Anchor tries to pick smartly, by default.

Nevertheless, for certain standard image-types (2D, RGB or grayscale images), there's a variety of available formats, and **a particular format can be requested by the command-line option** [`-of`](/user_guide_command_line.html#output-options).

```shell
-of png
-of jpg
-of jpeg
-of tif
-of tiff
-of png
-of bmp
-of ome.xml
-of ome.tif
```

If a particular requested format is unsupported by the image-type, *Anchor* will prefer to quietly use the format  proposed by the rules before throwing an error message.

This [`-of` command-line option](/user_guide_command_line.html#output-options) can be used for *any* image producing task.

### Additionally copying non-input files 

Given an input directory, typically *Anchor* will create an output directory with *n* files derived from each input. For all examples on this page, a single input is created (*n==1*), and as a special case, the output is assigned the same as the input-name.

Using the [`-ir`](/user_guide_examples_investigating_images.html#changing-the-derived-input-name) command-line option, the input-name is identical to the file-name (and any subdirectories). As a whole, the task ***immutably* transforms images** from one directory to another, preserving file-names and subdirectory-structure.

e.g. `input_directory/foo/file12.png` produces `output_directory/foo/file12.ext`. 

{% include tip.html content="The input directory will **never** be altered. By default, *Anchor* refuses to write into an existing output-directory, and names output-directories with a timestamp to reduce chances of unintended overwriting." %}

Sometimes files exist alongside images in the input directory that we also wish to copy to the output directory (metadata files etc.). They should not be inputs, as they will not be processed, just copied unchanged.

The [`-ic` command-line option](/user_guide_command_line.html#input-options) achieves this by **additionally** copying all files that are ***not* considered inputs** in the input directory to the output directory.

e.g. `input_directory/foo/file12.txt` (ignored as an input, being not an image file) is copied to `output_directory/foo/file12.txt`

### Writing outputs as a sequence

The [`-on` command-line option](/user_guide_command_line.html#output-options) will write each output as a sequence of increasing integers (beginning at 0).

This can be useful for software that expects images as a sequence, e.g. `image_0000.tif`, `image_0001.tif`, `image_0002.tif`, etc. like is needed in the creating [video from images](/user_guide_examples_video_from_images.html) tutorial.

{% include tip.html content="[`-on`](/user_guide_command_line.html#output-options) can be used for the outputs from *any* task." %}

### Suppressing directory structure

The [`-os` command-line option](/user_guide_command_line.html#output-options) will replace any directory separators (i.e. the `/`) in the output-names with an underscore.

This **eliminates any subdirectory hierarchy** e.g.

`path_to_output_directory/foo/bar/output.png` becomes instead `path_to_output_directory/foo_bar_output.png`

{% include tip.html content="[`-os`](/user_guide_command_line.html#output-options) can be used for the outputs from *any* task." %}

## Predefined tasks

### Converting images to a different file format

Imagine that our current working-directory contains [three JPEGs](/downloads/examples/alps.zip): `alps-13.jpg` `alps-78.jpg` and `alps-91.jpg`.

The pre-defined task [convert](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/convert.xml) will convert images to the format specified by the [`-of` command-line argument](#specifying-image-format).

```none
anchor -t convert -of png -o C:\Users\owen\Desktop
```

This produces the following files in `C:\Users\owen\Desktop\convert_20.31.08`: `13.png` `78.png` and `91.png`

{% include note.html content="If the [`-of` command-line argument](#specifying-image-format) is omitted, the default rules are applied to determine the format. This may be different from the existing file format of the input file." %}

#### Perserving the image file-name

To similarly convert but **keep the *full* image file-name preserved**:

```none
anchor -ir -t convert -of png -o C:\Users\owen\Desktop
```

This produces instead: `alps-13.png` `alps-78.png` and `alps-91.png`.  

#### Outputting to a specific output-directory (avoiding creating a subdirectory)

Note how the output-directory becomes a newly created directory `convert_20.31.08` of what is passed to the `-o` option.

{% include note.html content="The newly-created subdirectory's name includes a timestamp, so an unchanged command can be **repeatedly and safely called** to produce outputs **in different directories**. Useful perhaps when changing parameters or debugging." %}

However, the behavior isn't always desired, and the [`-oo` command-line option](/user_guide_command_line.html#output-options) will disable it, letting the output directory be specified directly with `-o`. 

```none
anchor -t convert -of png -o C:\Users\owen\Desktop\desired_output_directory\ -oo
```

This creates the `C:\Users\owen\Desktop\desired_output_directory\` directory, and outputs to it.

As a protection mechanism, **if the directory already exists, it will exit with an error**. The existing directory must be deleted or moved, before re-executing the command.

#### Preserving image file-names and any non-image-files

This command will convert images from a source directory to a target directory, while preserving file-names and subdirectory-structure **and** [any other non-image files](/user_guide_examples_converting_manipulating_images.html#additionally-copying-non-input-files) in the directory.

```none
anchor -i c:\foo\source\ -ir -ic -t convert -of png -o c:\bar\destination\ -oo
```

### Resizing images

To resize an image, use the predefined task [resize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/resize.xml).

{% include tip.html content="The previously-described command-line options can *all* be applied, including to change the outputted file format." %}

**By default, images are resized to 1280x768** (*width* x *height*). 

```none
anchor -t resize
```

We usually instead specify a different target size with the [`-ps` command-line option](/user_guide_command_line.html#task-options) which offers multiple possibilities.

For simplicity, the following examples omit the [`-i` command-line option](user_guide_command_line.html#input-options) (therefore reading images from the current directory) and the [`-o` command-line option](/user_guide.html#outputs) (therefore outputting into a temporary directory).

#### Resizing with a scaling factor 

To resize to ***half* the existing width and height**:

```none
anchor -t resize -ps 0.5
```

To resize to ***double* the existing width and height**:

```none
anchor -t resize -ps 2
```

#### Resizing to a specific width and height 

To resize to **specifically *1024x768*** (*width* x *height*), breaking aspect ratio if necessary.

```none
anchor -t resize -ps 1024x768
```

#### Resizing preserving aspect ratio

To resize to ***800* pixels width, preserving existing aspect ratio**.

```none
anchor -t resize -ps 800x
```

To resize to ***600* pixels height, preserving existing aspect ratio**.

```none
anchor -t resize -ps 1024x
```

To resize to **the maximal-size possible, preserving existing aspect ratio, that fits inside 1000x900**.

```none
anchor -t resize -ps 1000x900+
```

#### Resizing to preserve file-names and any non-image files

Like [previously for image format conversion](/user_guide_examples_converting_manipulating_images.html#preserving-image-file-names-and-any-non-image-files), we can include extra command-line options to build advanced operations.

The following command ***immutably* resizes images from a source directory into a destination directory**, preserving filenames, directory-structure and any adjacent non-image files. 

```none
anchor -i c:\foo\source\ -ir -ic -t resize -ps 250x350 -o c:\bar\destination\ -oo
```

### Copying images

To copy images, use the predefined task [copy](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/copy.xml).

By default, it will find image files, and copy them to the output-directory, using the varying parts of the filenames.

```none
anchor -i c:\foo\source\ -t copy -o c:\bar\destination\ -oo
```

#### Preserving file-names

To **preserve file-names**, the [`-ir` command-line option](/user_guide_command_line.html#input-options) is added.

```none
anchor -i c:\foo\source\ -ir -t copy -o c:\bar\destination\ -oo
```

This also preserves subdirectory hierarchy.

#### Suppressing subdirectory hierarchy

To **preserve file-names but suppress subdirectory hierarchy**, the [`-os` command-line option](/user_guide_examples_converting_manipulating_images.html#suppressing-directory-structure) is added.

```none
anchor -i c:\foo\source\ -ir -t copy -o c:\bar\destination\ -oo -os
```

{% include note.html content="The `copy` task executes more quickly than `convert`, copying files bytewise rather than loading as images. If the [-of command-line option](/user_guide_examples_converting_manipulating_images.html#specifying-image-format) is selected to request a different output format, then `copy` behaves instead like `convert`." %}

## Adjusting number of parallel CPU cores

By default, Anchor uses all available CPU cores (except one) to execute operations in parallel.

Sometimes, there is insufficient available memory to facilitate so much parallelism, especially if a computer has a very large number of processors, and *out-of-memory* errors appear in the logs.

The [-tp command-line option](/user_guide_command_line.html#task-options) species an explicit maximum on the number of parallel cores to use. 

To allow **no more than 4 cores in parallel**:

```none
anchor -t resize -tp 4
```

{% include tip.html content="One may experiment with different `-tp` values to find an appropriate number that doesn't result in memory errors." %}



{% include links.html %}