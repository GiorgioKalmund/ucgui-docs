---
sidebar_position: 5
title: ButtonComponent
description: A simple button based on the LabelComponent
---

> extends [LabelComponent](./label-component.md) implements [IStylable\<ButtonComponent, ButtonStyle\>](../interfaces/istylabe.md), [ICopyable\<ButtonComponent\>](../interfaces/icopyable.md), [IFocusable](../interfaces/icopyable.md)

## Description

A button is essential to any user interface. The ButtonComponent makes use of the [UnityEngine.UI.Button](https://docs.unity3d.com/2018.2/Documentation/ScriptReference/UI.Button.html) under the hood for integrated functionality for most user interactions.

Implementing `IStylable<ButtonComponent, ButtonStyle>` also allows for easy and reusable styling of your button. 
With the Button inheriting from the Label, this means that all [label styles](./label-component.md) are also applicable to the Button!

## Examples

```csharp title="Simple UI Builder"
UI.Button("Click me!", () => {
    // ... execute code on click of the button
});
```

The button also supports and optional `label` call which allows for initialization with 
an image:

```csharp title="Label Builder"
UI.Button(() => {
    // ... action
}, label => {
    label.Label("Click me!", _pointerSprite);
})
.Style(LabelStyle.IconOnly); // inhertied support for label styles
.Padding(20); // apply padding of 20 to all sides
```

## Implementation

<div align="center">
:::note

[**ButtonComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/ButtonComponent.cs)

::: 
</div>
