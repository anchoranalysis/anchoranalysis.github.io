---
title: "Example - Converting and copying images"
tags:
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_examples_converting_copying_images.html
folder: user_guide
---


## Converting images to a different file format

Imagine that our current working-directory contains [three JPEGs](/downloads/examples/alps.zip): [`alps-13.jpg`, `alps-78.jpg`, `alps-91.jpg`].

The predefined task [convert](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/convert.xml) will convert images to the format specified by the [`-of` command-line option](/user_guide_command_line.html#output-options).

```none
anchor -t convert -of png -o C:\Users\owen\Desktop
```

This produces the following files in `C:\Users\owen\Desktop\convert_20.31.08`: [`13.png`, `78.png`, `91.png`]

{% include note.html content="If the [`-of` command-line option](/user_guide_command_line.html#output-options) is omitted, the default rules are applied to determine the format. This may be different from the existing file format of the input file." %}

### Perserving the image file-name

To similarly convert but **keep the *full* image file-name preserved** add the [`-ir` command-line option](/user_guide_command_line.html#input-options):

```none
anchor -ir -t convert -of png -o C:\Users\owen\Desktop
```

This produces instead: `alps-13.png` `alps-78.png` and `alps-91.png`.  

### Outputting to a specific output-directory (avoiding creating a subdirectory)

Note how the output-directory becomes a newly created subdirectory `convert_20.31.08` of what is passed to the `-o` option.

However, the behavior isn't always desired, and the [`-oo` command-line option](/user_guide_command_line.html#output-options) will disable it, letting the output directory be specified directly with `-o`. 

```none
anchor -t convert -of png -o C:\Users\owen\Desktop\desired_output_directory\ -oo
```

This creates the `C:\Users\owen\Desktop\desired_output_directory\` directory, and outputs to it.

### Preserving relative file-paths and any non-image-files

This command will convert images from a source directory to a target directory, while preserving file-names and subdirectory-structure **and** [any other non-image files](/http://localhost:4000/user_guide_examples_changing_output_options.html#additionally-copying-non-input-files) in the directory (via the [`-ic` command line option](/user_guide_command_line.html#output-options)).

```none
anchor -i c:\foo\source\ -ir -ic -t convert -of png -o c:\bar\destination\ -oo
```

## Copying files

To copy images, use the predefined task [copy](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/copy.xml).

By default, it will find image files, and copy them to the output-directory, using the varying parts of the filenames.

```none
anchor -i c:\foo\source\ -t copy -o c:\bar\destination\ -oo
```

### Preserving file-names

To **preserve file-names**, the [`-ir` command-line option](/user_guide_command_line.html#input-options) is added.

```none
anchor -i c:\foo\source\ -ir -t copy -o c:\bar\destination\ -oo
```

This also preserves subdirectory hierarchy.

### Suppressing subdirectory hierarchy

To **preserve file-names but suppress subdirectory hierarchy**, the [`-os` command-line option](/user_guide_command_line.html#output-options) is added.

```none
anchor -i c:\foo\source\ -ir -t copy -o c:\bar\destination\ -oo -os
```

{% include note.html content="The `copy` task executes more quickly than `convert`, copying files bytewise rather than loading as images. If the [-of command-line option](/user_guide_examples_converting_manipulating_images.htmlspecifying-an-alternative-image-format) is selected to request a different output format, then `copy` behaves instead like `convert`." %}


### Copying non-image files

The [copy](https://github.com/anchoranalysis/anchor-assembly/blob/master/anchor/src/main/resources/config/tasks/copy.xml) task
can be applied to any type of input. Use a file-filter on, the [`-i` command-line option](/user_guide_command_line.html#input-options) to search for particular types of
file extension - overriding the default behavior which only looks for images.

```none
anchor -i c:\foo\source\*.txt -ir -t copy -o c:\bar\destination\ -oo
```

{% include links.html %}