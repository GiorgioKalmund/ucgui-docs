---
sidebar_position: 7
title: Layouts
---

Most user interfaces require some sort of dynamic layout system. Containers need to adjust to the size of their parents and elements need to be properly spaced within them.

Unity offers some basic tools for this and UCGUI mostly builds on top of them.
Similar to other UI building tools UCGUI offers standard flexible directional layout containers:

## VStack and HStack

The V(ertical) and H(orizontal) Stacks are essential to most UIs. They lay out elements 
in their respective direction automatically, either aligning content the edges or to the relative centers.

They are very useful to quickly create some evenly spaced content without the need for manual positioning.
Let's take a look at a simple example first.

```csharp
UI.HStack(_ => {
    for (int i = 0; i < 5; i++)
            UI.Image(new Color(i * .1f, i * .1f, i * .1f))
});
```

![HStack Simple](../../../static/img/screenshot/tutorial-layouts-hstack-simple.png)

As we can see, the HStack automatically aligns our color gradient images horizontally.
Additionally, the stack makes use of UCGUI's automatic parenting to add all of the content part of the closure to the stack directly, without having to explicitly specify this parent relationship.
All builders of this type make use of this functionality, allowing the syntax of your code to somewhat represent its underlying semantics!

You might notice however that the images are very tightly packed together and you want your color gradient 
to feel more like a piece of paper with some color blocks on it.

We can change the distance _between the individual elements_ with the **'spacing'** value of the HStack when instantiating it.

Additionally, the HStack itself is exactly the size of its contents. 
If we want it to have some outer **margins / padding** we need can manually specify that as well.

One more thing: All layouts indirectly inherit from the Image, meaning we can simply call `.Color` or `.Sprite` on them to fill them in!

Let's put all of these things together to create a more advanced layout for our gradient.

```csharp
int spacing = 20;
int paddingAmount = 20;
UI.HStack(spacing, stack => {
    for (int i = 0; i < 5; i++)
            UI.Image(new Color(i * .1f, i * .1f, i * .1f))

    stack.Padding(PaddingSide.All, paddingAmount);
})
.Color(Color.white); // inherited from ImageComponent
```

![HStack Advanced](../../../static/img/screenshot/tutorial-layouts-hstack-advanced.png)

_The VStack works analagously, just in the vertical instead of the horizontal direction._

:::tip

There is nothing stopping you from nesting these to create more complex layout combinations :).
To find out more about what these stacks can do visit their respective pages: 
[HStack](../../components/layouts/hstack-component.md) / [VStack](../../components/layouts/vstack-component.md).

:::

## Grid

The GridComponent is a simple wrapper around Unity's built in grid layout.
The builder can be configured to have either a fixed column or row count:

```csharp
UI.Grid(GridLayoutGroup.Constraint.FixedColumnCount, 5, grid =>
{
    grid.CellSize(100, 100);
    for (int y = 0; y < 5; y++)
        for (int x = 0; x < 5; x++)
            UI.Image((x + y) % 2 == 0 ? Color.gray2 : Color.gray1);
}).Parent(canvas);
```

Grids always enforce a certain cell size. You can change it but it defaults to 100x100.

![Grid](../../../static/img/screenshot/tutorial-layouts-grid.png)


:::note

There are also some other layouts in UCGUI such as the SwitchLayout (which can dynamically switch its orientation between horizontal 
and vertical), however they are not too relevant for this rather basic tutorial.

:::

What we have learnt in this section:
- HStack and VStack are powerful tools, allowing you to easily distribute elements.
- The Grid aligns objects in a ... _you guessed it_ ... grid!
- All layouts make use of autmatic parenting within their respective layout scopes.
