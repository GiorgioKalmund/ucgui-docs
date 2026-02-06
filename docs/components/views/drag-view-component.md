---
sidebar_position: 3
title: DragViewComponent
description: A view which be dragged around, optionally inside a confined area
---

> extends [AbstractViewComponent](./abstract-view-component.md) 

## Description

The DragViewComponent is a simple view which can additionally be dragged around in a confined, or unconfined area.
It acts just like an [empty view](./abstract-view-component.md) otherwise.

Simply make use of the `Bounds` function to create an arbitrarily sized and position rectangle which act as bounds for movement.
By default the DragView will collide on all four sides directly and thus cannot cross the border in any direction.

## Examples

For a simple and non-reusable view, there is a built-in shorthand.
If you already have existing static views simply add a 'Drag' prefix to the builder to make it draggable:

```csharp title="Simple UI Builder"
// anonymous view
UI.DragView(canvas, v => { // optionally directly link to canvas
    v.Add(
        UI.Image(_iceCreamCone)
            .Pivot(PivotPosition.UpperLeft)
            .Offset(20, -20)
        ,
        UI.Text("Sam's Ice Cream")
            .Pivot(PivotPosition.UpperLeft, true)
            .Offset(120, -20),
        // ...
    );
    v.Bounds(new Vector2(_boundsWidth, _boundsHeight));
}).Size(_width, _height);
```
However for more complex and reusable scenarios you might want to store the contents somewhere in a dedicated class:

```csharp title="Custom View Example"
using UCGUI;

class MyViewComponent : DragViewComponent
{
    private TextComponent title
    private string titleString = "Lil Whip's Ice Cream";

    // create initial configuration durig 'Awake'
    protected override void Create() { 
        base.Create(); // always call base first

        ImageComponent iceLogo = UI.Image(_iceCreamCone)
            .Pivot(PivotPosition.UpperLeft)
            .Offset(20, -20)
            .Parent(this);

        UI.Text(titleString)
            .Pivot(PivotPosition.MiddleLeft, true)
            .OffsetX(20)
            .Parent(iceLogo);

        // ...

        this.Size(600, 800);
    }

    // apply additional configuration during 'Start'
    protected override void Initialize() {

    }
    
    // called every time the view opens
    public override void Render() { 
        // even though the DragViewComponent render call is empty, 
        // it is good habit to call it here in case it changes
        base.Render(); 

        titleString = GetTitleString();
        title.Text(titleString);
    }
}
```


## Implementation

<div align="center">
:::note

[**DragViewComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/DragViewComponent.cs)

::: 
</div>
