---
title: IRenderable
description: Unifying a render call between elements
---

## Description

The IRenderable interface aims to provide a unifyed function `Render()` which 
must be implemented by inhertors. 

The idea of this function is that should be in such a way that 
it is **[idempotent](https://en.wikipedia.org/wiki/Idempotence)**.

## Examples

```csharp title="Simple UI Example"
// somewhere inside a valid layout
SpacerComponent spacer = UI.Spacer(new HorizontalSpacerBehaviour());

// later on, re-trrigger the spacer expansion when something has changed 
// forcing it to re-expand or contract
spacer.Render();
```

## References

This interface is implemented by: [`SpacerComponent`](../components/layouts/spacer-component.md), [`AbstractViewComponent`](../components/views/abstract-view-component.md).

## Implementation

<div align="center">
:::note

[**IRenderable.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Interface/IRenderable.cs)

::: 
</div>
