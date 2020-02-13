---
title: "Developer Guide - Introduction: Anchor Distribution"
tags: [build, maven, getting_started]
keywords: distribution, maven, jars, release, build
sidebar: developer_guide_sidebar
permalink: developer_guide_intro_anchor_distribution.html
folder: developer_guide
---

## What is an Anchor Distribution?

An *Anchor distribution* is a folder which contains all the jars and configuration-files to run Anchor. It has the following structure:

| Folder | Description |
|--------|-------------|
| bin/ | anchor-launcher.jar and anchor-browser.jar and associated helper-applications |
| lib/ | other anchor jars and third-party dependencies  |
| config/ | default configuration files in [BeanXML](https://bitbucket.org/anchorimageanalysis/anchor/wiki/Anchor%20Beans) for the anchor application |
| configGUI/ | default configuration files in [BeanXML](https://bitbucket.org/anchorimageanalysis/anchor/wiki/Anchor%20Beans) for the anchorGUI application |

**N.B. The *bin/* directory should usually be added to the system PATH variable** for easy command-line usage.

## Helper applications

Helper-applications (*anchor*, *anchor.exe*, *anchorGUI*, *anchorGUI.exe* etc.) start the relevant jar with a specific memory profile, and making sure *lib/* and *plugins/* folder are also added to the classpath.

The UNIX helper applications (*anchor* and *anchorGUI*) are BASH scripts that can be easily edited.

The Windows helper applications (*anchor.exe* and *anchorGUI.exe*) use [Launch4J](http://launch4j.sourceforge.net/) to launch Java directly from windows. These are created during the Maven build process.
