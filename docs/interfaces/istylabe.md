---
title: IStylable<T, TStyle>
description: Unified, preset-based styling options for components
---

> where `T` extends `MonoBehaviour` \
> where `TStyle` extends `AbstractStyle\<T, TStyle\>`

## Description

The IStylable interface aims to provide an easy way to save and load presets for configuration of your components.

Classes making use of this interface are required to implement a given `Style(TStyle)` 
function which takes in any `AbstractStyle` and applies it to the component.

A style is essentially just a shorthand for a configuration of a component. 
It can be as simple or complex as you like!

## Examples

Let's take a look at an example. I might want to have a specific style for my buttons
in my game an it would obviously be quite redundant and difficult to maintain if I
always simply inline my styling options.

Styles help you with exactly that! They provide a handle to the component they are styling and simply apply (*by calling `AbstractStyle.Apply()`*) the given configuration when `Style(TStyle)` is called.


```csharp title="Simple UI Example"
// create a custom, reusable, style ...
MyStyle Plain = new MyStyle(myComponent =>
{
    myComponent.Color(UnityEngine.Color.gray);
    myComponent.FitToContents(20, 20);
    myComponent.text.Style(TextStyle.ButtonText);
});

// ... and apply it onto your components
MyComponent foo = UI.N<MyComponent>(); // ... base creation
foo.Style(Plain)
```
A very handy thing is the `Expand()` functionality for styles.
Let's expand (*badum-ts*) on the example above...

```csharp title="Style Expansion"
// expand on the style from above by making additional changes!
// all changes defined in 'Plain' will be applied first
MyStyle PlainTitle = Plain.Expand(myComponent => {
    myComponent.text.FontSize(72);
    myComponent.text.Bold();
});

MyComponent fooTitle = foo.Copy();
// apply expansion style
fooTitle.Style(PlainTitle);
```

## References

This interface is implemented by: [`TextComponent`](../components/text-component.md), [`LabelComponent`](../components/label-component.md), [`ButtonComponent`](../components/layouts/button-component.md), [`InputComponent`](../components/input-component.md), [`SliderComponent`](../components/slider-component.md).

## Implementation

<div align="center">
:::note

[**IStylable.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Interface/IStylable.cs)

::: 
</div>
