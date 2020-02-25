# Panel (Anchored UI)

This library was originally created for use in my [Tactics RPG project](http://theliquidfire.com/2015/06/22/tactics-rpg-anchored-ui/), and has since been used in several other projects.

## Features

Allows you to position UI Panels programmatically with the same ease that you have while working with them in the insepector at edit time.  You can position them with or without animation.  This makes it easy to slide menus on and off screen etc.

## Setup

1. Build your menu/screen with Unity UI (Canvas, Panel, etc).  For example, begin with the menu "GameObject -> UI -> Panel" (note that Unity calls it a `Panel` object but there is no `Panel` component provided by Unity.  They simply have a `RectTransform`, `Canvas Renderer`, and `Image`.  I created a `Panel` component that should be added to the equivalent `Panel` object in the hierarchy.
2. Configure the `Panel` component by defining the positions you want it to occupy.

### Example Setup

In this setup example, we configure a `Panel` to be able to show in the lower right corner of the screen, and animate on and off from the side of the screen.

1. Set the `Position List` `Size` to `2`
2. For the first position:
    - `Name`: "Hide"
    - `My Anchor`: `Lower Left`
    - `Parent Anchor`: `Lower Right`
3. For the second position:
    - `Name`: "Show"
    - `My Anchor`: `Lower Right`
    - `Parent Anchor`: `Lower Right`
  
 Note that you can also specify a non-zero offset per position so that your panel isn't required to be exactly on the edges.
  
## Usage

Import the namespace where required:

```csharp
using TheLiquidFire.UI;
```

### Without Animation

Obtain a reference to a `Panel` (here named "panel"), then `SetPosition` based on the position name you configured in the Setup step.  Pass a bool to determine whether the change should be animated:

```csharp
// When ready to apply Show position
panel.SetPosition("Show", false);

// When ready to apply Hide position
panel.SetPosition("Hide", false);
```

### With Animation

Additionally import the namespace where required:

```csharp
using TheLiquidFire.Animation;
```

The animation of a `Panel` is driven by my dynamic animation library.  You may optionally grab a reference to a returned `Tweener` and edit any animation values you like:

```csharp
var tweener = panel.SetPosition("Show", true);
tweener.duration = 0.25f;
tweener.equation = EasingEquations.EaseOutBack;
```
