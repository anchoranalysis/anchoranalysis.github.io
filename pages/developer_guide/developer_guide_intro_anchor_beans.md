---
title: "Introduction - Anchor beans"
tags:
keywords: beans
sidebar: developer_guide_sidebar
permalink: developer_guide_intro_anchor_beans.html
folder: developer_guide
---

## What is an AnchorBean?

1. It is a [JavaBean](https://en.wikipedia.org/wiki/JavaBeans), subject to all the official conventions.
2. It inherits form the class *AnchorBean*
3. The fields which define bean properties are additionally annotated with @BeanField.
4. Serveral additional annotations are possible: @Optional @NonEmpty etc.

## Why use AnchorBeans?

1. To seperate the implemention of algorithms from their parameterization.
2. To allow for easy serialization of configuration back and forth to XML.
3. To have a core-object model that implements certain repeated functionality (initialization, duplication) that occurs commonly in the platform.
4. To keep a record of the parameters and algorithms used (for scientific record keeping).
5. For all the above happen, without holding back rapid ongoing development i.e. the cost of adding new code-features must be kept small, as image analysis usually involves lots of prototyping.

By encoding configuration in seperate XML files, this allows the user to change application beaviour (substantially) without recompiling any Java code. The user may change configuration settings, define new experimental pipelines, modify existing pipelines, tweak parameters etc., all without compiling and Java code.

This approach implements principles of [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection) and [Inversion of Control](https://en.wikipedia.org/wiki/Inversion_of_control), similarly to the [Spring Framework](https://en.wikipedia.org/wiki/Spring_Framework) (but simplified).

## Anchor BeanXML

BeanXML is a basic XML standard for defining AnchorBeans, which just uses the [Apache Commons Configuration](https://commons.apache.org/proper/commons-configuration/) framework for serializing beans.

![beanxml.png](/images/anchor_beans/beanxml.png)

**N.B. Please read and understand this guide to [Declaring and Creating Beans](https://commons.apache.org/proper/commons-configuration/userguide/howto_beans.html) before proceeding.**

### Types of properties

Two types of properties can be specified in a bean:

1. **Non-nested property** - simple primitives (String, integer, double, boolean, etc.) can be defined as an XML element's attribute.
2. **Nested property** - defined as an element inside the definition of the containing element.

It follows that any bean in 2. must also be an AnchorBean. A tree forms of nested-beans who exist as properties of each other.

When certain operations are executed (duplication, configuration-checks etc.), they occur not only on the bean itself, but **recursively** on all its child properties i.e. duplicate() is a deep-copy not a shallow-copy

### Special beans
We additionally add some special beans via custom-factories that make our life easier e.g.

| Factory Name | Registered *config-factory* | Purpose
|--------------|-----------------|--------
| `ListBeanFactory` | list | for creating a List of items (itself not a bean!)
| `StringSetFactory` | stringSet | for creating sets of strings (itself not a bean!)
| `IncludeBeanFactory` | include | defines a bean in an external file
| `ReplacePropertyBeanFactory` | replaceProperty | defines a bean in an external file

The specific factory is specified as an attribute *config-factory* on the BeanXML declaration.

#### Lists of beans

```xml
<list config-class="java.util.List" config-factory="list">
	<item config-class="org.anchoranalysis.bean.shared.regex.RegExSimple" matchString="*_red.tif$"/>
	<item config-class="org.anchoranalysis.bean.shared.regex.RegExSimple" matchString="*_blue.tif$"/>
</list>
```

#### String sets

```xml
<datasets config-class="org.anchoranalysis.bean.StringSet" config-factory="stringSet">
	<item>jan30</item>
	<item>feb05</item>
	<item>feb16</item>
</datasets>
```

#### Include (another BeanXML file)

```xml
<input filePath="inputManager.xml" config-class="org.anchoranalysis.io.bean.input.InputManager" config-factory="include"/>
```

#### Replace (a property with an alternative value)

```xml
<!-- Changes the end attribute (non-nested-property) -->
<bean config-class="org.anchoranalysis.bean.shared.SequenceInteger" key="end" replacement="10" config-factory="replaceProperty">
	<item config-class="org.anchoranalysis.bean.shared.SequenceInteger" start="1" end="5"/>
</bean>
```

```xml
<!-- Replaces the 'calculateLevel' bean nested-property on a thresholder -->
<bean
    config-class="org.anchoranalysis.image.bean.threshold.ThresholderGlobal"
    key="calculateLevel" config-factory="replaceProperty">

    <item
        config-class="org.anchoranalysis.image.bean.threshold.ThresholderGlobal">
        <calculateLevel
            config-class="org.anchoranalysis.image.bean.threshold.calculatelevel.Otsu" />
    </item>

    <replacement level="20"
        config-class="org.anchoranalysis.image.bean.threshold.calculatelevel.Constant" />
</bean>
```

### Important prior step before usage

Code must always first call [RegisterBeanFactories](https://github.com/anchoranalysis/anchor/blob/master/anchor-bean/src/main/java/org/anchoranalysis/bean/xml/RegisterBeanFactories.java)`.registerAllPackageBeanFactories()` before loading any beans. This registers the additional-factories, and a replacement default factory ([AnchorDefaultBeanFactory](https://github.com/anchoranalysis/anchor/blob/master/anchor-bean/src/main/java/org/anchoranalysis/bean/xml/factory/AnchorDefaultBeanFactory.java)).

### Initializable beans

Certain types of beans require initialization-parameters before they can be used. These beans should derive from [InitializableBean](https://github.com/anchoranalysis/anchor/blob/master/anchor-bean/src/main/java/org/anchoranalysis/bean/init/InitializableBean.java), which provides helpful methods for recursively initializating a bean and all its nested children.

The type of parameter is application-dependent, and typically another abstract-base-class will subclass *InitializableBean* and specify both the parameter-type and some further interfaces.

### Package namespaces in JARs

By convention, Anchor beans are always stored within a package `bean` in the root namespace of the JAR e.g.

- org.anchoranalysis.image.**bean**.threshold.ThresholderGlobal
- org.anchoranalysis.**bean**.StringSet
- org.anchoranalysis.image.**bean**.unitvalue.distance.UnitValueDistanceVoxels


{% include links.html %}
