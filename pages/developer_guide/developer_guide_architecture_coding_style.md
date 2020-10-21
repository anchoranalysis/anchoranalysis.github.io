---
title: "Architecture - Coding Style"
tags: [architecture]
keywords: architecture, packages
sidebar: developer_guide_sidebar
permalink: developer_guide_architecture_coding_style.html
folder: developer_guide
---

## General Principles

Authored by: Owen Feehan

### DRY 

[Do not repeat yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). By eliminating duplication in code, the code becomes better structured and is easier to understand and maintain. [SonarQube](developer_guide_environment_sonarqube.html) automatically checks for duplicated code patterns.

{% include warning.html content="Don't WET (write everything twice) unless there is a strong mitigating circumstances, as it is just deferring and increasing deduplication effort for the next developer - who may not even realise the preexisting duplication." %}

### Encapsulate enthusiastically

Hide as much internal detail with private methods and classes, so only the necessary external interfaces between components are apparent. The encapsulation should occur on each of a function / class / package level.

### Keep functions small

{% include tip.html content="A function should do one clear thing, and not two. An ideal function can be understand in a matter of seconds, because it is <10 lines of code, and detail has been hidden elsewhere." %}

- Bury detail in *private* helper functions, which are called from a function expressing higher-level logic.
- Prefer many small functions to few large functions, but also keep classes small, by factoring out methods to helper classes, and packages small by splitting them up if they grow large.

Strive for [high cohesion and low coupling](https://stackoverflow.com/questions/14000762/what-does-low-in-coupling-and-high-in-cohesion-mean).

### Use polymorphism for alternative operations

Avoid switch-cases or flags in favour of abstract-base-classes. Apply [SOLID](https://en.wikipedia.org/wiki/SOLID) design principles, especially dependency inversion.
 
Instantiating abstract-base-classes via [BeanXML](/user_guide_bean_xml.html) is encouraged to give inversion-of-control and dependency injection, but not for minor detail. Every polymorphic class does **not** need to be an [AnchorBean](/developer_guide_anchor_beans.html).  

### Commenting

Document parameters to `public` interfaces rigorously and systematically (not always obeyed at present!), but private functions only partially or not at all, as best judgment allows.

Creating a small function with a clear understandable name is preferable to a comment above several lines of code.

### Avoid premature optimization

Parts of the codebase suffer from being in Java instead of native code, or could be made performance at the expense of cleaner code. But these are rare, and should be tackled only when clearly necessary.

### Testing

The more tests the better, but coverage is currently low on Anchor's (large) code base. Concentrate and enhance coverage around problematic areas, especially after a bug-fix.

## Java-specific

### Use `Optional` instead of nullable variables.

Prefer to avoid variables that can be null in favour of [Optional](https://www.oracle.com/technical-resources/articles/java/java8-optional.html).

**Strongly** avoid nullable-variables in function interfances (arguments in and out of a function). When deviating from this rule, very clearly document it in the `Javadoc`.

### Prefer functional-style inside classes.

Prefer immutable data structures, and functions without side-effects, unless it clashes with the design of a system component or a third-party library, or creates an impactful performance penalty.

The `final` keyword can be useful to indicate immutable variables, but it's good to generally indicate that class/function is immutable in its `Javadoc`.

{% include warning.html content="Note that some parts of Anchor interact with third-party-libraries that use nullable functions. Please document clearly these circumstances." %}

## Python-specific {#python}

### Type-hints

Always use Python's [type-hints](https://docs.python.org/3/library/typing.html) to document the type of each argument in and out of functions. It helps create understandable code and provides for a certain amount of automated checking at build time.

### Docstrings

Use [sphinx-style](https://sphinx-rtd-tutorial.readthedocs.io/en/latest/docstrings.html) docstrings.

### Prefer `from package import` style for internal modules

Avoid needlessly exposing package-internal functions and classes by:
- prefixing functions and filenames with `_` 
- exposing only where needed functions/classes outside the packages via the package's ``__init__.py`` (also in a nested way between hierarchies of sub-packages).
- `__all__` if it helps.

This means internal packages should only ordinarily be imported via `from package import` and not `import package` as the former uses the ``__init__.py``.

## R-specific

### Use `.` as a prefix for private functions

The `R` language does not have any equivalent of `private` for only-internally-used functions. As a workaround, prefix such a function conventionally with a period. This promises only be called from the current source-file. e.g.

```R
.some_private_function <- function() {
	# Function contents
}
```

{% include links.html %}
