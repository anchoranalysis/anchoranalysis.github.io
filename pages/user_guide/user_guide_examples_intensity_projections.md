---
title: "Example - Intensity Projections"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_intensity_projections.html
folder: user_guide
---

## Maximum intensity projection

A [maximum-intensity-projection](https://en.wikipedia.org/wiki/Maximum_intensity_projection) can be applied:

- across slices in a 3D image (across the z-dimension)
- across multiple images 

It finds the <b>maximum</b> across the corresponding voxels in many images / slices.

### Across constant size images

```bash
anchor -t project/mean
```

### Across varying size images

The following is similar to previous, but first resizes images to a particular size (*1024x768* by default), and flattens any 3D
image. This allows the operation to work with images of different sizes.

```bash
anchor -t project/meanResize
```


### Example image

By way of example, we will show the results of the operation on some time-series images of a tennis player.

<img alt="montage of time-series tennis photos" src="/images/examples/intensityProjections/montage.jpg"/>

Note how the background is very similar across the frames.

It produces a <b>maximum</b>-intensity-projection across the images:

<img alt="maximum-intensity-projection of time-series tennis photos" src="/images/examples/intensityProjections/max.png"/>


## Mean intensity projection

This is similar to the previous projection except it finds the <b>mean</b> (average) of each voxel value across images.

It can be useful for <a href="https://en.wikipedia.org/wiki/Foreground_detection">background subtraction</a>, or investigating the consistency of images.

```bash
anchor -t project/mean
anchor -t project/meanResize
```

<img alt="mean-intensity-projection of time-series tennis photos" src="/images/examples/intensityProjections/mean.png"/>

## Minimum intensity projection

And similarly, but to find the <b>minimum</b> across the corresponding voxels in many images.

```bash
anchor -t project/min
anchor -t project/minResize
```

<img alt="min-intensity-projection of time-series tennis photos" src="/images/examples/intensityProjections/min.png"/>


## Standard-deviation intensity projection

And to find the <b>standard-deviation</b> across the corresponding voxels in many images.

This can be useful for identifying the pixels which change little over the course of a time-series.

```bash
anchor -t project/standardDeviation
anchor -t project/standardDeviationResize
```

<img alt="standard-deviation-intensity-projection of time-series tennis photos" src="/images/examples/intensityProjections/standardDeviation.png"/>


*The original tennis time-series images come from the [UCF101 video classification dataset](https://www.crcv.ucf.edu/data/UCF101.php), downloaded from [Kaggle](https://www.kaggle.com/ashuguptahere/video-classification-ucf101).*

## Grouping

The images above all performed the projection on every input image. To instead, partition the inputs into groups, and perform a separate projection for each group use the [`-pg` command-line option](/user_guide_command_line.html#grouping):

```bash
anchor -t project/meanResize -pg 0	# to partition by the first identifier element (directory).
anchor -t project/min -pg 0:-2		# to partition by all elements, except the last.
anchor -t project/min -pg -1		# to partition by the last element.
```

Examples ([montaged](/user_guide_examples_montage.html) together) follow of `project/mean` and `project/standardDeviation`, as  applied on groups in the [fruits dataset]:

<img alt="mean-intensity-projection of groups of fruits" src="/images/examples/intensityProjections/fruit_grouped_mean.jpg"/>

<img alt="standard-deviation-intensity-projection of groups of fruits" src="/images/examples/intensityProjections/fruit_grouped_standardDeviation.jpg"/>


## Next steps

- Use a projection to inform further analysis of time-series images / video, e.g:
	- to [background subtract](https://docs.opencv.org/4.x/d1/dc5/tutorial_background_subtraction.html) the mean-intensity.
	- to consider only regions with significant standard-deviation.

{% include links.html %}