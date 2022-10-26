---
title: "Example - Resizing images"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_resizing_images.html
folder: user_guide
---

## Resizing images

To resize an image, use the predefined task [resize](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/resize.xml).

**By default, images are resized to 1280x768** (*width* x *height*). 

```bash
anchor -t resize
```

We usually instead specify a different target size with the [`-ps` command-line option](/user_guide_command_line.html#task-options) which offers multiple possibilities.

{% include note.html content="For simplicity, the following examples omit the [`-i` command-line option](user_guide_command_line.html#input-options) (therefore reading images from the current directory) and the [`-o` command-line option](/user_guide.html#outputs) (therefore outputting into a temporary directory)." %}

{% include tip.html content="See [changing output options](http://localhost:4000/user_guide_examples_changing_output_options.html) for useful
tips on how to change the output image format or naming." %}

### Resizing with a scaling factor 

To resize to ***half* the existing width and height**:

```bash
anchor -t resize -ps 0.5
```

To resize to ***double* the existing width and height**:

```bash
anchor -t resize -ps 2
```

### Resizing to a specific width and height 

To resize to **specifically *1024x768*** (*width* x *height*), breaking aspect ratio if necessary.

```bash
anchor -t resize -ps 1024x768
```

### Resizing preserving aspect ratio

To resize to ***800* pixels width, preserving existing aspect ratio**.

```bash
anchor -t resize -ps 800x
```

To resize to ***600* pixels height, preserving existing aspect ratio**.

```bash
anchor -t resize -ps x600
```

To resize to **the maximal-size possible, preserving existing aspect ratio, that fits inside 1000x900**.

```bash
anchor -t resize -ps 1000x900+
```

### Resizing to preserve file-names and any non-image files

The following command ***immutably* resizes images from a source directory into a destination directory**, preserving filenames, directory-structure and any adjacent non-image files. 

```bash
anchor -i c:\foo\source\ -ip -ic -t resize -ps 250x350 -oo c:\bar\destination\
```

{% include tip.html content="See [command line](http://localhost:4000/user_guide_command_line.html) for a summary of each command-line option, and [more detailed explanation](http://localhost:4000/user_guide_examples_changing_output_options.html)." %}


## Resizing with a common-size across all images

The `center` task will resize, in a similar way to above accepting an identical `-ps` argument, but ensure all outputted images have identical size.

Where necessary, it will achieve this by adding padding (with black color i.e. intensity value 0) around the resized image, centering it in the larger image.

```bash
# Resizes every image to 400 pixels width, while preserving aspect ratio, and centering vertically.
anchor -t center -ps 400x

# Resizes every image to 300 pixels height, while preserving aspect ratio, and centering horizontally.
anchor -t center -ps x300

# Preserves aspect ratio, and makes sure an image is never greater than 1000x900, centering horizontally and vertically.
anchor -t center -ps 1000x900+

# Resizes every image to half its existing size, taking the maximum size in each dimension as a common size in which any smaller images are centered horizontally and vertically.
anchor -t center -ps 0.5
```

{% include links.html %}