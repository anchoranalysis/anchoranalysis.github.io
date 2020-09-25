---
title: "Source Repository - anchor-gui"
tags:
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_gui.html
folder: developer_guide
---

## Introduction

A **Java** ([Maven](/developer_guide_environment_maven.html)) source repository on [GitHub](https://github.com/anchoranalysis/anchor-gui) containing the [GUI application](/user_guide_advanced_gui.html) for Anchor.

{% include warning.html content="This repository is considered deprecated legacy code. It is not maintained to same standards as elsewhere." %}

The GUI application is based on [Swing](https://en.wikipedia.org/wiki/Swing_(Java)).

### What belongs in the repository?

{% include tip.html content="It **should** include: anything related exclusively to the client-side Anchor GUI application." %}

{% include warning.html content="It should **not** include: GPL-licensed code, components reusable outside the GUI application, pipeline BeanXML, entry-point applications." %}

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-gui-annotation](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-annotation) | `org.anchoranalysis.gui.annotation`<br>**Deprecated**. Interactively annotating images. | 107 | 4,588 |
| [anchor-gui-browser](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-browser) | `org.anchoranalysis.gui.interactivebrowser`<br>**Deprecated**. Launching the GUI application. | 17 | 1,185 |
| [anchor-gui-common](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-common) | `org.anchoranalysis.gui.common`<br>**Deprecated**. Shared utilities and data classes. | 92 | 3,717 |
| [anchor-gui-export](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-export) | `org.anchoranalysis.gui.export`<br>**Deprecated**. Exporting from the GUI. | 9 | 305 |
| [anchor-gui-feature-evaluator](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-feature-evaluator) | `org.anchoranalysis.gui.feature.evaluator`<br>**Deprecated**. Evaluating features on images. | 50 | 2,034 |
| [anchor-gui-finder](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-finder) | `org.anchoranalysis.gui.manifest`<br>**Deprecated**. Loading from manifests. | 14 | 609 |
| [anchor-gui-frame](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-frame) | `org.anchoranalysis.gui`<br>**Deprecated**. Frames and related widgets. | 228 | 9,421 |
| [anchor-gui-import](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-import) | `org.anchoranalysis.gui`<br>**Deprecated**. Loading files. | 16 | 566 |
| [anchor-gui-mdi](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-mdi) | `org.anchoranalysis.gui`<br>**Deprecated**. Arranging frames/windows. | 31 | 1,334 |
| [anchor-gui-plot](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-plot) | `org.anchoranalysis.gui.plot`<br>**Deprecated**. Visualizing plots. | 39 | 1,836 |
| [anchor-plugin-gui-annotation](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-plugin-gui-annotation) | `org.anchoranalysis.plugin.annotation`<br>**Deprecated**. Annotation plugins. | 5 | 396 |
| [anchor-plugin-gui-export](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-plugin-gui-export) | `org.anchoranalysis.plugin.gui`<br>**Deprecated**. Plugins for exporting. | 33 | 1,463 |
| [anchor-plugin-gui-import](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-annotation) | `org.anchoranalysis.plugin.gui`<br>**Deprecated**. Plugins for importing. | 146 | 7,570 |

Number of classes/code is as per *SonarQube, June 24th, 2020*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
