---
sidebar_position: 6
title: InputComponent
description: Text input based on TextMeshPro
---

> extends [ImageComponent](image-component.md) implements [IStylable\<InputComponent, InputStyle\>](../interfaces/istylabe.md), [IFocusable](../interfaces/ifocusable.md), [ICopyable\<InputComponent\>]()

## Description

The InputComponent is a neat wrapper around the [TextMeshPro TMP_InputField](https://docs.unity3d.com/Packages/com.unity.textmeshpro@2.0/api/TMPro.TMP_InputField.html).

It works quite analogously and mostly just offers a code-based access to all of the neccessary features.\
Built using [TextComponents](./text-component.md) it is very easy to customize the 
input field. 

:::note

All relevant fields and functions provided by the underlying `TMP_InputField` are
also provided via the InputComponent, however if you need more granular control 
`GetInput()` returns you the raw TextMeshPro component directly.

:::

Additionally the InputComponent makes use of the [IFocusable](../interfaces/ifocusable.md) interface, allowing for easy control flows when using them in combination with FocusStates.\
When an input is focused, Unity's underlying focused element also switches to the input, allowing for seamless transitions of where your input is displayed (*i.e. switching
between login fields*).

## Examples

```csharp title="Simple UI Builder"
InputComponent inputField = UI.Input("Your name here...")
.OnChanged(value =>
{
    // ... fluent style handler for change event
})
.OnSubmit(value =>
{
    // ... and submit event
})
.FontSize(20)
.Size(300, 50)
.Focusable(_state, UserName) // native support for FocusStates
.Parent(canvas);
```

## Implementation

<div align="center">
:::note

[**InputComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/InputComponent.cs)

::: 
</div>
