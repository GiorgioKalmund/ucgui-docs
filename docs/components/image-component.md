---
sidebar_position: 3
title: ImageComponent
description: Uses Unity's UI.Image to display sprites
---

> extends [GraphicComponent\<ImageComponent\>]() implements [ICopyable\<ImageComponent\>](../interfaces/icopyable.md)


## Description

The ImageComponent is one of the foundational elements of UCGUI.\
It makes use of the [UnityEngine.UI.Image](https://docs.unity3d.com/2018.2/Documentation/ScriptReference/UI.Image.html) and offers all kinds of customization options, similar to what you would expect to be able to do with it in the editor.

:::tip

Take a look at the [ImageService](../services/image-service.md) to programatically load
sprites into your user interface.

:::

## Properties

### DefaultSize
*protected* - Describes the default size this image should initialize with. You should propably use `Size(float, float)` though.

## Examples

```csharp title="Simple UI builder"
// Returns a simple image, attached to any hierarchy. 
UI.Image(_sprite).Parent(canvas);

// Additional specification of the image type
// in the builder and additional ppum config.
UI.Image(_sprite, Image.Type.Sliced)
    .PixelsPerUnitMultipler(0.2f)
    .Parent(canvas);
```


```csharp title="Fluent Pattern!"
UI.Image(_sprite)
    .Filled(FillMethod.Horizontal, 0.5f) // Defined in ImageComponent 
    .Color(UnityEngine.Color.purple) // Defined in GraphicComponent
    .Alpha(0.1f) // Defined in GraphicComponent
    .OffsetX(200) // Global BaseComponent extension
    .Parent(canvas); // Global BaseComponent extension
```

## References

This component is referenced or inherited by: [`AbstractViewComponent`](), [`InputComponent`](input-component.md), 
[`LabelComponent`](./label-component.md), [`LayoutComponent`](./layouts/layout-component.md), [`ScrollViewComponent`](), [`SliderComponent`](slider-component.md).

## Implementation

<div align="center">
:::note

[**ImageComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/ImageComponent.cs)

::: 
</div>
