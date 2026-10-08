---
sidebar_position: 7
title: Automatic Parenting
---

Before we dive into more nuanced aspects of UCGUI's layout system and varitey of component types we first need to introduce a curcial mechanism acting behind the scenes of UCGUI's interface system.

As hinted at during the beginning of this tutorial, manually parenting elements to other elements is actually optional in UCGUI. 
When reading through the previous examples you might have already thought *"Ok if everything is parented to the canvas, why can't I just say that once?"*. This is exactly the problem UCGUI's automatic parenting aims to solve.

Take this example from a previous section:

```csharp title="Manual Parenting"
public override void Create(){
    UI.Image(Color.purple)
    .Maximize()
    .Parent(canvas);

    UI.Text("Hello, World!")
    .FitToContents()
    .Color(Color.white)
    .Bold()
    .Parent(canvas);

    UI.Button("Press Me", () => {
        // ... action on press
    }).OffsetY(-150).Parent(canvas);
}
```

As we can see, all elements should be parented to the top level of the canvas, and we manually declared this for every individual element.
There are multiple ways to simplify this piece of code, whilst leading to the identical result. 
We can make use of UCGUI's `BeginParentContext(...)` and `EndParentContext()` functions which allow us to group consecutive declarations of elements into one parenting context. 
Users familiar with immediate-style user interfaces might be already familiar with this paradigm of "Begin..." and "End...".


```csharp title="Begin and End via Contexts"
public override void Create(){
    // Until we end this context, all elements are parented to the "canvas"
    BeginParentContext(canvas); 

        UI.Image(Color.purple)
        .Maximize();

        // other elements ...

    // "canvas" end
    EndParentContext();
}
```

This approach lets us remove all `Parent()` calls which attach elements to the context's parent. 
It also works in a stack-like manner, allowing us to nest these statements, creating a hierarchy:

```csharp title="Begin and End via Contexts"
public override void Create(){
    // Until we end this context, all elements are parented to the "canvas"
    BeginParentContext(canvas); 

       // parented to "canvas"
       var img = UI.Image(Color.purple)
        .Maximize();

        BeginParentContext(img);  // "img" begin
            // parented to "img"
            UI.Image(Color.yellow); 
        EndParentContext(); // "img" end

        // parented to "canvas" again
        var img3 = UI.Image(Color.red).Pivot(UpperCenter, true); 

    // "canvas" end
    EndParentContext();
}
```

This might seem rather verbose and tedious, especially the context only consists of a singular element. 
However, this is not the case in most scenarios, especially when putting elements in layouts, which we'll see in the next section.
For simple scenarios you can refer back to using the standard `.Parent()` extension.

The `ParentContext(..., UnityAction)` wrapper also helps with keeping track of you parent scopes more clearly by wrapping the body in an `UnityAction`. 
Using it, the same code shown above can also be written as:

```csharp title="Parent Context Shorthand"
public override void Create(){
    // Until we end this context, all elements are parented to the "canvas"
    ParentContext(canvas, () => {
       // parented to "canvas"
       ParentContext(UI.Image(Color.purple).Maximize(), () => {
            // parented to purple image
            UI.Image(Color.yellow); 
       });

       // parented to "canvas" again
       UI.Image(Color.red).Pivot(UpperCenter, true); 
    });
}
```

Here the scopes of the parent context are easier to distinguish using, however the resulting behaviour and layout are functionally identical. 
Note that we can directly inline creation of the purple image into the `ParentContext` call, allowing us to save on some dellarations and definitions of obejcts if we don't need their references for anything else.

This aumatic parenting behaviour is also the standard for anythign created within a screen. 
This is why we could also omit the first `ParentContext` call and simply parent everything to the screen object directly, leading to a visually identical result:

```csharp title="Parent Context Shorthand"
// parent context is initialized to "this" before entering here
public override void Create(){  
   // parented to "this" (screen)
   ParentContext(UI.Image(Color.purple).Maximize(), () => {
        // parented to purple image
        UI.Image(Color.yellow); 
   });

   // parented to "this" again
   UI.Image(Color.red).Pivot(UpperCenter, true); 
}
```

In the next section we will not only explore the automatic layout options avaiable in UCGUI, but also how the available builder functions make use of this automatic parenting, enabling a more enjoyable syntax.
