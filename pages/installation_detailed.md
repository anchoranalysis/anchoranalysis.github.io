---
title: "Installation - Detailed Instructions"
keywords: install download anchor image analysis microscopy
tags: [getting_started]
sidebar:
permalink: installation_detailed.html
hide_sidebar: true
toc: false
disable_editme: true
---

Anchor is a command-line application, designed to be used with `PowerShell` / `Command Prompt` in Windows, `Terminal` in MacOS or any `Linux` shell.

It should be added to the system's `PATH` environmental variable.

## Steps

### 1. Download and unpack

1. Download the [latest distribution](download.html). 
2. Unpack the `zip` or `tar.gz` into a directory of one's choosing.


### 2. Install a Java Runtime Environment (JRE) if necessary. 

JRE version 8 or above is required. This is often already present. If not, Oracle offers a [free download](https://www.java.com/download). 

### 3. Set up environment variables

1. Add Anchor's `bin/` subdirectory of the anchor-distribution to `PATH`. 

Please use the standard ways to set environment variables, e.g. for [Windows](https://www.computerhope.com/issues/ch000549.htm), and for Linux and macOS, lines can be added at the end of `$HOME/.bash_profile` ala:

```shell
export PATH=/SOME_PATH_TO_ANCHOR/bin/:$PATH
export ANCHOR_HOME=/SOME_PATH_TO_ANCHOR/
```
2. Type `java -version` in a shell, and check it returns at least version 1.8.

If not:
1. Ensure `JAVA_HOME` points to the location of the JRE.
2. Ensure the directory for the `java` application (`$JAVA_HOME/bin`) exists in the `PATH` variable.

### 4. Installation complete - test the command!

Congratulations, *Anchor* should now be ready to run!

Open a shell (e.g. Command Prompt or PowerShell in Windows) in a directory with images, and type:

```
anchor
```

{% include tip.html content="Follow the [User Guide](user_guide.html) to learn more." %}


