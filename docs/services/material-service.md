---
sidebar_position: 3
title: MaterialService
description: Loading materials at runtime
---

## Description

The MaterialService aims to provide programatic access to materials for you user 
interface at runtime.

:::tip

`GetMaterial` defaults to searching in `"/Assets/Resources/Materials/"`, however you can change the default parent folder to not be "Materials/" by passing the name of a folder as a second parameter.

:::

## Examples

```csharp title="Material Service"
// load material and apply it to an image
Material glowMaterial = MaterialService.GetMaterial("glow");

UI.Image(_blobSprite).Material(glowMaterial);
```

## Implementation

<div align="center">
:::note

[**MaterialService.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Service/MaterialService.cs)

::: 
</div>

