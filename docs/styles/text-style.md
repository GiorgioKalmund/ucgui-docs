---
sidebar_position: 2
title: TextStyle
description: UCGUI default styles for TextComponents
---

> extends [AbstractStyle\<TextComponent, TextStyle\>](./abstract-style.md) 

## Description

Text is at the core of most graphical user interfaces and having
an unified font and text styles is crucial.

UCGUI comes with _five_ basic styles for texts: **Primary**, **Secondary**, 
**Tertiary**, **Caption** and **ButtonText**.

The first four allow for simple hierarchial differentiation of
text:

![Basic Text Styles](../../static/img/screenshot/text-style-basic-styles.png)

The Secondary, Tertiary and Caption styles all expand from the Primary one.

The **ButtonText** style also expands on the primary one and simple centers the text 
horizontally as well. 
It is applied once to the default text element in the [ButtonComponent](../components/button-component.md) when it is initially created.

:::tip

Take a look at the [AbstractStyle class](./abstract-style.md#the-power-of-styles) for examples on how to 
customize existing and create new styles.

:::

## Implementation

<div align="center">
:::note

[**TextStyle.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Style/TextStyle.cs)

::: 
</div>


