---
title: IEnabled
description: Unifying calls to elements which can be enabled or disabled
---

## Description

The IEnabled interface aims to provide a unifyed function `Enabled(bool)` which 
must be implemented by inhertors. 

This allows for a simpler syntax across components, as well as allowing bulk requests 
when using `GetComponents[...]<T>()` calls.

## Examples

```csharp title="Simple UI Example"
TextComponent myText = UI.Text("Foo");
ButtonComponent myButton = UI.Button("Click", () => { /* ... */ });

myText.Enabled(false); // invokes the text-specific implementation
myButton.Enabled(false); // invokes the button-specific implementation
```

## References

This interface is implemented by: [`GraphicComponent`](), [`AbstractViewComponent`](),
[`LayoutComponent`](../components/layouts/layout-component.md), [`ScrollViewComponent`](), [`SpacerComponent`](../components/layouts/spacer-component.md).



## Implementation

<div align="center">
:::note

[**IEnabled.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Interface/IEnabled.cs)

::: 
</div>
