---
title: "User Guide - Supported image formats"
tags: [getting_started]
keywords: formats
sidebar: user_guide_sidebar
permalink: user_guide_supported_formats.html
folder: user_guide
---

## Images are diverse

### Image types

We typically intuitively think of an image file as a digital photograph, similar in appearance to human vision, containing a matrix of RGB or grayscale pixels.

In reality, images come in diverse form:

- An image may be three-dimensional.
- An arbitrary number of independent or dependent channels may exist, neither three *(RGB)* nor one channel *(grayscale)*.
- Pixel color depth varies: 8-bit, 12-bit, 16-bit, floating point, color maps etc.
- Pixel-sizes may not be physically uniform in X, Y and Z dimensions *(anisotropy)*.
- Rather than pixels, they may be vectors or point-cloud images *(neither supported in Anchor)*.
- They may be non-rectangular or support transparency *(neither supported in Anchor)*.

### Image file formats

And when encoded onto a filesystem:

* A single image may span several files; or a single file may contain several images *(e.g an animated gif)*.
* Formats vary widely and are often proprietary.
* Compression or color-space encoding may introduce artefacts.
* Metadata is often included: text, numbers, shapes *(annotations)*, etc.
* Pyramid formats may introduce additional structure *(multiple scaled-down versions of the original)* for quick access.

## Supported in Anchor

### Image types

Anchor supports much of this diversity:

* **2D/3D rectangular images with arbitrary number of channels and pixel-size**.
* **Diverse bit depths**: *unsigned 8-bit*, *unsigned 16-bit*, *unsigned 32-bit* and *floating point*.
* Time-series and other indexed forms of images in a limited way.
* **Certain forms of metadata (pixel size, channel names)** but not others.
* Anchor-specific data structures for object-segmentations (pixel subregions, encoded into [HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format)) and  geometric shapes (useful for shape annotations).

{% include note.html content="Remember, in all cases, anchor supports **sets** of these image-types, rather than processing only single images." %}

### Image file formats

Anchor supports customizable <i>drivers</i> for reading and writing images, inheriting from [StackReader](/javadoc/org/anchoranalysis/image/io/bean/stack/StackReader.html) and [StackWriter](/javadoc/org/anchoranalysis/image/io/bean/stack/writer/StackWriter.html) respectively. 

#### Default Reader - Bioformats

The default reader, [org.anchoranalysis.plugin.io.bean.rasterreader.BioformatsReader](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/rasterreader/BioformatsReader.java), employs [Bioformats](https://www.openmicroscopy.org/bio-formats/) a popular open source library for reading microscopy and digital pathology images - as well as conventional photographs.

Please see the full list of Bioformat's [150 supported formats](https://docs.openmicroscopy.org/bio-formats/6.3.1/supported-formats.html) - with varying degrees of  support.

{% include warning.html content="Caveat emptor. Anchor has been tested so far on a limited subset of these formats." %}

#### Multi-file driver

Another driver, the [org.anchoranalysis.plugin.io.bean.rasterreader.MultiFileReader](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/rasterreader/MultiFileReader.java) virtually combines different files into a single image (as varying channels, or varying z-stacks in a 3D image, or varying timepoints in a time-series). A regular-expression is used to match file-paths.


#### Helper *utility* drivers

Other drivers  in `org.anchoranalysis.plugin.io.bean.rasterreader` provide useful utility functions:

|Class | Function|
|------|---------|
[FlattenAsChannel](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/stack/reader/FlattenAsChannel.java) | Converts indexed/time-series images into different channels.
[ImposeResolution](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/stack/reader/ImposeResolution.java)|Imposes a specific physical pixel size (across X,Y,Z dimensions).
[ReadVoxelExtentXml](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/stack/reader/ReadVoxelExtentXml.java)|Reads physical pixel-size from an accompanying `.xml` file for each image.
[ThreeWayBranchXYResolution](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/stack/reader/ThreeWayBranchXYResolution.java)|Uses different readers for different ranges of X,Y physical pixel size.
[RejectIfConditionXYResolution](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/stack/reader/RejectIfConditionXYResolution.java)|Rejects images if a condition is filled on the X-Y resolution.

### Changing the default driver

The default readers and writers are set in a `defaultBeans.xml` configuration-file:

* `$ANCHOR_HOME/config/defaultBeans.xml` in the main Anchor distribution, and
* `$USER_HOME/.anchor/defaultBeans.xml` optionally, taking precedence.

In practice, these readers and writers are usually implemented via hierarchies of rules that select an appropriate driver for a particular type of image, based upon whether its 2D/3D, the number
of channels, bit depth etc.

The user may also suggest a file format via the [`-of` command-line-option](/user_guide_command_line.html#output-options). 

{% include links.html %}
