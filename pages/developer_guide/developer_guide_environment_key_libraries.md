---
title: "Development Environment - Key Libraries"
tags: [build]
keywords: environment, lombok
sidebar: developer_guide_sidebar
permalink: developer_guide_environment_key_libraries.html
folder: developer_guide
toc: false
---

## Maven plugins

Anchor uses several key libaries via [Maven](/developer_guide_environment_maven.html) plugins:

* [Project Lombok](https://projectlombok.org/) to reduce boilerplate code and duplication of code. Note its [key features](https://projectlombok.org/features/all).

* [spotless](https://github.com/diffplug/spotless/tree/master/plugin-maven) to automatically restyle
Java code to match the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).

## Java libraries

* [Apache Commons](https://en.wikipedia.org/wiki/Apache_Commons) for utility functions and classes.

* [Guava](https://en.wikipedia.org/wiki/Google_Guava) for additional data structures and algorithms.

* [VavR](https://www.vavr.io/) for additional functional programming constructs.

* [JUnit 4](https://junit.org/junit4/) and [Mockito](https://site.mockito.org/) for testing.

{% include links.html %}