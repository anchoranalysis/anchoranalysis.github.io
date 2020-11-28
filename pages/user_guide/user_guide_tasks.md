---
title: "User Guide - Tasks"
tags: [getting_started]
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_tasks.html
folder: user_guide
---

## Tasks

A task is a unit of processing, applied to one or more inputs, and producing derived outputs.

{% include tip.html content="Each task accomplishes one goal - either its is entirety, or as single step towards a greater goal, like a single step in a pipeline of image processing operations." %}

Note:
- Some tasks produce no outputs, only messages in the console.
- Tasks often produce outputs **independently** for each corresponding input e.g. *scaling each  image to a different size*.
- However, tasks can also produce outputs by **aggregating** many inputs e.g. *a montage image of all inputs*.

If you are familar with the [map-reduce](https://en.wikipedia.org/wiki/MapReduce) processing
paradigm, these can be considered like a *map* step or a *reduce* step.

## Predefined tasks

Several predefined tasks are bundled with the Anchor distribution - intended to be easily executed from the command line.

### The `/config/tasks/` directory.

The predefined tasks are specified by BeanXML in the [/config/tasks/](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/config/tasks) subdirectory in an [Anchor distribution](/developer_guide_anchor_distribution.html).

Users are free to add (or remove) tasks to this directory.

Any task in this directory can be referred in the Anchor command-line application by only its name, with neither a full path nor an `.xml` extension. These statements both refer to the same task, and achieve the same effect:

```shell
anchor -i *.png -t features/hog
anchor -i *.png -t /path/to/anchorDistribution/config/tasks/features/hog.xml
```

### Understanding each task

- An overview of all the predefined tasks is found in [Example Usage](/user_guide_examples.html).
- Each task also includes a more detailed description as a comment in its [BeanXML](https://github.com/anchoranalysis/anchor-assembly/tree/master/anchor-assembly/src/main/resources/config/tasks).


## Building a new task
 
New tasks can be specified in BeanXML using classes that inherit from [Task](/javadoc/org/anchoranalysis/experiment/bean/task/Task.html).

{% include links.html %}
