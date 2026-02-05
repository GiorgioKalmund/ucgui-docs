---
sidebar_position: 1
title: AbstractViewComponent
description: Base elements for all views 
---

> extends [ImageComponent](../image-component.md) implements [IRenderable](../../interfaces/irenderable.md)

## Description

The AbstractViewComponent acts as common denominator for all view-based components.

Views are components which, similar to [screens](../simple-screen.md), are meant to act as 
content holder for a hierarchy of elements. They support an identical `.Add(...)` call which parents
a given component to the view.

In constrast to screens, views are more dynamic. They can be 'opened' and 'closed', allowing them to only be visible at 
certain times.

Similar to the screen, a view requires a lifecycle handler to be implemented. For views the `Create()` handler must be overriden. 
It will called during the **Awake** phase of the Unity lifecycle.
\
*If you additionally need to configure some aspects of the view or their children in the 'Start' phase, simply override the default Unity 'Start' function.
You can learn more about how to work with the Unity lifecycle and UCGUI [here](../../getting-started/quickstart.md#interacting-with-the-unity-lifecycle).*
With these functions, similar to screens, you can create you interactive user interface!

:::tip

UCGUI defaults to having the initial state of views to be 'closed'. If you want to change this behaviour
simply adjust `Defaults.View.StartsOpen`.

:::

There are also native handlers for toggling opening and closing via an [InputAction](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.0/api/UnityEngine.InputSystem.InputAction.html) (helpful for example if you creating something like a pause menu), as well as 
UnityEvents you can listen to for when the view opens and closes.

[`Link(Canvas)`](#implementation) can be used to automatically parent the view to the canvas, as well as setting the internal `canvas` property.

The `Lock` and `Unlock` calls can be used to prevent opening and closing of a view.

:::important

`Render` is called **every time the view opens**. Use it to change anything about your view on re-opening instead of 
creating new views over and over again. You can imagine a view to be more of a potential template for any state which 
it can render when opened.

A view will **always bubble to the top of its hierarchy** when it opens.
:::

### Events

Any view has four native events tied to it.
Two for generic open and close:

1. `OnOpen`     - Fires every time the view transitions from being **closed** to being **open**.
2. `OnClose`    - Fires every time the view transitions from being **open** to being **closed**.

And another two for notifying when the view has become relevant inside of a [ViewStack](#ViewStack):

3. `OnStackReveal`  - Fires every time the view is part of a stack and has been **revealed by a pop**, i.e. is now on top of the stack.
4. `OnStackHide`    - Fires every time the view has been **hidden by a pushed** view, i.e. now directly under the top of the stack.

*But what even is a ViewStack? The following section will explain more about their behaviours and capabilities.*

## ViewStacks

ViewStacks act similar to a stack ([*the data structure*](https://en.wikipedia.org/wiki/Stack_(abstract_data_type))), in that they support the `Push` and `Pop` operations
for views, as well as a `Peek` to retrieve the upmost element. 

ViewStacks help you manage your flow and organization of views.
By **pushing** a view to the stack, the stack **automatically opens it** and **closes it when it is popped** from the stack.

Additionally there is a special version of popping from the stack using `PopUntil(AbstractViewComponent)`. This will keep on popping from the stack until 
a given view is reached (meaning it is at the top of the stack); if no matching element is present **no operation** will be performed.

To pop every element from the stack at once simply use `Collapse`.

## Examples

For a simple and non-reusable view, there is a built-in shorthand:

```csharp title="Simple UI Builder"
// anonymous view
UI.View(canvas, v => { // optionally directly link to canvas
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
}).Size(_width, _height);
```
However for more complex and reusable scenarios you might want to store the contents somewhere in a dedicated class:

```csharp title="Custom View Example"
using UCGUI;

class MyViewComponent : AbstractViewComponent
{
    private TextComponent title
    private string titleString = "Lil Whip's Ice Cream";

    // create initial configuration during 'Awake'
    public override void Create() { 
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
    public override void Initialize() {

    }
    
    // called every time the view opens
    public override void Render() { 
        titleString = GetTitleString();
        title.Text(titleString);
    }
}
```

## Implementation

<div align="center">
:::note

[**AbstractViewComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/AbstractViewComponent.cs)

::: 
</div>
