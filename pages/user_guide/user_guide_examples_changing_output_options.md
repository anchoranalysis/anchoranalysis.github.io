---
title: "Example - Changing output options"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_changing_output_options.html
folder: user_guide
---

## Background

This guide introduces certain command-line options to change the **file format** or **file naming** in the outputted files.

The output files derive from input files, with three typical cases:

- **Case 1**: a function of a *single* image: `one image in, one derived file out` - executed on **each** input image.
- **Case 2**: a function of a *single* image: `one image in, one derived directory out` - executed on **each** input image.
- **Case 3**: a function of *many* images: `many images in, one derived directory out` - executed on **all** input images.

In **Case 1**, only a single output file is produced for each input. The other cases produce a derived directory of output files.

Filenames are selected from a unique *identifier* guessed from the input names (e.g. a varying number or substring).

This guide describes command-line options to select alternatives - both for the naming, and the outputted file format.

### Example of guessed names

For an example, given an input directory with three input images:

```
selfie_january.jpg
selfie_february.jpg
selfie_december.jpg
```

Then Anchor would guess identifiers [`january`, `february`, `december`].

Outputs would be formed for each of the three cases above, as follows:

- For **Case 1** producing *one derived file out*:  [`january.jpg`, `february.jpg`, `december.jpg`]
- For **Cases 2 and 3** producing *one derived directory out*: [`january/`, `february/`, `december/`]

{% include tip.html content="The input directory will **never** be altered. By default, *Anchor* refuses to write into an existing output-directory, and names output-directories with a timestamp to reduce chances of unintended overwriting." %}

## Disabling the shortened identifiers

As described above, the default behaviour guesses a shorted identifier from the file-path (using the varying elements).

The [`-ip` command-line option](/user_guide_command_line.html#input-options) disables this shortening behaviour. It instead **preserves the entire input file-name**.

 e.g. the previous example would produce [`selfie_january.jpg`, `selfie_february.jpg`, `selfie_december.jpg`] 

### Preserving file-paths exactly

If only a single output file produced (see [Case 1](/user_guide_examples_changing_output_options.html#background)), the `-ip` option gives it an identical name to the corresponding input-file.

In fact, the behaviour is *more general*: the entire **relative file-path** (relative to the input-directory) is considered, so that any subdirectory hierarchy is perfectly preserved. This is ideal for repeated successive immutable transformations.

e.g. `input_directory/foo/file12.png` produces `output_directory/foo/file12.ext`. 

The following example command converts input files from one directory to another, preserving the file-naming and hierarchy.

```none
anchor -i c:\foo\source\ -ip -t convert -o c:\bar\destination\ -oo
```

## Enabling and disabling outputs

A task typically can make several outputs, but only certain outputs occur by default. All available outputs are printed upon completion e.g.

{% include shell.html
command="anchor -t feature/intensity"
response="Experiment intensity_09.50.11 started writing to C:\Users\owen\AppData\Local\Temp\intensity_09.50.11
------------------------------------ Inputs ------------------------------------
The job has 3 inputs.

They are named with the pattern: ${0}
${0} = 3 unique integers between 13 and 91 inclusive
---------------------------------- Processing ----------------------------------
Preparing jobs to run with common initialization.
Maximally using 7 simultaneous CPUs (from 8 available), and up to 1 simultaneous GPU (if available).
Job    3:       start   [  0 compl,   2 exec,   1 rem of   3]           91
Job    1:       start   [  0 compl,   2 exec,   1 rem of   3]           13
Job    2:       start   [  0 compl,   3 exec,   0 rem of   3]           78
Job    2:       end     [  1 compl,   2 exec,   0 rem of   3]   (0s)    78
Job    3:       end     [  2 compl,   1 exec,   0 rem of   3]   (0s)    91
Job    1:       end     [  3 compl,   0 exec,   0 rem of   3]   (0s)    13
All 3 jobs completed successfully. The average execution time was 0.315 s.
----------------------------------- Outputs ------------------------------------
Enabled:        features, logExperiment
Disabled:       executionTime, featuresAggregated, thumbnails
--------------------------------------------------------------------------------" %}

The last four lines indicate which outputs were enabled and disabled. The user can enable/disable these outputs with the `-oe` and `-od` and `-oa` [command-line options](/user_guide_command_line.html#output-options):

```bash
# Enable all outputs
anchor -t feature/intensity -oa

# Enables thumbnails and disables two (multiple options)
anchor -t feature/intensity -oe thumbnails -od logExperiment -od features

# Enables two (comma-separated), disables one
anchor -t feature/intensity -oe thubmnails,featuresAggregated -od features
```

## Additionally copying non-input files 

Files may exist alongside images in the input directory that are not inputs, but that we wish to also copy to the output directory (metadata files etc.). They should not be inputs, as they will not be processed, but just copied unchanged.

The [`-ic` command-line option](/user_guide_command_line.html#input-options) achieves this by **additionally** copying all files that are ***not* considered inputs** from the input directory to the output directory.

e.g. `input_directory/foo/file12.txt` (not an input image file) is copied to `output_directory/foo/file12.txt`

```none
anchor -i c:\foo\source\ -ic -t convert -o c:\bar\destination\ -oo
```

## Specifying an alternative image format

Anchor uses context-sensitive [configurable rules](/user_guide_supported_formats.html#writing-images) to select an image file-format for writing.

These rules exist as **no one format is ideal for all circumstances**. Certain types of images (3D, multi-channel etc.) require or are better suited to particular formats. Anchor tries to pick smart defaults.

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

{% include warning.html content="If a particular requested format is unsupported by the image-type, *Anchor* will prefer to quietly use a different fallback, rather than exit with an error message." %}

This [`-of` command-line option](/user_guide_command_line.html#output-options) can be used for *any* image producing task.


## Writing outputs as a sequence

The [`-on` command-line option](/user_guide_command_line.html#output-options) will ignore the identifier, and instead write each output as a sequence of increasing integers (beginning at 0).

This can be useful for software that expects images as a sequence, e.g. `image_0000.tif`, `image_0001.tif`, `image_0002.tif`, etc. as is needed in the creating [video from images](/user_guide_examples_video_from_images.html) tutorial.

## Suppressing directory structure

The [`-os` command-line option](/user_guide_command_line.html#output-options) will replace any directory separators (i.e. the `/`) in the output-names with an underscore.

This **flattens any subdirectory hierarchy** e.g.

`path_to_output_directory/foo/bar/output.png` becomes instead `path_to_output_directory/foo_bar_output.png`

## Outputting to a specific output-directory (avoiding creating a subdirectory)

By default, output files are **not** placed directly in the output-directory specified via the [`-o` command-line option](/user_guide_command_line.html#output-options), but rather **in a newly created subdirectory** thereof.

{% include tip.html content="The newly-created subdirectory's name includes a timestamp, so an unchanged command can be **safely called repeatedly** e.g. for debugging, or exploring parameter change." %}

However, the behavior isn't always desired, and the [`-oo` command-line option](/user_guide_command_line.html#output-options) will disable it.

The `-oo` option is always accompanied by an `-o` to specify directly the directory.

{% include warning.html content="As a safety protection, **a directory must not already exist at this path**, Anchor will exit with an error. The existing directory must be deleted or moved, before re-executing the command." %}

e.g. the following creates the `C:\Users\owen\Desktop\desired_output_directory\` directory, and outputs directly into it.

```none
anchor -t convert -of png -o C:\Users\owen\Desktop\desired_output_directory\ -oo
```


{% include links.html %}