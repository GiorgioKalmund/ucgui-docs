---
sidebar_position: 1
title: AbstractStyle
description: Base class for component styling with UCGUI
---

> where `T` extends `MonoBehaviour` \
> where `TStyle` extends `AbstractStyle<T, TStyle>`

## Description

The AbstractStyle is a simple base class which, in combination with
[IStylable](../interfaces/istylabe.md), allows for a unified way of
saving and reusing certain configurations for components.

It makes use of a generic builder (according to `T`) to 
allow for builder-pattern style access to a component for styling.

`TStyle` is simply the implementing class itself, allowing
for a generic `TStyle Expand(UnityAction<T>)` call. 

## Requirements

Inheritors **must** implement two simple elements:
The constructor of the style, according to the `T` generic,
and a protected `Create(UnityAction<T>)` call, which is also used as part
of the expansion functionality.

This might seem a bit confusing so let's take a look at a small
example from the [TextStyle](./text-style.md):

```csharp
    public class TextStyle : AbstractStyle<TextComponent, TextStyle>
    {
        // MUST implement constructor
        public TextStyle(UnityAction<TextComponent> builder) : base(builder) { }

        // MUST implement 'Create'
        protected override TextStyle Create(UnityAction<TextComponent> builder)
        {
            // simple as that! 
            return new TextStyle(builder);
        }

        // ...
    }
```

:::tip

Take a look at the styles either on [GitHub](https://github.com/giorgiokalmund/UCGUI/tree/main/Runtime/Components/Style) or here in the docs as they offer examples
of how basic UCGUI components are styled and how you can easily style yours 
to achieve your unique look!

:::

## The Power of Styles

As already described in the example shown on the [IStylable](../interfaces/istylabe.md) page, styles can 
be created on the fly and applied to supported components. Here are some things we can do with them, from simple
to a bit more powerful.

### Creating a Style

Styles are just objects and not MonoBehaviours, meaning you can easily create one using the constructor, as
mentioned [in the example above](#requirements). The following examples will continue to make use of the 
[TextStyle](./text-style.md), however these principles apply to any style.

The builder in the constructor is simply a reference to the respective `T` component (here: TextComponent) which is 
going to be styled by the style.

```csharp title="Creating a basic Style"
TextStyle myWarningStyle = new TextStyle(txtCmpnt => {
    txtCmpnt.Italic().Bold();
    txtCmpnt.FontSize(52);
    txtCmpnt.Color(Color.red);
});
```

It can then be applied to any associated member:

```csharp
var warning = UI.Text("HELLO, WORLD!!!");
warning.Style(myWarningStyle);
```

:::tip

It is probably best to have some sort of class (like UCGUI does it for its default styles) which 
holds your static styles so you can easily access them from anywhere in your project.

:::

### Expanding Styles

As hinted at previously, styles can be 'expanded upon'.
Expaning on a style copies all its configurations,
allowing you treat it as a baseline for a new style.

Let's expand on the example from above, by creating a new style which 
is based on the `myWarningStyle`.

```csharp title="Style Expansion"

TextStyle mySecondaryWarningStyle = myWarningStyle.Expand(txtCmpnt => {
    // first, all elements of the base style are applied, then:
    txtCmpnt.FontSize(txt.GetTextMesh().fontSize * 0.75);
    txtCmpnt.Color(Color.orange);
});
```

`mySecondaryWarningStyle` is now also italic and bold but orange and a bit smaller
instead. The neat thing is that if at any point you decide that all warnings should no
longer be bold you only need to make a change to one style and the hierarchy propagates
it downwards.

:::tip

You can access the underlying TextMeshPro behaviour of any TextComponent using
`GetTextMesh()`. This is helpful in situations where you need access to a property
which is not routed / exposed via UCGUI.

In the example above the secondary warning will thus always be only 75% of the size of the 
main warning style, making it even simpler to handle styles as you now need to only
change the font size of the main style and the relative sizes between warnings 
stay the same.

:::


### Redefinition of Existing Styles

For your own project you probably want to change the default styles for certain UCGUI components.
Some components, such as text or buttons, automatically apply a basic styling to them when created via 
UCGUI. This is done in the 'Awake' phase, meaning that your customization and configuration
(i.e. inside of a [Screen](../components/simple-screen.md) or [View](../components/views/abstract-view-component.md)) will be applied **after** it.

For example, the TextComponent applies the `TextStyle.Primary` style on Awake, coloring it in a subtle tone of dark gray 
and and aligning the text vertically. However, you might want your game to to have white primary text, align it at the bottom
edge, as well as change the font-size and font-family. The latter can be already be done by changing `Defaults.Text.GlobalFont` or calling
`GlobalFont()` on a text, but the other requirements cannot be changed so easily.
Obviously you do not want to apply your custom style every time manually (i.e. `<text>.Style(MyStyle)`); it would
be way more convenient to have this happen automatically every time you create a new TextComponent via UCGUI!

The existing TextStyles are static, but modifiable, allowing you to simply override them initially:

```csharp title="Creating a new style for Primary text"
TextStyle.Primary = new TextStyle(txt => {
    txt.Color(Color.white);
    txt.VAlignment(VerticalAlignmentOptions.Bottom);
    txt.FontSize(42); // a bit larger than unity's default of 36
});

TextComponent.GlobalFont(_myFontAsset);

// ... 

UI.Text("Foo"); // now styled white, bottom, etc...

```

Now all of the basic text is automatically formatted according your custom rules 
without any manual code changes to the individual elements!
_It might be helpful to take a look at [TextStyle](./text-style.md) for a complete overview of all builtin text styles._

### Redefinition with Expansion

Even though a bit twisted to look at, you can also redefine a style
by expanding on itself. This might be useful in the rare occasion where 
you want to actually keep the existing configuration of a style and 
simply update it:

```csharp
TextStyle.Primary = TextStyle.Primary.Expand(txtCmpnt => {
    txtCmpnt.AlignCenter();
});
// => TextStyle.Primary (and all inheritors) are now also horizontally 
// aligned around the center in addition to being vertically aligned
```

## Implementation

<div align="center">
:::note

[**AbstractStyle.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Style/AbstractStyle.cs)

::: 
</div>


