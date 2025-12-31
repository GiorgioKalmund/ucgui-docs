---
sidebar_position: 7
title: SliderComponent
description: Configurable slider based on Unity's Slider component
---

> extends [BaseComponent]() implements [IStylable\<SliderComponent, SliderStyle\>](../interfaces/istylabe.md)

## Description

The SliderComponent is quite simple as it, simimlar to the [InputComponent](./input-component.md), simply tries to mirror what the native uGUI functionaly offers with some additional 
configuration options.

You can customize the `background`, `foreground` and `handle`, as well as 
configure `MaxValue` and `MinValue` for your range.

For a basic slider simlpy use the [provided builder](#examples) with your custom [`SliderStyle`](../interfaces/istylabe.md)!

:::important

If the range of the slider is incorrectly ordererd (min value is larger than max) the range will automatically be 
flipped.

:::
 
## Examples

```csharp title="Simple UI Builder"
SliderComponent slider = UI.Slider(new Range(0, 1), builder =>
{
    // optionally style your slider here ...
    builder.Foreground(_fillSprite);
    builder.Background(_backgroundSprite);
    builder.Handle(_handleSprite);

    // ... and modify its behaviour
    builder.IntegerSteps(); 
}, newVal =>
{
    // optional on value changed callback
})
.Parent(canvas);

Debug.Log(slider.Value) // retrieve the current value in the slider
```

## Implementation

<div align="center">
:::note

[**SliderComponent.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/SliderComponent.cs)

::: 
</div>
