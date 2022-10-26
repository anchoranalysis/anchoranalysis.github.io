---
title: "Example - Video from images"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_video_from_images.html
folder: user_guide
---

## Background

It is often convenient to display a set of images as a video, to quickly view a large set of images, to embed in a presentation, or otherwise communicate. A set of images may have a natural order, or be better viewed randomly.

This guide illustrates how to create a video from a directory of images using the open-source command-line tool [ffmpeg](https://www.ffmpeg.org/), with preprocessing steps via *Anchor*.

`ffmpeg` has [particular requirements](https://trac.ffmpeg.org/wiki/Slideshow) to convert images to a video:

- Image filenames **contain an integer sequence** (zero padded) e.g. `img001.png`, `img002.png`, `img003.png`, etc. 
- Images are 2D.
- Images have **identical width, height and bit-rate**.

If these conditions are already true, no preprocessing is needed, and one can skip to the [final section](/user_guide_examples_video_from_images.html#creating-the-video-with-ffmpeg) of the tutorial.

Otherwise, *Anchor* can be used to transform the images accordingly.

## Preprocessing

### Outputting the image sequence

The [`-on` command-line option](/user_guide_examples_converting_manipulating_images.html#writing-outputs-as-a-sequence) will ensure all files are outputted in a sequence.

To write images in a **automatically-created subdirectory of a parent**:

```bash
anchor -i path_to_input_directory/ -t copy -o path_to_parent_output_directory/ -on
```

To write images in a **newly-created specific output directory**:

```bash
anchor -i path_to_input_directory/ -t copy -oo path_to_specific_output_directory/ -on
```

### Randomizing the image order

To add *randomized* order to images, add the [`-is` command-line option](/user_guide_command_line.html#input-options) to **shuffle the inputs**.

```bash
anchor -i path_to_input_directory/ -is -t copy -oo path_to_specific_output_directory/ -on
```

### Images with different sizes

With images of varying sizes, use the `resize` [predefined task](/user_guide_predefined_tasks.html) instead of `copy`, [setting the desired size with the -ps option](/user_guide_examples_converting_manipulating_images.html#resizing-images).

```bash
anchor -i path_to_input_directory/ -t center -ps 800x600 -oo path_to_specific_output_directory/ -on
```

## Creating the video with ffmpeg

### Installing ffmpeg

If not already installed:

1. Download [ffmpeg](https://www.ffmpeg.org/).
2. Unzip to a convenient location on the file-system.
3. Add `ffmpeg`'s `bin/` directory to the system `PATH` variable, so that it can be called on a shell as `ffmpeg`.

{% include tip.html content="See Anchor's [detailed installation instructions - step 3](/installation_detailed.html#3-set-up-environment-variables) for tips on how to change the `PATH` variable." %}


### Encoding the images as a video

Open a shell in the images directory. See [how to run a predefined task](/user_guide_predefined_tasks.html#how-to-run-a-predefined-task) for tips on how to do this.

Try `ffmpeg` with a command similar to the following:

```bash
ffmpeg -framerate 2 -i img%03d.png -c:v libx264 -vf fps=2 -pix_fmt yuv420p out.mp4
```

Remember to:

- **Change the pattern in** `-i img%03d.png` to reflect the filename pattern, replacing the `3` with the width of numeric sequence (the **total number of digits** including leading zeros to describe the number). 

- Adjust the `-framerate` option to the **number of frames per second**, to control the **speed of the video**.

- For `-vf fps=` it is recommended to **use the same number** as `-framerate` if it's `>=1`. Otherwise simply use `1` and the `mp4` format (or a higher number to be less jumpy, but create a larger file size).

- Change `out.mp4` to the **desired output-path and format type** of the created video e.g. `..\my_video.wmv` 

{% include note.html content="A `framerate >=1` shows **one or more images every second**. A `framerate <1` shows **each image for longer than a second** e.g. `-framerate 1/4` gives 4 seconds per image." %}

{% include tip.html content="Outputting `.wmv` files are friendly to use in Microsoft Powerpoint, but is problematic with a `framerate <1`." %}

{% include warning.html content="The `-framerate` option should always be placed **to the left** of the `-i` option in the command." %}

`ffmpeg` is very sensitive to parameter changes, and can be buggy, so please see its [Slideshow documentation](https://trac.ffmpeg.org/wiki/Slideshow) to try different parameters if undesired video output occurs.

{% include links.html %}