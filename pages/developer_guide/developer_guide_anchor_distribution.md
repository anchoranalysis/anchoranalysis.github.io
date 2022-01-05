---
title: "Developer Guide - Anchor distribution"
tags: [build, maven, getting_started]
keywords: distribution, maven, jars, release, build
sidebar: developer_guide_sidebar
permalink: developer_guide_anchor_distribution.html
folder: developer_guide
---

## What is an Anchor distribution?

An *Anchor distribution* is a folder which contains all the jars and configuration-files to run Anchor. It has the following structure:

| Folder | Description |
|--------|-------------|
| `bin/` | anchor-launcher.jar and associated helper-applications |
| `lib/` | other anchor jars and third-party dependencies  |
| `config/` | default configuration files in [BeanXML](https://bitbucket.org/anchorimageanalysis/anchor/wiki/Anchor%20Beans) for the anchor application |
| `models/` | bundled trained machine-learning models |

{% include note.html content="Add the *bin/* directory to the `PATH` system environment variable for easy command-line usage." %}

## Launcher applications

Launcher applications (`anchor`, `anchor.exe`, `anchorGUI`, `anchorGUI.exe` etc.) run the relevant jar with a specific memory profile, also ensuring `lib/` and `plugins/`are added to the classpath.

The UNIX launcher applications (`anchor` and `anchorGUI`) are BASH scripts that can be easily edited.

The Windows launcher applications (`anchor.exe` and `anchorGUI.exe`) use [Launch4J](http://launch4j.sourceforge.net/) to launch Java directly from windows. These are created during the Maven build process.
