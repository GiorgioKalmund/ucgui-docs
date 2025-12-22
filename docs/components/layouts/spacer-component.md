---
title: SpacerComponent
description: A flexible space that expands along the axis of its containing stack layout.
---

> extends [BaseComponent]() implementes [IEnabled](), [IRenderable]()

## Description

The Spacer is a very simple but powerful component. It takes the maximum space possible when inside a stack.\
If there are multiple Spacers within the same stack, they share the remaining distance **equally** between them.

Spacers act based on their configured [ISpacerBehaviour]().\
For example the [HorizontalSpacerBehaviour]() is applied to a spacer inside of an `HStack`, the [VerticalSpacerBehaviour]() for when it is insde a `VStack`. This normally happens automatically but you can also set your behaviour yourself with `.SetBehaviour(ISpacerBehaviour)`. \
The Spacer will then call its behaviour's `.Apply()` function, which makes the Spacer properly behave according to its envrionment.

`VerticalSpacerBehaviour` and `HorizontalSpacerBehaviour` or supported natively seamlessly work with the `HStack` and `VStack`, respectively. Whenever you call `LayoutBuilder.Spacer()` the new spacer will choose the appropriate behaviour on its own if non is manually set beforehand.

:::note important

If there is **not enough space** for a Spacer, for example if there are only 10px of space between two elements but the spacing is bigger or equal to 5px, then the Spacer **automatically disables itself**.

:::

## Examples

```csharp title="Sometimes I could use a little bit of space..."
// naive formatting, no spacer
UI.HStack(s => {
    // --------[][]-------- 
    s.Add(UI.Image(_left));
    s.Add(UI.Image(_right));
})
.Width(_width)

// spacer to push objects apart
UI.HStack(s => {
    // []----------------[]
    s.Add(UI.Image(_left));
    s.Spacer();
    s.Add(UI.Image(_right));
})
.Width(_width)

// positioning of the spacer obviously matters
UI.HStack(s => {
    // [][]----------------
    s.Add(UI.Image(_left));
    s.Add(UI.Image(_right));
    s.Spacer();
})
.Width(_width)

// and you can use multiple spacers simulatenously!
// they will balance out!
UI.HStack(s => {
    // []-------[]-------[]
    s.Add(UI.Image(_left));
    s.Spacer();
    s.Add(UI.Image(_middle));
    s.Spacer();
    s.Add(UI.Image(_right));
})
.Width(_width)
```

:::important

The native horizontal and vertical behavious **only** work if the surrounding layout has a **fixed size** in the respective direction. 

:::

Here an example for the case mentioned above where the Spacer disables itself if there is not enough space for it and it would otherwise have to push elements out of the bounds
of the containing stack.

If the Spacer in this example would not disable itself we would run into a **problem**. 
The HStack is only 220px wide and the elements (exluding the Spacer) already take up exactly that amount of space. If we would now want to add a Spacer we would need enough
horizontal space for the **extra padding added due to an additional element** in the hierarchy as well as **addtional space for the spacer to flex into**.\

The calculations for the native behavious respect **spacing as well as padding** of the stack in the relevant direction to decide whether to disable or enable the spacer.

```csharp title="Tight Space(r)s"
UI.VStack(20, s => {
    s.Add(UI.Image(_left)); // default width 100
    // spacing of 20 between these two set by the VStack
    s.Spacer(); // !!! DISABLES ITSELF DUE TO LACK OF SPACE !!!
    s.Add(UI.Image(_right)); // default width 100

    // 220 <= 100 + 100 + (1 * 20) => not enough space for spacer
})
.Width(220)
```

As we have seen above Spacers have an integrated shorthand inside of the `LayoutBuilder`for stacks. There is also a default `UI.Spacer()` shorthand as well though. Meaning that all of these are functionally equivalent:

```csharp title="Insert Spiderman Meme Here"
UI.VStack(s => {
    // all of these are the same...
    s.Spacer();
    s.Add(UI.Spacer());
    s.Add(UI.Spacer(new VerticalSpacerBehaviour()));
    s.Add(UI.N<SpacerComponent>());
});
```

## Implementation

<div align="center">
:::note 

[**SpacerComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/SpacerComponent.cs)

::: 
</div>
