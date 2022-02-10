---
title: "User Guide - Supported image formats"
tags: [getting_started]
keywords: formats
sidebar: user_guide_sidebar
permalink: user_guide_supported_formats.html
folder: user_guide
---

## Supported image types

### Images are diverse

We intuitively think of an image file as a digital photograph, similar in appearance to human vision, containing a matrix of RGB or grayscale pixels.

In reality, images come in diverse form: varying in dimension, number of channels, color depth and type, whether pixel-sizes are uniform in all dimensions, and in many other respects.

And when encoded onto a filesystem, file formats vary widely also with different encodings, types of compression, proprietary codes, and metadata.

### Image types supported in Anchor

Anchor supports much, but not all, of this diversity:

* **2D/3D rectangular images with arbitrary number of channels and pixel-size** *(anisotropy)*.
* **diverse bit depths**: *unsigned 8-bit*, *unsigned 16-bit*, *unsigned 32-bit* and *floating point*.
* time-series and other indexed forms of images in a limited way.
* **certain forms of metadata (pixel size, channel names)** but not others.
* Anchor-specific data structures for:
	* object-segmentations *(pixel subregions, encoded into [HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format))*
	* geometric shapes *(useful for shape annotations)*.

### What's not supported

Images containing the following are not yet supported:
- transparency
- pyramidal formats *(containing multiple scaled-down versions for quick access at scale)*
- point clouds 

{% include note.html content="Remember, in all cases, anchor supports **sets** of these image-types, rather than processing only single images." %}

## Reading and writing image formats

A flexible method of reading and writing different file-formats is provided through customizable
classes for reading and writing images, inheriting from [StackReader](/javadoc/org/anchoranalysis/image/io/bean/stack/StackReader.html) and [StackWriter](/javadoc/org/anchoranalysis/image/io/bean/stack/writer/StackWriter.html) respectively.

### Specifying image file extensions

By default anchor, searches for image-files by comparing file-extensions against those in [defaultInputExtensions.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/defaultInputExtensions.xml):

* `$ANCHOR_HOME/config/defaultInputExtensions.xml` in the main Anchor distribution.

### Specifying default readers and writers

The default readers and writers are set in [defaultBeans.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/defaultBeans.xml) configuration-files, found at:

* `$ANCHOR_HOME/config/defaultBeans.xml` in the main Anchor distribution, and
* `$USER_HOME/.anchor/defaultBeans.xml` optionally, taking precedence.

In practice, these readers and writers are usually implemented via hierarchies of rules that select an appropriate driver for a particular type of image, based upon whether its 2D/3D, the number of channels, bit depth etc.

The user may also suggest a preferred file format for writing via the [`-of` command-line-option](/user_guide_command_line.html#output-options). See the [Converting and manipulating images](/user_guide_examples_converting_manipulating_images.html) for example usage.

### Reading images

By default, the following logic decides which reader is used for an image file:

| Condition | Reader | Supported Formats |
|-----------|--------|-------------------|
| `.bmp` extension | [OpenCVReader](/javadoc/org/anchoranalysis/plugin/opencv/bean/stack/OpenCVReader.html) | BMP |
| `.jpg` or `.jpeg` extension | [BioformatsReader](/javadoc/org/anchoranalysis/io/bioformats/bean/BioformatsReader.html) | JPEG ([auto-adjusted to any EXIF orientation](https://www.howtogeek.com/254830/why-your-photos-dont-always-appear-correctly-rotated/)) |
| anything else | [BioformatsReader](/javadoc/org/anchoranalysis/io/bioformats/bean/BioformatsReader.html) | approximately [150 supported formats](https://docs.openmicroscopy.org/bio-formats/6.3.1/supported-formats.html) |

See the `StackReader` section of [defaultBeans.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/defaultBeans.xml) for the exact [configurable](/user_guide_supported_formats.html#specifying-default-readers-and-writers) rules.

{% include warning.html content="Caveat emptor. Anchor has been tested so far on a limited subset of these formats." %}

#### Multi-file driver

Another driver, the [MultiFileReader](/javadoc/org/anchoranalysis/plugin/io/bean/stack/reader/MultiFileReader.html) virtually combines different files into a single image (as varying channels, or varying z-stacks in a 3D image, or varying timepoints in a time-series). A regular-expression is used to match file-paths.

#### Helper *utility* drivers

Other drivers  in `org.anchoranalysis.plugin.io.bean.rasterreader` provide useful utility functions:

|Class | Function|
|------|---------|
[FlattenAsChannel](/javadoc/org/anchoranalysis/plugin/io/bean/stack/reader/FlattenAsChannel.html) | Converts indexed/time-series images into different channels.
[ImposeResolution](/javadoc/org/anchoranalysis/plugin/io/bean/stack/reader/ImposeResolution.html)|Imposes a specific physical pixel size (across X,Y,Z dimensions).
[ReadVoxelExtentXml](/javadoc/org/anchoranalysis/plugin/io/bean/stack/reader/ReadVoxelExtentXml.html)|Reads physical pixel-size from an accompanying `.xml` file for each image.
[RejectIfConditionXYResolution](/javadoc/org/anchoranalysis/plugin/io/bean/stack/reader/RejectIfConditionXYResolution.html)|Rejects images if a condition is filled on the X-Y resolution.

### Writing images

By default, the following logic decides which writer is used for an image:

| Image Type | Writer | Reason |
|-----------|--------|-------------------|
| Binary 2D | [PNG](/javadoc/org/anchoranalysis/io/imagej/bean/stack/writer/PNG.html) via *ImageJ* | Avoids compression artefacts. |
| Binary 3D | [Tiff](/javadoc/org/anchoranalysis/io/bioformats/bean/writer/Tiff.html) via *Bioformats* | Like above, but can save 3D images. |
| *RGB or Grayscale 2D | [PNG](/javadoc/org/anchoranalysis/io/imagej/bean/stack/writer/PNG.html) via *ImageJ* | Widely-supported and lossless compression. |
| RGB or Grayscale 3D | [Tiff](/javadoc/org/anchoranalysis/io/bioformats/bean/writer/Tiff.html) via *Bioformats* | Can save 3D images as multi-frame. |
| *Three-channels but **not** RGB | [Tiff](/javadoc/org/anchoranalysis/io/bioformats/bean/writer/Tiff.html) via *Bioformats* | Can save three channels independently. | 
| anything else | [OMETiff](/javadoc/org/anchoranalysis/io/bioformats/bean/writer/OMETiff.html) via *Bioformats* | Supports diverse image types. |

Binary images are stored as unsigned 8-bit but with only 0 and 255 as valid states.

In the two asterixed cases, if a [`-of` command-line-option](/user_guide_command_line.html#output-options) is supplied, a matching writer for this format
will be found and instead used, but only if one is available and supports the image-type.

See the `StackWriter` section of [defaultBeans.xml](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/defaultBeans.xml) for the exact [configurable](/user_guide_supported_formats.html#specifying-default-readers-and-writers) rules.


{% include links.html %}
