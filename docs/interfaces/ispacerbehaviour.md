---
title: ISpacerBehaviour
description: Unifying access to Spacer behaviours
---

## Description

The ISpacerBehaviour interface aims to provide a unifyed function `Apply(SpacerComponent)` which must be implemented by inhertors. 

The goal of this interface is to allow an instance implementing it to
apply a certain configuration to a [Spacer](../components/layouts/spacer-component.md) after it has been created.

UCGUI supports two native behaviours: [HorizontalSpacerBehaviour](https://github.com/GiorgioKalmund/UCGUI/blob/main/Runtime/Components/Support/HorizontalSpacerBehaviour.cs)
and [VerticalSpacerBehaviour](https://github.com/GiorgioKalmund/UCGUI/blob/main/Runtime/Components/Support/VerticalSpacerBehaviour.cs)


## Examples

```csharp title="Simple UI Example"
// if inside a valid respective layout the spacer will either expand ...

// ... horizontally
var spacerH = UI.Spacer(new HorizontalSpacerBehaviour());

// ... or vertically 
var spacerV = UI.Spacer(new HorizontalSpacerBehaviour());

// ... or automatically choose the appropriate native behaviour
var spacerA = UI.Spacer();
```

## References

This interface is implemented by: [`HorizontalSpacerBehaviour`](https://github.com/GiorgioKalmund/UCGUI/blob/main/Runtime/Components/Support/HorizontalSpacerBehaviour.cs), [`VerticalSpacerBehaviour`](https://github.com/GiorgioKalmund/UCGUI/blob/main/Runtime/Components/Support/VerticalSpacerBehaviour.cs).

## Implementation

<div align="center">
:::note

[**ISpacerBehaviour.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Interface/ISpacerBehaviour.cs)

::: 
</div>
