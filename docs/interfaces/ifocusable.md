---
title: IFocusable
description: Simplify parttaking in focus-based interactions
---

## Description

Focus and focus states are a core concept to any user interface.
They play a crucial role in the communication of interactions and feedback to the user.

The IFocusable interface aims to provide a handy system which allows for easy 
focus-based transitions.

To achieve such interactions `IFocusable`'s core is based on a simply hashmap which tracks which member is the currently focused one for a given string key. This key is 
also referred to as the 'FocusGroup'. All  components which share the same FocusGroup will therefore be part of the same logical group for focus-based interactions.

The idea of FocusGroup is that at any point in time there can only be **exactly one** member which is the 'focused' one. Whenever another members wants to be focused the 
previously focused element will first be unfocused and then the new element will be focused. Behind the scenes the reference to the focused element in the map for the respective FocusGroup will also be adjusted to properly reflect the new state.

### Requirements
To conform to this interface members have to implement the following members:

1. `string FocusGroup` - The group the element is part of.
2. `UnityEvent OnFocusEvent` - Reference to an optional event which is fired on focus.
3. `UnityEvent OnUnfocusEvent` - Reference to an optional event which is fired when loosing focus.
4. `void HandleFocus()` - Handler invoked when element is focused.
5. `void HandleUnfocus()` - Handler invoked when element looses its focused.

:::tip

You dont't have to initialize the `FocusGroup` string to specify which group they want 
to belong to.
UCGUI will fall back to an internal global group `"ucgui-focus-group-default"`. \
It is set via `Defaults.Focus.DefaultGroup`.

You can also change it at runtime by setting the property (*only recommended for unqiue or single-use components, otherwise initialize the property inside the class directly*).

:::

:::tip

The static `FocusableHelper` class offers `CreateFocusEvent()` and `CreateUnfocusEvent()` functions which can be used to externally and safely initialize your optional events.

:::

### `FocusState<T>`

> where `T` extends `struct`, `Enum`

The FocusState class aims to provide a closed and context based focus group wrapper with some additional functionalities.

To join a FocusState, any member implementing [IFocusable](#description) can call
`.Focusable(FocusState<T>, T)`. This uniquely links this member to that specific enum value.

The idea behind a FocusSate is that it created a bidirectional relationship between the 
enum and the members in the FocusState. 

Every FocusState has a `T Value` property which points to the "current" or "active" enum
value. This allows for easy control the internal FocusGroup's active member: simply set
'Value' to the new desired enum member and the corresponding `IFocusable` is focused.
This also works vice versa.

:::important

When joining a FocusState a member's FocusGroup is automatically assigned based on a unique identifier. 
There is no need to unify the members into a separate group manually!

:::

### Cycling Through States
Additionally FocusStates have the `Next()` and `Previous()` functions which all you to 
easily cycle through the bound members. The order is defined by the order you add the 
elements to the FocusState.

Additionally, an optional `TransitionMode`s can be specified to adjust the 
forward and backward cycling behaviour:

1. `Simple` - Cycles through every element in the state until either the left or right border has been hit.
2. `Loop` - Cycles through every element in the state, looping around to the opposite border after it has been hit.
3. `LoopWithNull` - Cycles through every element in the state. After a border has been hit the state will first set its value to `null` before looping back to the opposite border.

:::note 

FocusStates are by no means a new concept. If you are familiar with [SwiftUI's @FocusState property wrapper](https://developer.apple.com/documentation/swiftui/focusstate)
expect this to work in a very similar way.

:::


## Examples


```csharp title="Simple Class Example"
class MyFocusableElement : BaseComponent, IFocusable {
    /* your element code */ 

    // mandatory ifocsuable members:
    public string FocusGroup { get; set; } // = "my-custom-focus-group"
        
    public UnityEvent OnFocusEvent { get; set; } // = new UnityEvent();
    
    public UnityEvent OnUnfocusEvent { get; set; } // = new UnityEvent();
    
    public void HandleFocus() { 
        // invoked every time this element calls '.Focus()'
    }

    public void HandleUnfocus() {
        // invoked every time this element calls '.Unfocus()'
    }
}
```


```csharp title="A Simple FocusState"
enum SelectedTab { Shop, Home, Profile }

FocusState<SelectedTab> focusState = new (/* optional default init value*/);

// create and configure your elements ...

var tab1 = UI.N<MyFocusableElement>().Focusable(focusState, Shop); 
var tab2 = UI.N<MyFocusableElement>().Focusable(focusState, Home); 
var tab3 = UI.N<MyFocusableElement>().Focusable(focusState, Profile); 

// ... and later focus them
focus.Value = Home; // invokes 'HandleFocus' in 'tab2'

// ... or cycle through them
focus.Next(); // invokes 'HandleFocus' in 'tab3', sets Value to 'Profile'
focus.Next(TransitionMode.Loop); // invokes 'HandleFocus' in 'tab1', sets Value to 'Shop'
```

## References

This interface is implemented by: [`ButtonComponent`](../components/button-component.md), [`InputComponet`](../components/input-component.md).

## Implementation

<div align="center">
:::note

[**IFocusable.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/Interface/IFocusable.cs)

::: 
</div>
