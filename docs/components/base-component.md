---
sidebar_position: 1.5
title: BaseComponent
description: UCGUI's foundation
---

> extends [MonoBehaviour](https://docs.unity3d.com/6000.3/Documentation/ScriptReference/MonoBehaviour.html)

## Description

The BaseComponent is the foundation for UCGUI's component system.

Building on top of Unity's MonoBehaviour the BaseComponent provides access to many core 
elements required for configuring your user interfaces.

For example, `GetRect()` gives you access to a reference to the [RectTransform](https://docs.unity3d.com/6000.3/Documentation/ScriptReference/RectTransform.html) of 
the object. `IgnoreLayout()` adds a [LayoutElement](https://docs.unity3d.com/2018.1/Documentation/ScriptReference/UI.LayoutElement.html) behaviour and sets it to 'Ignore Layout'. This is especically useful if 
you want to directly parent an object to another object which contains some fort of layout (i.e. [horizontal](./layouts/hstack-component.md) or [vertical](./layouts/vstack-component.md))
and you do want your element remain independent of such alignment. 

The BaseComponent serves as the most low-level and light-weight element in UCGUI. If you are in need of an easily customizable MonoBehaviour you can use the BaseComponent 
for quick control over rect properties like size, position, anchors etc.

:::tip

As UCGUI makes use of the [Fluent Interface pattern](https://en.wikipedia.org/wiki/Fluent_interface) having general purpose 
methods in a non-generic class would lead to loads of casting between classes. 
Therefore, UCGUI additionally makes use of [CSharp's Extension Classes](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods)
to make these generically available when working with any class inheriting from BaseComponent.

These are all stored in [a separate file](https://github.com/GiorgioKalmund/UCGUI/blob/main/Runtime/Components/Support/UI.cs).

::: 

## Implementation

<div align="center">
:::note

[**BaseComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/BaseComponent.cs)

::: 
</div>

