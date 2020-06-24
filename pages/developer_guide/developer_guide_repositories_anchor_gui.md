---
title: "Source Repository - anchor-gui"
tags: [architecture]
keywords: architecture, packages, repositories
sidebar: developer_guide_sidebar
permalink: developer_guide_repositories_anchor_gui.html
folder: developer_guide
---

## Introduction

A Java (maven) source repository on [GitHub](https://github.com/anchoranalysis/anchor-gui) containing the GUI application for Anchor.

{% include warning.html content="This repository is considered (mostly) legacy code. It is not maintained to same standards as elsewhere." %}

It uses [Swing](https://en.wikipedia.org/wiki/Swing_(Java)) to run a graphical-app on the desktop.

{% include callout.html content="The command `anchor-gui` will launch it in an [Anchor distribution](developer_guide_anchor_distribution.html)" %}

### What can I do with the GUI application?

The GUI application supports:
- Loading sets of images
- Visualizing collections of objects and marks on top of individual images (including time-series and 3D).
- Interactive feature querying and calculation for objects and marks (click on objects and see its features!).
- Collecting ground truth by adding annotations (labels or marks) on top of images.
- Replaying optimization processes from the serialized output recorded.

### What belongs in the repository?

{% include tip.html content="It **should** include: anything related exclusively to the client-side Anchor GUI application." %}

{% include warning.html content="It should **not** include: GPL-licensed code, components reusable outside the GUI application, pipeline BeanXML, entry-point applications." %}

## Modules

| Module | Java Package Root &amp; Description  | Classes | Lines&#x2011;of&#x2011;Code |
|------------|------------------|-------------:|-------------:|
| [anchor-gui-annotation](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-annotation) | | ? | 4,588 |
| [anchor-gui-browser](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-browser) | | ? | 1,185 |
| [anchor-gui-common](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-common) | | ? | 3,717 |
| [anchor-gui-export](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-export) | | ? | 305 |
| [anchor-gui-feature-evaluator](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-feature-evaluator) | | ? | 2,034 |
| [anchor-gui-finder](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-finder) | | ? | 609 |
| [anchor-gui-frame](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-frame) | | ? | 9,421 |
| [anchor-gui-graph](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-graph) | | ? | 1,836 |
| [anchor-gui-import](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-import) | | ? | 566 |
| [anchor-gui-mdi](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-mdi) | | ? | 1,334 |
| [anchor-plugin-gui-annotation](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-plugin-gui-annotation) | | ? | 396 |
| [anchor-plugin-gui-export](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-plugin-gui-export) | | ? | 1,463 |
| [anchor-plugin-gui-import](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-gui-annotation) | | ? | 7,570 |
| [anchor-plugin-gui-live](https://github.com/anchoranalysis/anchor-gui/tree/master/anchor-plugin-gui-live) | | ? | 488 |

Number of classes/code is as per *SonarQube, June 24th, 2020*. Lines-of-code excludes whitespace and comments.

{% include links.html %}
