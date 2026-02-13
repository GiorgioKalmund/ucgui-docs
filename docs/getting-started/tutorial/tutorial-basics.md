---
sidebar_position: 2
title: Tutorial - Basics
---

## Philosphy and Core Principles

Before we take a look at some code let's first quickly explore some of the philosophy 
and core principles of UCGUI. I promised less yapping but I want to get some stuff
of my chest and explain some of the decisions made before we take a look at some 
code. If this seems boring to you (_look at how long this section is! omg!!!_), feel 
free to [jump ahead](./tutorial-creating.md).

As the 'C' in UCGUI stands for 'codable' one might correctly assume that this is a code-based UI 
library for the [Unity Game Engine](https://unity.com). This means that your user interface 
will live inside of classes and MonoBehaviours. This comes with some advantages, but 
also major drawbacks.

As opposed to relying on a dedicated visual editor, like the Unity Editor, UCGUI
relies on your coding skills and thus has **no visual editor** to move things around, 
rescale them or set the text of an element. If this is a dealbreaker for you, you might
have picked the wrong library (I mean, it _is in_ the name O_o). This means your UI is only compiled,
built and initialized the moment you press 'Play' in your editor.

However, if the lack of a visual editor is not a problem for you (_i.e. 
you know what ViM, tmux or emacs is and have a slight lack of touching grass_) then 
UCGUI might even feel **more useful** to you. Especially for very complex state transitions,
animations, input handling etc. the editor quickly reaches its limits and you experience yours
as you try to juggle your hierarchy, managing various popups, enabling and disbaling inputs
at the proper time and so much more.
Most of these actions require you to use MonoBehaviours anyways
so why bother always alt-tabbing between your editor and code just to try to set a function
for a button which is 10 layers deep in your hierarchy? \
More on how exactly we can solve these issues later.


UI elements in UCGUI, often also referred to as 'components', are simple MonoBehaviour scripts,
thus you have full control over their [lifecycle](https://docs.unity3d.com/6000.3/Documentation/Manual/execution-order.html).

Additionally, most components to make use of the [Fluent Interface](https://en.wikipedia.org/wiki/Fluent_interface) 
pattern, allowing you to hook into their lifecycle 
and quickly modify them through chaining of function calls.

:::tip

If you want a more specific insight on how **exactly** UCGUI handles timing inside 
Unity's lifecycle I recommend you to go through the ["Interacting with the Unity Lifecycle"](../quickstart.md#interacting-with-the-unity-lifecycle) section
on the quickstart page **after** this tutorial.

:::
