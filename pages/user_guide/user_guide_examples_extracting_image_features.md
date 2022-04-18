---
title: "Example - Extracting image features"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_extracting_image_features.html
folder: user_guide
---

## Extracting image features

Anchor contains several [predefined tasks](/user_guide_predefined_tasks.html) to extract [features](https://en.wikipedia.org/wiki/Feature_(machine_learning)) from images.


|Predefined Task | Features |
|-----|-----|
| [feature/metadata](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/metadata.xml) | image metadata (width, height, number of channels etc.) (*often runs quickly* as the entire image must not be read). |
| [feature/intensity](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/intensity.xml) | descriptive statistics on the pixel intensity values. |
| [feature/hog](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/hog.xml) | a [HOG feature descriptor](https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients) - given certain fixed parameters. |

Each task produces a `features.csv` CSV file, where each column represents a particular feature (and an *identifier* column) and each row represents a single input image.

## Example: extracting metadata features

The predefined task [feature/metadata](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/feature/metadata.xml) will extract features from the image header like width, height, number of channels etc. also providing physical measurements in microns, if included in image metadata.

{% include shell.html
command="anchor -t feature/metadata"
response="Experiment metadata_12.41.23 started writing to C:\Users\owen\AppData\Local\Temp\metadata_12.41.23
------------------------------------ Inputs ------------------------------------
The job has 3 inputs.

They are named with the pattern: ${0}
${0} = 3 unique integers between 13 and 91 inclusive
---------------------------------- Processing ----------------------------------
Preparing jobs to run with common initialization.
Using 7 processors CPUs from 8, and if needed and if possible, up to 0 simultaneous jobs using a GPU.
Job    2:       start   [  0 compl,   3 exec,   0 rem of   3]           78
Job    1:       start   [  0 compl,   3 exec,   0 rem of   3]           13
Job    3:       start   [  0 compl,   3 exec,   0 rem of   3]           91
Job    2:       end     [  1 compl,   2 exec,   0 rem of   3]   (5s)    78
Job    3:       end     [  2 compl,   1 exec,   0 rem of   3]   (6s)    91
Job    1:       end     [  3 compl,   0 exec,   0 rem of   3]   (7s)    13
All 3 jobs completed successfully. The average execution time was 6.700 ms.
----------------------------------- Outputs ------------------------------------
Enabled:        logExperiment, features, thumbnails
Disabled:       manifestExperiment, manifestJob
--------------------------------------------------------------------------------
Experiment metadata_12.41.23 completed (7s) writing to C:\Users\owen\AppData\Local\Temp\metadata_12.41.23" %}

{% include note.html content="This produces console messages **with** [execution-details](/user_guide.html#parallelization)." %}

Note in the console messages:
- the start / end events for each input.
- the name of the input is indicated on the right-hand side - and a job's total execution time.
- the output directory `C:\Users\owen\AppData\Local\Temp\metadata_12.41.23` is printed twice, at the start and end.

The following files are produced:

- `features.csv` where each row represents an input image, and each column an extracted feature.
- `experimentLog.txt` records the console output.
- the `thumbnails/` subdirectory, which contains a thumbnail for each row in the CSV file.
- **Only if an error occurs** (which it didn't!) then a job-specific log for `13_job_log.txt` etc.

The latter is useful for visualizing features alongside each other via derived embeddings etc. 

{% include tip.html content="The output directory can be changed with the [`-o` command-line option](/user_guide.html#outputs) e.g. `-o path_to_parent_directory`" %}


Here follows an *example `features.csv`* (with `-t feature/intensity`) from the [fruits dataset](/user_guide_examples_montage.html#example---fruits):

<img alt="screenshot of example features.csv" src="/images/examples/features/csv_ungrouped.jpg" class="screenshotExample"/>


## Grouping

Features can also be assigned a group via the [`-pg` command-line option](/user_guide_command_line.html#grouping):

```bash
anchor -t feature/hog -pg		# to group by the first identifier element (directory)
anchor -t feature/hog -pg 0		# identical to above
anchor -t feature/intensity -pg 0:-2	# to group by all elements, except the last

# like above, but enables other relevant outputs
anchor -t feature/intensity -pg 0:-2 -oe featuresAggregated,featuresGroup,featuresAggregatedGroup	
```

This has four impacts:

- A `group` column is added to `features.csv`
- Creates `featuresAggregated.csv` with group feature statistics (if the `featuresAggregated` output is enabled).
- Creates `featuresGroup.csv`*per group* with feature values (if the `featuresGroup` output is enabled).
- Creates `featuresAggregatedGroup.xml` *per group* with group statistics (if `featuresAggregatedGroup` is enabled).


Here follows an *example `featuresAggregated.csv`* (with `-t feature/intensity`) from sample of the [fruits dataset](/user_guide_examples_montage.html#example---fruits):

<img alt="screenshot of example featuresAggregated.csv" src="/images/examples/features/csv_grouped.jpg" class="screenshotExample"/>


## Next steps

- The CSV files can be visualized / processed in *Excel*, *Python* ([pandas](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)), [R](https://stat.ethz.ch/R-manual/R-devel/library/utils/html/read.table.html), [Spotfire](https://www.tibco.com/products/tibco-spotfire), [Ron's Editor](https://www.ronsplace.eu/products/ronseditor), and similar.

- The CSVs can be attached to images (as *multi-inputs*) for subsequent tasks in Anchor.

{% include links.html %}