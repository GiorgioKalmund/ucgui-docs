---
sidebar_position: 1
title: Screens
description: Displaying your components via Screens
---

## Description

Before you take a closer look at what components even exist it is important to first
get an understanding of the philosophy behind UCGUI's instantiation process.

In the examples you seen before, as well as the ones which are to follow, the 
components always seem to be instantiated in some area or file which also has 
a reference to the canvas at the top of the hierarchy. \
It was also maybe unclear where you should exactly create these examples.

This is what [screens](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Screen/SimpleScreen.cs) are used for. Similar to how you would attach a [Canvas component](https://docs.unity.com/en-us/unity-studio/develop/ui-creator/canvas) to a GameObject to act as a root for you hierarchy, screens act as a root parent element for 
your UCGUI based UIs.

Screens enforce three methods:

1. `void Create()` - Called during the 'Awake' phase
2. `void Initialize()` - Called during the 'Start' phase
3. `Canvas GetCanvas()` - Returns a Canvas object which will act as a point of reference

The first two methods are the core elements of a screen. As the configuring your UI 
is strongly intertwined with the Unity lifecycle (*see the [Quickstart page](../getting-started/quickstart.md) for more information*), the screen offers two endpoints into which you can hook into both the 'Awake' and 'Start' phases.\
Inside of these hooks you can now simply create your desired user interface! 

:::important

When instantiating a new component to the screen you **need** to parent it to an existing element in the hierarchy. 
Inside any screen you have direct access to the `canvas` property which refernces the 
Canvas returned by your implemnentation of `GetCanvas()`. However, you can also simply
use the `this` reference for the `.Parent(...)` call and the object will then parent to the GameObject which the screen's script is attached to, not the overarching canvas.

:::

With this straight forward approach we can easily create a new screen for our first UI:

```csharp title="Screen Example"
using UCGUI;
using UnityEngine;

public class MyScreen : SimpleScreen
{
    TextComponent title;
    // Called during 'Awake'
    public override void Create()
    {
        title = UI.Text("Hello")
                  .Parent(this);
        
        ImageComponent image = UI.Image(ImageService.GetSprite("penguin"))
                                 .OffsetY(-100)
                                 .Parent(title);
        
        // ... Create more UI here
    }
    
    // Called during 'Start'
    public override void Initialize()
    {
        // ... Additionally configure your UI here
        title.Text(", World!", TextMode.Additive);
    }
    
    // Every screen has a direct reference to the Canvas (`canvas`) 
    // it is attached to, allowing quick access for `Parent()`.
    // This function initializes the variable with the return value
    public override Canvas GetCanvas()
    {
        return GetComponentInParent<Canvas>();
    }
}
```

If we now attach our `MyScreen.cs` script to an element in the canvas hierarchy our
UI will build as soon as we enter Play mode.

Our hierarchy would then look something like this:
```title="Hierarchy Example"
Canvas 
└─ MyScreen (SimpleScreen.cs on i.e. an Empty)
   └─ TextComponent ("Hello, World!")
      └─ ImageComponent (penguin)
```

