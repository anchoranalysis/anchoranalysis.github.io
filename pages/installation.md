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

[Download](download.html), run the installer, and add the directory containing `anchor` to the `$PATH` environmental variable.

Default installation locations are `C:\Users\SOMEUSER\AppData\Local\Anchor\` for Windows, and `/opt/anchor/` for Linux.

{% include important.html content="The installers provide a suitable runtime environment. A separate [JRE](https://www.java.com/download) (>= v21) is needed only with the `.zip` distribution" %}

{% include warning.html content="The Linux installer for .deb (e.g. `sudo dpkg -i anchor._1.0.0_amd64.deb`), may warn about *missing dependencies*. Fix with `sudo apt-get --fix-broken install`" %}

### Testing if successful

Simply, open a shell in a directory with images, and run `anchor`

{% include shell.html
command="anchor"
response="Searching recursively for image files. CTRL+C cancels.
Learn how to select inputs, outputs and tasks with 'anchor -h'.
<span class='commandLinesFollow'>...lines will follow after it searches for images...</span>" %}

{% include tip.html content="Follow the [Example Usage](/user_guide_examples.html) and [User Guide](/user_guide.html) to learn more." %}


