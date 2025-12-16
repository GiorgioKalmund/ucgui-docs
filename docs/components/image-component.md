---
title: ImageComponent
description: Uses Unity's UI.Image to display sprites.
---

> extends [GraphicComponent\<ImageComponent\>]() implements [ICopyable\<ImageComponent\>]()


## Description

The ImageComponent is one of the foundational elements of UCGUI.\
It makes use of the [UnityEngine.UI.Image](https://docs.unity3d.com/2018.2/Documentation/ScriptReference/UI.Image.html) and offers all kinds of customization options, similar to what you would expect to be able to do with it in the editor.


## Properties

### DefaultSize
> *protected*

Describes the default size this image should initialize with. You should propably use `Size(float, float)` though.

## Functions

### `Sprite(...)`
Sets the sprite of the image. Can be called with a ton of differnt initializers. 

### `Clear()`
Clears the currently set sprite by setting it null. This will display the default null sprite.
*If you want your image to actually not be visible either call `ToggleVisibility()`
or `Enabled(false)`.

### `NativeSize(Vector2)`
Sets the component's size to a multiple of the sprite's native size.

### `GetNativeSize() : Vector2`
Returns the native size of the current sprite (in pixels).

### `ImageType(Image.Type)`
Sets the [Image.Type](https://docs.unity3d.com/2018.1/Documentation/ScriptReference/UI.Image.Type.html) of the image.

### `Filled(Image.FillMethod, float?)`
Sets the [Image.FillMethod](https://docs.unity3d.com/2019.1/Documentation/ScriptReference/UI.Image.FillMethod.html) 
with an optional value for the amount which defaults to 1.\
Automatically also sets the image type to `Filled`.

### `FillAmount(float)`
Sets the fill amount of the image. 

### `PixelPerUnitMultiplier(float)`
Sets the pixels per unit multiplier of the image. This especially useful for images which
have the type `Sliced`.

### `GetGraphic() / GetImage() : Image`
Returns the underlying `UnityEngine.UI.Image`.

### `HasImage() : bool`
Whether the sprite is null or not.

### `AddAnimator() : SpriteAnimator`
Adds an `SpriteAnimator` component to the GameObject.

### `GetAnimator() : SpriteAnimator`
Returns the attached `SpriteAnimator` component if one was previously added, else *null*.

## References

This component is referenced or inherited by: [`AbstractViewComponent`](), [`InputComponent`](), 
[`LabelComponent`](), [`LayoutComponent`](), [`ScrollViewComponent`](), [`SliderComponent`]().

## Implementation

<div align="center">
:::note

[**ImageComponent on GitHub**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/ImageComponent.cs)

::: 
</div>
