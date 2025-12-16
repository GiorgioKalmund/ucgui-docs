---
sidebar_position: 2
title: TextComponent 
description: Based on TextMeshPro
---

> extends [GraphicComponent\<TextComponent\>]() implements [ICopyable\<TextComponent\>](), [IStylable\<TextComponent\>]()

## Description

The TextComponent is one of the foundational elements of UCGUI.\
It builds on [TextMeshPro's text component](https://docs.unity3d.com/Packages/com.unity.ugui@2.0/manual/TextMeshPro/index.html) and offers all kinds of customization options, similar to what you would expect to be able to do with it in the editor.

## Functions
### `Text(...)`
Sets the text the component displays. Can either take in a string or an integer.\
For floats or other types please use format strings or their respective `ToString()` method.

Has various overrides which also allow to set a `TextMode` which can either by `Additive` or `Normal`, either adding onto the string or replacing it completely.


### `Clear()`
Clears the text by setting it to an empty string.

### `Font(TMP_FontAsset)`
Sets the font of this specific text instance.

:::tip

If you want to change your global font either call `TextComponent.GlobalFont(TMP_FontAsset)` or use set it directly via the defaults: `Defaults.Text.GlobalFont`. This has to be done **before** any text is instantiated.

:::

### `FontSize(float)`
Sets the font size.

### `GetText() : string`
Returns the current text contents of the TextMeshPro element.


### `AutoSize(float?, float?, bool?)`
Sets the optional `min` and `max` font sizes and enables the corresponding functionality for the TextMeshPro component. The `active` bool optionally sets whether auto sizing is enabled.

### `Alignment(TextAlignmentOptions)`
Sets the horizontal alignment options for the TextMeshPro component.

#### `AlignCenter()`
Shorthand for aligning the text to the center horizontally.

### `VAlignment(VerticalAlignmentOptions)`
Sets the vertical alignment options for the TextMeshPro component.

#### `VAlignCenter()`
Shorthand for aligning the text to the center vertically.

### `OverflowMode(TextOverflowModes)`
Sets the overflow behaviour of the text. 

### `WrappingMode(TextWrappingModes)`
Sets the wrapping behaviour of the text. 

#### `NoWrap()`
Shorthand for setting the `NoWrap` text wrapping mode.

### `FontStyle(FontStyles)`
Adds the given style to the existing ones. 

#### `Bold()`
Shorthand for making the font bold.

#### `Italic()`
Shorthand for making the font italic.

#### `Underline()`
Shorthand for making the text underlined.

### `FontStyleRemove(FontStyles)`
Removes the given style from the existing ones. 

### `Margin(RectOffset)`
Sets the TextMeshPro text component's built in margins. 

### `FitToContents(bool?, ScrollViewDirection?)`
Sets mesh's `autoSizeTextContainer` to the provided `fit` bool which defaults to **true**. 
Additionally adds a `ContentSizeFitter` in the provided direction which defaults to `Horizontal`.

### `GetGraphic() / GetTextMesh() : TextMeshProUGUI`
Returns the connected TextMeshPro text component. 
> `GetGraphic()` is required because the `TextComponent` inherits from `GraphicComponent`, however `GetTextMesh()` is a clearer name, thus currently exists as well ;) 

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
    .Parent(canvas) // Global BaseComponent extension
```

## References

This component referenced or inherited by: [`LabelComponent`](), [`InputComponent`]().


## Implementation

<div align="center">
:::note

[**TextComponent on GitHub**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/TextComponent.cs)

::: 
</div>
