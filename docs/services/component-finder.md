---
sidebar_position: 2
title: ComponentFinder
description: Easily handle instances, singleton style
---

## Description

The ComponentFinder aims to provide a quick and easy way to create Instances for your
GameObjects, as well as statically store reference to certain important objects.

It offers a section dedicated to simple object reference storage (`Dictionary<string, MonoBehaviour>`) based on a string, as well as an analogous system for instances of a class (`Dictionary<Type, MonoBehaviour>`).  
The instance creation is based on the [Singleton pattern](https://medium.com/codex/game-design-pattern-using-singletons-in-unity-acbd05d8ac9d). It ensures that only instance of the given type is present at all types (*given it is done via the ComponentFinder*).

## Examples

```csharp title="GUI Service"

// store monobehaviours in a string dictionary
ComponentFinder.Put("i_need_this_somewhere", _myBehaviour);

// handle singleton flows easily
// create a new gameobject and assign it as an instance ...
MyClass instance = ComponentFinder.CreateInstance<MyClass>();
// ... or assign an existing gameobject as the instance
MyClass2 instance2 = ComponentFinder.PutInstance(_myClass2Obj);
// ... finally, delete instances whenever you like
ComponentFinder.DeleteInstance<MyClass>();

// ... or retrieve it somewhere else
MyClass2 instance2 = ComponentFinder.GetInstance<MyClass2>();
```

## Implementation

<div align="center">
:::note

[**ComponentFinder.cs**](https://www.github.com/GiorgioKalmund/UCGUI/tree/main/Runtime/Service/ComponentFinder.cs)

::: 
</div>

