---
title: "Introduction - Anchor beans"
tags:
keywords: beans
sidebar: developer_guide_sidebar
permalink: developer_guide_anchor_beans.html
folder: developer_guide
---

## What is an AnchorBean?

1. It is a [JavaBean](https://en.wikipedia.org/wiki/JavaBeans), subject to all the official conventions.
2. It inherits form the class *AnchorBean*
3. The fields which define bean properties are additionally annotated with `@BeanField`.
4. Serveral additional annotations are possible: `@Optional` `@NonEmpty` etc.

## Why use AnchorBeans?

1. To separate the implementation of algorithms/components from their parameterization.
2. To allow for easy serialization of configuration back and forth to XML.
3. To have a core-object model that implements certain repeated functionality (initialization, duplication) across the platform.
4. To remember of the parameters and algorithms used (for scientific record keeping).
5. To facilitate rapid ongoing development i.e. the cost of adding new code-features must be kept small, as image analysis usually involves lots of prototyping.

By encoding configuration in separate XML files, this allows the user to change application behavior without recompiling. e.g. change configuration settings, define new experimental pipelines, modify existing pipelines, tweak parameters etc.

This approach implements principles of [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection) and [Inversion of Control](https://en.wikipedia.org/wiki/Inversion_of_control), similarly to the [Spring Framework](https://en.wikipedia.org/wiki/Spring_Framework) but simplified.

## Anchor BeanXML

BeanXML is a basic XML standard for defining AnchorBeans, which just uses the [Apache Commons Configuration](https://commons.apache.org/proper/commons-configuration/) framework for serializing JavaBeans to/from XML.

**N.B. Please read and understand the [user-guide to BeanXML](user_guide_bean_xml.html)**
 
For technical code-level details on BeanXML and Java please see the guide [Declaring and Creating Beans](https://commons.apache.org/proper/commons-configuration/userguide/howto_beans.html) before proceeding.

Additional Anchor-specific aspects are added to standard BeanXML. For example, when certain operations are executed (duplication, configuration-checks etc.), they occur not only on the bean itself, but **recursively** on all its child properties e.g. duplicate() is a deep-copy not a shallow-copy

### Important prior step before usage in code

Code must always first call [RegisterBeanFactories](https://github.com/anchoranalysis/anchor/blob/master/anchor-bean/src/main/java/org/anchoranalysis/bean/xml/RegisterBeanFactories.java)`.registerAllPackageBeanFactories()` before loading any beans. This registers the additional-factories, and a replacement default factory ([AnchorDefaultBeanFactory](https://github.com/anchoranalysis/anchor/blob/master/anchor-bean/src/main/java/org/anchoranalysis/bean/xml/factory/AnchorDefaultBeanFactory.java)).

### Initializable beans

Certain types of beans require initialization-parameters before they can be used. These beans should derive from [InitializableBean](https://github.com/anchoranalysis/anchor/blob/master/anchor-bean/src/main/java/org/anchoranalysis/bean/init/InitializableBean.java), which provides helpful methods for recursively initializating a bean and all its nested children.

The type of parameter is application-dependent, and typically another abstract-base-class will subclass *InitializableBean* and specify both the parameter-type and some further interfaces.

### Package namespaces in JARs

By convention, Anchor beans are always stored with `bean` in the **root package namespace** of the JAR e.g.

- org.anchoranalysis.image.**bean**.threshold.ThresholderGlobal
- org.anchoranalysis.**bean**.StringSet
- org.anchoranalysis.image.**bean**.unitvalue.distance.UnitValueDistanceVoxels

The namespace to the left of **bean** is the root package namespace.

## Locating the source-code for a particular bean {#locatingSource}

1. Read the bean-class from the `config-class` attribute
2. The relevant source-code repository can be inferred from the root package namespace (see above). (TODO insert link here!)
3. Follow the maven structure of `src/main/java/org/anchoranalysis/` etc. backwards along the package namespace to eventually locate the class.

{% include note.html content="Remember, a bean often inherits properties from parent-beans, so consider also all classes the bean inherits from." %}


{% include links.html %}
