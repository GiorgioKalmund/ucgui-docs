---
sidebar_position: 1
title: Introduction
id: intro
---

Welcome to the official documentation for [Unity Codable GUI (UCGUI)](https://www.github.com/GiorgioKalmund/UCGUI).

:::warning
**UCGUI is still in very early development. Components, classes and functions are currently 
still subject to change at any time.** 
:::

## Why UCGUI?

Simple UIs can easily be created in the editor, however they often need assistance from scripts and other libraries to do things like animation, transitions, etc.
This is where UCGUI jumps in.
Building on top of [Unity's built in uGUI components](https://docs.unity3d.com/Packages/com.unity.ugui@2.0/manual/index.html) UCGUI offers easy access to a variety of basic components as well as additionally adding fully custom and new concepts and components.

## TODO Correct DocuSaurus references

UCGUI's built in tools allow easy and accessible creation of [Text](Runtime/Components/TextComponent.cs), [Images](Runtime/Components/ImageComponent.cs), [Buttons](Runtime/Components/ButtonComponent.cs), [Input](Runtime/Components/InputComponent.cs), [Sliders](Runtime/Components/SliderComponent.cs), [Views](Runtime/Components/ViewComponent.cs), [Layouts](Runtime/Components/LayoutComponent.cs) and so much more.
Everything is based on a singular [BaseComponent]() class and every class is created in such a way that it can be easily inherited from and expanded upon.

The main benefit comes from inherent code-based control over your UI at runtime, allowing dynamic UI combinations to be created faster and frictionless.

> <i>It might not be for everyone, but it helps me at least to keep everything **inside** my code, as code, without having to constantly search through the hierarchy to edit one specific parameter of my UI. Everything is just code, and way more flexible as it can be easily referenced during runtime.</i>

