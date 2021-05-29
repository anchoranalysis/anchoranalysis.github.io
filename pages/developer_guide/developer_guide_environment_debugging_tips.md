---
title: "Development Environment - Debugging Tips"
tags: [debugging]
keywords: environment, debugging, tips, eclipse
sidebar: developer_guide_sidebar
permalink: developer_guide_environment_debugging_tips.html
folder: developer_guide
toc: false
---

## Eclipse

### Debugging the command-line application

The anchor application can be launched in debugging-mode in Eclipse by running

```javascript
org.anchoranalysis.launcher.Launcher
```

with appropriate command-line arguments.

Be aware that in this context:

- not all plugins will necessarily be available, unless their projects are explicitly (and temporarily) added as dependencies, to the `anchor-launcher` project.

- Anchor expects to find a bootstrap `.properties` file in the current working directory, and if not present, an error message appears:

```none
Cannot find properties file at: C:\foo\bar\anchor-launcher\target\classes\anchor.properties
```

To resolve this error, simply create the small bootstrap files in this location, pointing to where the [Anchor Distribution](/developer_guide_anchor_distribution.html) is located e.g. `anchor.properties` becomes:

```none
default.config.path.relative=C:/Users/someuser/Apps/anchor/config/defaultExperiment.xml
```

### Debugging the GUI application

The above is similarly true of the [anchor-gui](developer_guide_repositories_anchor_gui.html) application, which can be debugged in Eclipse with:

```javascript
org.anchoranalysis.browser.launcher.LaunchInteractiveBrowser
```

It expects an `anchorGUI.properties` bootstrap file, e.g.

```none
default.config.path.relative=C:/Users/someuser/Apps/anchor/configGUI/experiment.xml
```

{% include links.html %}