---
title: "User Guide - Troubleshooting"
tags: [getting_started, debugging]
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_troubleshooting.html
folder: user_guide
---

## Troubleshooting

Image processing is often resource-heavy and computational demanding. Anchor runs jobs in parallel, and issues often arise.

Here are some tips to resolve common issues.

### Limiting parallel CPU cores

By default, Anchor uses all-except-once available CPU cores to execute operations in parallel.

Some [tasks](/user_guide_tasks.html) require more memory than others. For a particular task, there can be insufficient available memory to facilitate so much parallelism, especially if a computer has many processors.

{% include warning.html content="An indication is when **out-of-memory** errors appear in logs or on the console." %}

It is then recommended **to reduce the number of cores**, by setting an explicit maximum with the [-tp command-line option](/user_guide_command_line.html#task-options).

e.g. to permit *no more than 4 cores in parallel:

```bash
anchor -t resize -tp 4
```

{% include tip.html content="One may experiment with different `-tp` values to find an appropriate number that doesn't result in memory errors." %}


### Memory allocation

Anchor is a Java program that executes in a [Java Virtual Machine (JVM)](https://en.wikipedia.org/wiki/Java_virtual_machine). A JVM requires an explicit initial and maximum [memory allocation](https://stackoverflow.com/questions/14763079/what-are-the-xms-and-xmx-parameters-when-starting-jvm).

How Anchor decides this limit, varies by operating system:

- For Windows, the `anchor.exe` launcher will initially allocate 20% of the heap memory, subject to an upper limit of 80%.
- For Linux and MacOS, the `anchor` bootstrap script (in the `bin/` directory) has hardcoded values of `-Xms500m -Xmx16000m`.

The user is recommended to adjust the latter as makes sense.

For Windows, no adjustment is currently possible at runtime to the `anchor.exe` loader, but as a fallback, consider starting Anchor in the traditional way using the `java` command-line application, similar to the Linux/MacOS script.

{% include links.html %}
