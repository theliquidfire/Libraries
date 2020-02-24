# Animation

This library was originally created as part of my blog series, Dynamic Animation:
- [Part 1](http://theliquidfire.com/2015/01/02/dynamic-animation-part-1/)
- [Part 2](http://theliquidfire.com/2015/01/09/dynamic-animation-part-2/)

It has since been used in several of my [tutorial projects](http://theliquidfire.com/projects/) and has changed a little over time.

## Features

- Dynamic animation
- Lots of easing equations to pick from
- Choose between delta time, unscaled delta time, and fixed delta time for updates
- Loop, however many times you like, including forever with a simple repeat or ping-pong style
- Callback events for each Update Step, State Change, Looping and Completion
- Extensions make common animations (like moving a Transform) as simple as a single line of code
- Subclass different types of `Tweener` to add functionality where needed

## Usage

Import the namespace where required:

```csharp
using TheLiquidFire.Animation;
```

Utilize extensions to initiate an animation.  Animate using default duration and easing curve:

```csharp
transform.MoveTo(new Vector3(1, 2, 3));
```

The duration and easing curve are optional:

```csharp
transform.MoveTo(new Vector3(1, 2, 3), 1f, EasingEquations.EaseOutBounce);
```

To customize an animation, just keep a reference to the returned `Tweener`:

```csharp
var tweener = transform.MoveTo(end.position, duration, curve);

// Modifiy any other property such as loop type, etc
tweener.loopType = EasingControl.LoopType.PingPong;

// Register for completion callback
tweener.completedEvent += Tweener_completedEvent;
```

## Built-in Extensions

- RectTransform
  - AnchorTo: animate the anchored position
- Transform:
  - MoveTo: animate the world position
  - MoveToLocal: animate the local position
  - RotateTo: animate the rotation quaternion
  - RotateToLocal: animate the local euler angles
  - ScaleToLocal: animate the local scale
  
## Custom Animation

- Subclass `Tweener` for any `float` related animation
- Subclass `Vector3Tweener` for any `Vector3` related animation
- Subclass `QuaternionTweener` for any `Quaternion` related animation
  
