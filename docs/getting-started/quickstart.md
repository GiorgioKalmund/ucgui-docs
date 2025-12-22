---
sidebar_position: 2
title: Quickstart
description: Getting to know the basic workflow with UCGUI
---

Welcome to this little quickstart section.\
This part will be about some basic design and interaction concepts for UCGUI.

## Instantiating Components

UCGUI offers multiple ways to instantiate your components.

### Built-in 

There are configurable builders for easy creation of most built-in components.
You can access these via the `UI` class. These builders are meant of quick and easy
access to the essentials. A basic button, some text, or even a fully configured view.

```csharp title="Basic Components"
UI.Text("Hello, World!").Parent(canvas);

var myBtn = UI.Button("Click me!", () => {
    // ... action
}).Parent(buttonBar);
```

These builders return the created components, fully configured.

:::tip

As UCGUI elements and components are just regular GameObjects like everything else they
need to be added into the scene hierarchy.\
To add your elements into a spot in the hierarchy you can use the `.Parent(parentObj)` 
builder attachment. Otherwise your component will be created but it will not be
attached to its correct spot in the canvas and not be visible in most cases.

More on configuration [later](#configuration).

:::

### Custom

These pre-configured builders are good and all but if you have custom elements these
built-in functions won't cut it. \
For anything [custom](#creation), *assuming you also didn't write your own builder*, use the 
more 'low-level' function `UI.N<T>()`. This function takes in any `BaseComponent` (the
base of all other elements, similar to how `MonoBehaviour` is used for regular Unity 
scripts) and instantiates it. 

```csharp title="'Lower-level' instantiation"
// Instantiate any custom component if it inherits from BaseComponent ...
UI.N<MyCustomComponent>(); 

// ... or use it to create the native components as well
UI.N<TextComponent>(); 
``` 

:::tip

Behind the scenes the built-in builders use this way of instantiating anyways, 
meaning that `UI.Text()` is essentially just a convenient shorthand for `UI.N<TextComponent>()` with some additional 
configuration behind the scenes.

:::


## Configuring Components <a name="configuration"></a>

UCGUI heavily leans into the [Fluent Interface](https://en.wikipedia.org/wiki/Fluent_interface)
style of creating and configuring components. This allows for maximal control over 
how your components look and what they do. 

The `UI` class is split into two parts. One part allows for the convenient shorthands we 
have introduced above, the other part makes use of of C#'s ability to have global 
static extension methods which can be applied to any `BaseComponent`.\
All of these extensions follow the Fluent Interface pattern and return the component°
back to you after applying their respective configuration. 

These general-purpose functions control basic aspects like size, scale, rotation, sidebar_position,
anchors, pivots and more. 

Many native components also have such functions as part of their class for even more
component-specific configuration.

<a name="config-example"></a>
```csharp title="Configuration"
TextComponent title = UI.Text("Hello, Title!")
                        .FontSize(72) // TextComponent
                        .Color(UnityEngine.Color.red)  // GraphicComponent
                        .Pos(100, -100) // BaseComponent
                        .Pivot(PivotPosition.UpperLeft)
                        .AnchoredTo(PivotPosition.UpperRight);
```

Multiple functions from different levels of the element hierarchy can be applied a single 
instantiation to easily configure your element. 

Taking a closer look at the [example above](#config-example) we can see that different
functions come from differnt contexts. As in this case the native `TextComponent` inherits
from `GraphicComponent` we can also use its respective methods such as `Color(UnityEngine.Color)`,
`Alpha(float)` and some more. \
The final element is still a TextComponent however as both the base functions as well as 
the functions of the `GraphicComponent` are implemented with generics.

:::important tip

Watch out for order of operations when using this pattern. Some functions which come form 
lower down in the inheritance hierarhy might not return the same class back but instead
a refernce to a lower type leading to some functions to seemingly not be available.\
You can cast the the component back up to its desired class using `.Cast<T>()`.

:::


## Defining Custom Components <a name="creation"></a>

Creating a custom component is as easy as creating any other regular `MonoBehaviour`.
Let's take a look a small exercept:

```csharp title="Your Custom Component Class"
// MyCustomComponent.cs
import UCGUI;
// ...

class MyCustomComponent : BaseComponent {

    public override void Awake(){
        base.Awake();
        // Do all your initial creation for subcomponents, etc
    }

    public override void Start(){
        base.Start();
        // Do everything which needs to be done AFTER configuring your component
    }

}
```

As you can see, creating a custom component is as easy as it looks. Simply inherit from 
`BaseComponent` and start overriding Unity's lifecycle methods!

:::important

It is important to understand how [Unity's lifecycle](https://docs.unity3d.com/6000.3/Documentation/Manual/execution-order.html)
impacts the creation of elements, UI's and more when using UCGUI (*and for that matter everything which is code based 
makes use of multiple stages of the lifecycle.*).

Let's take a look at the relevant parts for us:
1. `Awake()` is called first. That is why this is where you optimally initialize all of your 
local variables and create any subcomponents your element might require.

2. [The configuration](#configuration) of your elements occurs **AFTER** `Awake` and
**BEFORE** `Start`. This is crucial to understand the timings for your UI.

3. `Start()` is called last. During this phase all variables have been initialized, either
via `Awake` or during the configuring phase, allowing you to now act based on this
state.

:::

## Displaying Components

No that we know some more about the inner workings of how UCGUI deals with components let's actually create a small complete interface.

Similar to how MonoBehaviours need to be attached to some GameObject using the edidtor, we need some point of reference which acts as a sort of "parent component".\
This is what [Screens]() are for. They a meant to act as a foundation and the upmost element of a hierarchy. All other components we create will most likely be parented 
to a screen or to its children.

Let's start:

```csharp title="Quickstart Example"
using UCGUI;
using UnityEngine;

public class MyScreen : SimpleScreen
{
    TextComponent title;
    // Called during 'Awake'
    public override void Create()
    {
        title = UI.Text("Hello")
                  .Parent(this);
        
        ImageComponent image = UI.Image(ImageService.GetSprite("penguin"))
                                 .OffsetY(-100)
                                 .Parent(title);
        
        // ... Create more UI here
    }
    
    // Called during 'Start'
    public override void Initialize()
    {
        // ... Additionally configure your UI here
        title.Text(", World!", TextMode.Additive);
    }
    
    // Every screen has a direct reference to the Canvas (`canvas`) 
    // it is attached to, allowing quick access for `Parent()`.
    // This function initializes the variable with the return value
    public override Canvas GetCanvas()
    {
        return GetComponentInParent<Canvas>();
    }
}
```

If we now attach our `MyScreen.cs` script to an element in the canvas hierarchy our
UI will build as soon as we enter Play mode.

Our hierary would then look something like this:
```title="Hierarchy Example"
Canvas 
└─ MyScreen (SimpleScreen.cs on i.e. an Empty)
   └─ TextComponent ("Hello, World!")
      └─ ImageComponent (penguin)
```
