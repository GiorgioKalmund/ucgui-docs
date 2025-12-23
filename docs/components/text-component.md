---
sidebar_position: 2
title: TextComponent 
description: Based on TextMeshPro
---

> extends [GraphicComponent\<TextComponent\>]() implements [ICopyable\<TextComponent\>](../interfaces/icopyable.md), [IStylable\<TextComponent, TextStyle\>](../interfaces/istylabe.md)

## Description

The TextComponent is one of the foundational elements of UCGUI.\
It builds on [TextMeshPro's text component](https://docs.unity3d.com/Packages/com.unity.ugui@2.0/manual/TextMeshPro/index.html) and offers all kinds of customization options, similar to what you would expect to be able to do with it in the editor.

:::tip

If you want to change your global font either call `TextComponent.GlobalFont(TMP_FontAsset)` 
or use set it directly via the defaults: `Defaults.Text.GlobalFont.`
This has to be done before any text is instantiated.

:::

## Examples

```csharp title="Simple UI builder"
// Returns a simple text, which is not attached to any hierarchy. 
UI.Text("Hello, World!");

// Integrating the text into the hierarchy and
// making use of the optional `color` parameter for the builder.
UI.Text("Hello, Mars!", Color.blue)
    .Parent(canvas);
```


```csharp title="Fluent Pattern!"
UI.Text("Hello, Mercury!")
    .FontSize(72) // Defined in TextComponent
    .Color(UnityEngine.Color.purple) // Defined in GraphicComponent
    .Alpha(0.1f) // Defined in GraphicComponent
    .OffsetX(200) // Global BaseComponent extension
    .Parent(canvas); // Global BaseComponent extension
```

## References

This component is referenced by: [`LabelComponent`](./label-component.md), [`InputComponent`]().


## Implementation

<div align="center">
:::note

[**TextComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/TextComponent.cs)

::: 
</div>
