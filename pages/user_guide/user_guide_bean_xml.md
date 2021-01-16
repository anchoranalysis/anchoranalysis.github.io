---
title: "User Guide - BeanXML"
tags: [getting_started]
keywords:
sidebar: user_guide_sidebar
permalink: user_guide_bean_xml.html
folder: user_guide
---

## What is BeanXML?

BeanXML is a type of XML used by Anchor to define experiments, configuration and many aspects of behaviour. It is flexible and extensible, and can easily be used with new types of plugins and other objects, as they are developed and added to Anchor.

{% include note.html content="Understanding XML is a prerequisite for BeanXML. Each BeanXML file describes values to create a [Java-class](developer_guide_anchor_beans.html). However, understanding Java is not necessary if a bean is well-documented; otherwise a basic knowledge is useful. " %}

## Structure of BeanXML

### Rules

Some rules apply:
- BeanXML is sub-divided into units called AnchorBeans, each described by an XML element.
- It always has the following structure `<config><bean>...</bean></config>` where the `<bean>` element describes the top-level AnchorBean.
- Each AnchorBean has a necessary attribute `config-class='xxxxx'` where **xxxxx** is the fully-qualified name of a Java class. This class accepts particular properties (nested and non-nested).

### Types of properties

![beanxml.png](/images/anchor_beans/beanxml.png)

Two types of properties can be specified in a bean:

1. **Non-nested property** - primitives (integer, double, boolean etc. - and String) can be defined as an XML element's attribute.
2. **Nested property** - defined as an element inside the definition of the containing element.

It follows that any bean in 2. must also be an AnchorBean. A tree forms of nested-beans who exist as properties of each other.

## What properties are available?

### Sources of documentation

To understand the available properties in a bean:
1. Documentation in the user-guide.
2. Any examples in guides or in existing BeanXML.
3. The Java source-code for a Bean for the respective `config-class` attribute.

{% include note.html content="The Java source-code for particular classes are stored in GitHub in a [particular predictable location](/developer_guide_anchor_beans.html#locatingSource), as can be inferred from the `config-class` value." %}

### Choice of beans

Two situations are common:
- Only **one specific** AnchorBean can exist in a particular property.
- A **choice exists** of possible AnchorBeans in a particular property - so long the bean **inherits** from a particular base bean.

### Inheritance

By **inherits**, we refer to a concept from object-oriented programming, where a **subclass** is as an expanded version of a **parent class**. The subclass includes all properties from the parent, and adds some more.

**insert more instructions**

{% include note.html content="This relates closely to a computer science principle called *polymorphism*." %}


## Special beans
Some special beans exist via custom-factories to perform common useful tasks. In these cases, in addition to the usual `config-class`, a `config-factory` must also be specified in the XML element.

| Factory Name | Registered *config-factory* | Purpose
|--------------|-----------------|--------
| `ListBeanFactory` | list | for creating a List of items (itself not a bean!)
| `StringSetFactory` | stringSet | for creating sets of strings (itself not a bean!)
| `IncludeBeanFactory` | include | defines a bean in an external file
| `ReplacePropertyBeanFactory` | replaceProperty | defines a bean in an external file

### Lists of beans

```xml
<list config-class="java.util.List" config-factory="list">
    <item config-class="org.anchoranalysis.bean.shared.regex.RegExSimple" matchString="*_red.tif$"/>
    <item config-class="org.anchoranalysis.bean.shared.regex.RegExSimple" matchString="*_blue.tif$"/>
</list>
```

### String sets

```xml
<datasets config-class="org.anchoranalysis.bean.StringSet" config-factory="stringSet">
    <item>jan30</item>
    <item>feb05</item>
    <item>feb16</item>
</datasets>
```

### Include (another BeanXML file)

The `config-class` should be identical to the Bean which is being included.

```xml
<input filePath="inputManager.xml" config-class="org.anchoranalysis.io.bean.input.InputManager" config-factory="include"/>
```

### Replace (a property with an alternative value)

The `config-class` should be identical to the Bean whose property is being replaced.

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

## Developer documentation

More detailed technical knowledge of BeanXML can be found in the [developer documentation](developer_guide_anchor_beans.html).

{% include links.html %}
