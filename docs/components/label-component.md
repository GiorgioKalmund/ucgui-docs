---
sidebar_position: 4
title: LabelComponent
description: Flexible text with an attached graphic.
---

> extends [SwitchLayoutComponent\<LabelComponent\>](), [IStylable\<LabelComponent, LabelStyle\>](), [ICopyable\<LabelComponent\>]()

## Description

The Label is a very simple yet powerful component. It consists of one [image](./image-component.md)
and one [text](./text-component.md) which can be arranged in a variety of ways.

As it extends the [SwitchLayout]() text and image can be arranged both vertically 
and horizontally, as well as reverse their order. It also automatically fits to its content
in both directions. 

There some native `LabelStyle`s which allow for easy customization:
1. `IconAndText` (Default)
2. `IconOnly` 
3. `TextOnly` 
4. `Hidden`

These can be set using `.Style(LabelStyle)`.

Using the provided `UI` initializers the text comes first (on the left side)
and it is then followed by the image. 

:::tip
A neat thing about labels is that they only create the required elements if they are
actually being used. So if your label doesn't contain an image (*essentially just a text again*)
, no additional GameObject for the image is created. Only by explicitly setting the 
`text` and `image` variables the respective objects are created. 

**See the third example below.**
:::

## Examples

```csharp title="Simple UI Builder"
// ---- []
UI.Label("Hello, World!", _globeSprite);

// [] ----
UI.Label("Hello, Mars!", _alienTexture2D).ReverseArrangement();

// ----
var label = UI.Label("Hello!"); // no GameObject for the image has been created yet ...
label.image.Sprite(_cowSprite); // ... only HERE it is instantiated and configured
label.text.Text("Hello, Mercury!"); 
```

:::note

The initializer for `UI.Label()` supports both `Sprite` and `Texture2D`, as well as
no image at all!

:::

## Implementation

<div align="center">
:::note

[**LabelComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/LabelComponent.cs)

::: 
</div>
