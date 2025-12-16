---
sidebar_position: 1
title: Overview
description: Overview of all components in UCGUI 
---

This is a small overview of all native UCGUI components.

Every component has its own entry. At the top of every file is a link to the implementation of that component.

:::tip important

In most cases, if not specified otherwise, the default return value of a function inside of a component is the component itself after the modification.
This is to maintaing the flexible [Fluent Interface](https://en.wikipedia.org/wiki/Fluent_interface) pattern.

If the function **does** have a return value which is not implicit the markdown header title will
state the return value after the function name using a semicolon, i.e. `Foo() : string` returns a string.

:::

:::tip

If you are unsure of how a component works or what functions are available it is always
a good idea to take a look at the source code directly.\
Even though this documentation tries to cover all the aspects which are relevant for 
development you might want to dive in deeper to understand certain nuances.

[Components on GitHub](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Components/)

:::
