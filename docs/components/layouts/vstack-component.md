---
sidebar_position: 3 
title: VStackComponent
description: A vertical layout built on top of Unity's 'VerticalLayoutGroup'
---

> extends [HorizontalOrVerticalLayoutComponent](./horizontal-or-vertical-layout-component.md)

The VStackComponent is essentially just a wrapper around Unity's [VerticalLayoutGroup](https://docs.unity3d.com/2022.3/Documentation/Manual/script-VerticalLayoutGroup.html).

The `UI.VStack(...)` builder is a very convenient shorthand, allowing you to syntactially and semantically encapuslate all of the stack's content.

:::note

Any component inherting from [LayoutComponent](./layout-component.md) automatically fits itself to the size of its children. This is done via 
a `ContentSizeFitter` component. If you don't want this, simply call `.Size(x,y)`
(or the related `.Width(x)` or `.Height(y)`) and the layout will instead conform 
to that size. 

:::

## Examples

```csharp title="Simple UI Builder"
UI.VStack(s => {
    // use .Add(BaseComponent) to add any arbitrary content
    s.Add(UI.Text("Hello from the top!"));

    // you can also create the elements first, then add them later ...
    TextComponent smiley = UI.Text("O_o");
    ImageComponent icon = UI.Image(_smileySprite);
    // ... and they don't even have to be of the same type inside 
    // the function call as it uses params syntax
    s.Add(smiley, icon);
})
.Parent(canvas);

UI.VStack(s => {
    s.Add(UI.Text("Hello from the bottom!"));
    s.Add(UI.Text("Hello from the top!"));
})
.ReverseArrangement()
.Parent(canvas);
```

:::tip

By default elements are ordered from **top to bottom** in a VStack based on the order you add them to the stack. 

If you want to reverse that arrangement you can simply call `.ReverseArrangement()` on
the stack to order them the other way!

:::

As any layout component can contain any type of contents, you can make the contents as 
complex as you'd like!

```csharp title="More Complex Example"
float spacing = 20f;
// set spacing between the elements vertically
UI.VStack(spacing, vs => {
    
    // add entire sub-hierarchies!
    vs.Add(
        // set spacing and the alignment of the children inside
        UI.HStack(spacing, TextAnchor.LeftCenter, hs => {
            hs.Add(UI.Text("Profile"));
            hs.Add(UI.Image(_profileSprite));
            hs.Spacer(); // push the elements to the left
            hs.Add(UI.Button("Home", () => {
                // ...
            }))
        }).Width(canvas.GetWidth())
    );

    // maximally separate the elements before and after the spacer within 
    // the bounds of the VStack 
    vs.Spacer();

    vs.Add(UI.Button("Home", () => {
        // ...
    }));

})
.Size(canvas.GetWidth(), canvas.GetHeight())
.Parent(canvas);
```

:::tip 

**Spacers** can be extremely useful when it comes to formatting your layouts. Learn more about them [here](./spacer-component.md).

*They idea takes very strong inspriation from [SwiftUI's Spacers](https://developer.apple.com/documentation/swiftui/spacer) again, so if you are familar with them UCGUI's Spacers work pretty much identically.*

:::

## Implementation

<div align="center">
:::note

[**VStackComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/VStackComponent.cs)

::: 
</div>
