---
sidebar_position: 1
title: ImageService
description: Loading of textures and sprites at runtime
---

## Description

The ImageService is probably the most important service for creating a user interface
with UCGUI. \
As the user has no visual editor to drag textures or sprites into ImageComponents, and 
with everything being created at runtime, there has to be a programatic way to load
images into your UI.

The ImageService supports loading of [Sprites](https://docs.unity3d.com/2018.2/Documentation/ScriptReference/Sprite.html) and [Textures](https://docs.unity3d.com/2018.2/Documentation/ScriptReference/Texture2D.html) as well an entire spritesheet assets.

:::important tip

In most cases you can make use of `.GetSprite(...)` to load a sprite. As most images
are usually stored as textures and not sprites in your Assets the Texture2D will first be automatically converted to a sprite and then returned to you as such.

However, if you are trying to explicitly load a sprite which is preconfigured (i.e. 
9-sliced, etc.) you **need** to make use of `.GetSpriteDirectly(...)` otherwise you
might run into some visual artifacts.

:::

:::tip

`GetSprite` and `GetSpriteDirectly` default to searching in `"/Assets/Resources/Textures/"`, however you can change the default parent folder to not be "Textures/" by passing the name of a folder as a second parameter into both functions.

:::


## Examples

```csharp title="Simple Image Example"
// easily retrieve sprites for your images
UI.Image(
    ImageService.GetSprite("ball")
);

// use direct access to maintain the configuration of sprites
UI.Image(
    ImageService.GetSpriteDirectly("sliced_rectangle")
)
.ImageType(Image.Type.Sliced)
.PixelsPerUnitMultiplier(0.3f);
```

## Implementation

<div align="center">
:::note

[**ImageService.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Service/ImageService.cs)

::: 
</div>
