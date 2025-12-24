---
sidebar_position: 4
title: GUIService
description: Quick access to Canvas and Camera related functionalities
---

## Description

The main purpose of the GUIService is to offer a shorthand for finding
the canvas and camera in the scene, as well as retrieving the canvas' properties.

:::warning

**This service might be removed in the future due to it being mostly useless. There 
exist cleaner and faster ways of achieveing the same things.**

:::

## Examples

```csharp title="GUI Service"

Canvas canvas = GUIService.GetCanvas()
Camera cam = GUIService.GetMainCamera()

// inside a screen 
public override Canvas GetCanvas()
{
    return GUIService.GetCanvas();
}
```

## Implementation

<div align="center">
:::note

[**GUIService.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Service/GUIService.cs)

::: 
</div>

