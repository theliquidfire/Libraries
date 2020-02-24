# Data Types

This library was created and used throughout many projects on my blog.  See more here [TheLiquidFire](http://theliquidfire.com/2014/12/08/social-scripting-part-1/)

## Point

A simple struct holding `x` and `y` values of type `int`.  Useful for any scenario where the ability to compare whole numbers rather than floating point numbers is desired.  

### Features

- Conforms to `[System.Serializable]`
- Implements `IEquatable`
- Provided operator overloads: `+`, `-`, `==`, `!=`
- Implicit to `Vector2`

### Usage

Import the namespace where required:

```csharp
using TheLiquidFire.DataTypes;
```

Create:

```csharp
var position = new Point(3, 4);
```

Use:

```csharp
var lhs = new Point(3, 4);
var rhs = new Point(1, 2);
var added = lhs + rhs; // (4, 6)
var subtracted = lhs - rhs; // (2, 2)
var checkEqual = lhs == rhs; // False
var checkNotEqual = lhs != rhs; // True

var list = new List<Point>();
list.Add(new Point(3, 4));
if (list.Contains(lhs))
{
	// Executes
}
```
