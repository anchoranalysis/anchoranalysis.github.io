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

We typically intuitively think of an image file as a digital photograph like a JPEG similar in appearance to human vision, containing a matrix of RGB pixels (three interdependent channels), or perhaps grayscale photographs (single channel).

In reality, images come in much more diverse form:

1. They may be three-dimensions.
2. They may contain multiple images indexed by time (time series, like movies or animated gifts), or other variables (location, modality).
3. They may have independent or dependent channels of any number.
4. The pixel color depth varies: 8-bit (as per RGB), 12-bit, 16-bit, floating point, color maps etc.
6. Their pixel-sizes may not be physically uniform in X, Y and Z dimensions (anisotropy).
7. Rather than pixels, they may be vectors or point-cloud images *(neither supported in Anchor)*.
8. They may be non-rectangular or support transparency *(neither supported in Anchor)*.

### Image file formats

And when encoded onto a filesystem:

* A single image may span several files; or a single file may contain several images.
* Formats vary widely and are often propietary.
* Compression or color-space encoding may introduce artefacts.
* Metadata is often included, text, numbers, shapes (annotations).
* Pyramid formats may introduce additional structure (multiple scaled-down version of the original) for quick access.

## Supported in Anchor

### Image types

Anchor supports much of this diversity:

* 2D/3D rectangular images with arbitrary number of channels and pixel-size, and 8-bit/16-bit color depths (some limited support for other depths). This is sufficient to include conventional photography, and many forms of biomedical, geospatial or scientific images.
* Time-series and other indexed forms of images (in a limited way).
* Certain forms of metadata (pixel size, channel names) but not others.
* Anchor-specific data structures for object-segmentations (pixel subregions, encoded into [HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format)) and  geometric shapes (useful for shape annotations and certain kinds of processing).

{% include note.html content="Remember, in all cases, anchor supports **sets** of these image-types, rather than processing only single images." %}

### Image file formats

The drivers for reading images in Anchor are termed *readers* and all inherit from [org.anchoranalysis.image.io.bean.rasterreader.RasterReader](https://github.com/anchoranalysis/anchor/blob/master/anchor-image-io/src/main/java/org/anchoranalysis/image/io/bean/rasterreader/RasterReader.java)

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
[FlattenAsChnl](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/rasterreader/FlattenAsChnl.java) | Converts indexed/time-series images into different channels.
[ImposeResolution](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/rasterreader/ImposeResolution.java)|Imposes a specific physical pixel size (across X,Y,Z dimensions).
[ReadVoxelExtentXml](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/rasterreader/ImposeResolution.java)|Reads physical pixel-size from an accompanying `.xml` file for each image.
[ThreeWayBranchXYResolution](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/rasterreader/ThreeWayBranchXYResolution.java)|Uses different readers for different ranges of X,Y physical pixel size.
[RejectIfConditionXYResolution](https://github.com/anchoranalysis/anchor-plugins/blob/master/anchor-plugin-io/src/main/java/org/anchoranalysis/plugin/io/bean/rasterreader/RejectIfConditionXYResolution.java)|Rejects images if a condition is filled on the X-Y resolution.


#### Custom drivers

Drivers for a wider range of formats are architecturally easily possible, but not currently implemented in the standard Anchor distribution.

### Changing the default driver

The default `RasterReader` is set in a configuration-file:

* `$ANCHOR_HOME/config/defaultBeans.xml` in the main Anchor distribution, and
* `$USER_HOME/.anchor/defaultBeans.xml` optionally, taking precedence.

{% include links.html %}
