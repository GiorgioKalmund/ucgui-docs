---
title: ICopyable<T>
description: Unifying calls to duplicate or copy properties of an element
---

> where `T` extends `MonoBehaviour`

## Description

Re-instantiating existing GameObjects is not always as easy as calling `Instantiate()`, especially
when the object has been created at runtime as is not a prefab of some sorts. 

ICopyable tries to bridge this gap by enforcing explicit `Copy()` and `CopyFrom()` method
calls which can be used to create a new instance of a component.

The intention of this interface is provide access to **deep copying** of a component.

`Copy()`

:::tip

Most of the native elements in UCGUI implement this interface. 
If you are unsure how exactly an implemenation could look like, take a look at 
the [Button's implemenation](https://github.com/GiorgioKalmund/UCGUI/blob/491b1fb81fc2f4f2faf9eeb7cd7762edc904c3b3/Runtime/Components/ButtonComponent.cs#L153C5-L174C10).

:::

## Examples

```csharp title="Simple UI Example"
TextComponent myText = UI.Text("Foo");

// creates a deep copy, text, rect, etc. are all copied
TextComponent myText2 = myText.Copy(); 
```

## Implementation

<div align="center">
:::note

[**ICopyable.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Interface/ICopyable.cs)

::: 
</div>
