---
title: "Example - Anonymizing and randomly sampling files"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_anonymizing_sampling.html
folder: user_guide
---

## Background

It is often desirable to run an Anchor task on a subset of files (either randomly chosen, or the first **n** inputs in order).

This can be:

- **temporarily**, testing a command before running it on the entire set of inputs.
- **permanently**, extracting a subset into another directory.
- **permanently with anonymization** - like above, but the filenames lose identifying information.

Anchor provides a series of [input command options](/user_guide_command_line.html#input-options), that can be combined to achieve this for many tasks.

It also provides the `anonymize` [predefined-task](/user_guide_predefined_tasks.html#file-copying--conversion).

## Subsetting inputs

### Taking the initial *n* inputs in order

Use the `-il` [command option](/user_guide_command_line.html#input-options) to restrict the total number of inputs.

e.g. to form a montage of the initial 7 files (maximally).

```none
anchor -il 7 -t montage
```

### Taking a % of all inputs.

The `-il` [command option](/user_guide_command_line.html#input-options) also accepts a floating-point in the range (`0.0 < floating_value < 1.0`), indicating a percentage of the total number of inputs.

e.g. to convert the initial `20%` of all inputs (maximally).

```none
anchor -il 0.2 -t convert
```


### A random subset

Add the `-is` [command option](/user_guide_command_line.html#input-options) to shuffle the files, before the limit is applied.

e.g. to copy a random subset:

```none
anchor -is -il 20 -t copy		# a random subset of 20 files (maximally)
anchor -is -il 0.5 -t copy		# a random subset of 50% of the total number of inputs
```

{% include tip.html content="The `-il` and `-is` options can be applied to the inputs for any [predefined task](/user_guide_predefined_tasks.html)." %}

## Anonymizing

### Outputting as a numeric sequence

The easiest anonymizaton occurs by combining the `-il` and `-is` [command input options](/user_guide_command_line.html#input-options) (see above) with the `-on` [command output options](/user_guide_command_line.html#output-options), which writes files as an incrementing numeric series.

```none
anchor -is -il 20 -on -t convert
```

{% include tip.html content="This approach is valid for any [predefined task](/user_guide_predefined_tasks.html), whether copying, converting, resizing etc." %}

### The `anonymize` predefined task

Alternatively, the `anonymize` [predefined-task](/user_guide_predefined_tasks.html#file-copying--conversion) is similar to the `copy` task, but will automatically anonymize the names.

For fully random selection, the `-is` option must be included when the `-il` option is also present. Otherwise it is unneeded, as the inputs will always be randomized internally within the task.

```none
anchor -t anonymize			# anonymize all the inputs
anchor -is -il 0.3 -t anonymize		# anonymize 30% of the inputs
```

{% include warning.html content="This approach is valid **only** for copying files" %}

{% include links.html %}