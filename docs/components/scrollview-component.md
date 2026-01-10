---
sidebar_position: 8
title: ScrollViewComponent
description: Scroll area based on Unity's ScrollView component
---

> extends [BaseComponent](./base-component.md) implements [IPointerEnterHandler](https://docs.unity3d.com/2019.1/Documentation/ScriptReference/EventSystems.IPointerEnterHandler.html), [IPointerExitHandler](https://docs.unity3d.com/2019.1/Documentation/ScriptReference/EventSystems.IPointerExitHandler.html), [IEnabled](../interfaces/ienabled.md)

## Description

The ScrollViewComponent is based on uGUI's [ScrollView](https://docs.unity3d.com/6000.2/Documentation/Manual/UIE-uxml-element-ScrollView.html). It offers a scrollable area
in both vertical and horizontal directions and can be configured to have a variety of 
scrolling behaviours.

## Examples

```csharp title="Simple UI Builder"
float spacing = 20f;
UI.ScrollView(ScrollViewDirection.Vertical, spacing, builder => {
    builder.Add(
        UI.Text("Top");
        UI.Image(_logoSprite);
        UI.Text("Lower");
    );
})
.ContentPadding(PaddingSide.All, 10)
.Size(_width, _height)
.Parent(canvas);
```

## Implementation

<div align="center">
:::note

[**ScrollViewComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/ScrollViewComponent.cs)

::: 
</div>
