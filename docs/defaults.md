---
sidebar_position: 8
title: Defaults
description: List of all default values used for various UCGUI components.
---

## Description

The [Defaults file](https://github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Support/Defaults.cs) contains a number of various static 
members for some UCGUI components.

## Text

### GlobalFont - `TMP_FontAsset`

> null

Accessor for `TextComponent.GlobalFont`. 
The specified font will be used for every instantiated text. 
If not overridden.

### DefaultSize - `Vector2`

> Vector2(100, 100)

The size a text should be if no size is specified. 
Defaults to Unity's convention of 100 x 100.

## Image

### DefaultSize - `Vector2`

> Vector2(100, 100)

The size an image should be if no size is specified. 
Defaults to Unity's convention of 100 x 100.

## Spacer

### AlternateDirectionExtents - `float`

> 25f

The default width or height of the spacer into its non-stretching dimension.

## Focus

### DefaultGroup - `string`

> "ucgui-focus-group-default"

The default group to use as fallback. 
Every IFocusable member will automatically be part of this group if
not specified otherwise using `IFocusable.FocusGroup`.

## View

### StartsOpen - `bool`

> false

Whether the view should start open by default (after creation).


### DefaultBackdropColor - `UnityEngine.Color`

> UnityEngine.Color.clear

Default backdrop color of the view.

## View

### MissingTexture2DLocation - `string`

> "missing"

Path to a Texture(2D) which should be displayed if a path is unavailable.
Defaults to 'Assets/Resources/Textures/\{location\}(.png)' when using image service **direct Sprite** access,
otherwise simply 'Assets/Resources/\{location\}(.png)' when using **direct Texture2D** loading.

## Screen

### ReferenceResolution - `Vector2` 

> Vector2(1920, 1080)

Reference resolution value. This can be used to dynamically scale your UI based on the real
resolution of the device the program is running on. Used to calculate `GUIService.WidthScale`
and  `GUIService.HeightScale`.

## Debug

### DebugWhite - `GUIStyle`

> FontSize: 14, Color: UnityEngine.Color.white

### DebugBlack - `GUIStyle`

> FontSize: 14, Color: UnityEngine.Color.black

### DebugRed - `GUIStyle`

> FontSize: 14, Color: UnityEngine.Color.red
