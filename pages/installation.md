---
title: "Installation"
keywords: install download anchor image analysis microscopy
tags: [getting_started]
sidebar:
permalink: installation.html
hide_sidebar: true
toc: false
disable_editme: true
---

Anchor is a command-line application, designed to be used with `PowerShell` / `Command Prompt` in Windows, `Terminal` in MacOS or any `Linux` shell.

## Quick Instructions

[Download](download.html), unzip, and add the `bin/` directory to `$PATH` environmental variable.

{% include important.html content="Ensure you have a [JRE](https://www.java.com/download)  > 1.8 and `$JAVA_HOME` properly configured." %}

[Detailed installation instructions](installation_detailed.html) are also available.

### Testing if successful

Simply, open a shell in a directory with images, and run `anchor`

<pre class="commandLine">
$ <b>anchor</b>
Searching recursively for image files. CTRL+C cancels.
Learn how to select inputs, outputs and tasks with 'anchor -h'.
<span class="linesFollow">...lines will follow after it searches for images...</span>
</pre>

{% include tip.html content="Follow the [User Guide](/user_guide.html) and [Example Usage](/user_guide_examples.html) to learn more." %}


