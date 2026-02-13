---
sidebar_position: 5
title: SliderStyle
description: UCGUI default styles for SliderComponents
---

## Description

SliderStyles allow for a unified styling when creating [SliderComponents](../components/slider-component.md).

UCGUI has only one native SliderStyle: **Default**.

It colors the handle, background and fill area in slightly differnt shades of brightness 
for easier differentiation. 

![Slider Style Default](../../static/img/screenshot/slider-style-default.png)


It is strongly recommended to create your own styles for sliders as UCGUI doesnt use any sprites or fancy colors for sliders by default.
Look at [this section](./abstract-style#redefinition-of-existing-styles) on how to overwrite the `Default` style, allowing for automatic application
every time you instantiate a slider.

## Implementation

<div align="center">
:::note

[**SliderStyle.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Style/SliderStyle.cs)

::: 
</div>
