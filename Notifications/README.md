# Notifications

This library was originally developed as part of my blog series, Social Scripting:
- [Part 1](http://theliquidfire.com/2014/12/08/social-scripting-part-1/)
- [Part 2](http://theliquidfire.com/2014/12/10/social-scripting-part-2/)
- [Part 3](http://theliquidfire.com/2014/12/10/social-scripting-part-3/)

## Features

- Any object can post any notification
- Any object can observe any notification
- Observation can target a specific sender or any sender
- Notification names can be dynamic (it's just a string)
- Notifications can include any extra information
- Notifications do not have to be handled, so you don’t have to check that they exist
- Handlers are only added once per notification, even if you “accidentally” add it multiple times

## Usage

Import the namespace where required:

```csharp
using TheLiquidFire.Notifications;
```

### Posting

Any object may post any notification.  Pass along a `string` to name the notification:

```csharp
this.PostNotification(NotificationName);
```

To post a notification with a additional information, pass along any type of `System.Object`:

```csharp
this.PostNotification(NotificationName, NotificationInfo);
```

### Observing

You may use a method as the notification handler.  It must have a signature that is compatible with `System.Action<System.Object, System.Object>`:

```csharp
void OnNotification(object sender, object args)
{
    // Do stuff here
}
```

Any object may observe any notification.  To register as an observer, you must pass a handler method and the name of the notification to observe.  The following example will observe all posted notifications with the name `NotificationName` from any sender.

```csharp
// Register, perhaps added to `OnEnable`
this.AddObserver(OnNotification, NotificationName);

// Un-register, perhaps added to `OnDisable`
this.RemoveObserver(OnNotification, NotificationName);
```

You may also choose to only observe notifications that are posted by a specified `target` object:

```csharp
// Register, perhaps added to `OnEnable`
this.AddObserver(OnNotification, NotificationName, target);

// Un-register, perhaps added to `OnDisable`
this.RemoveObserver(OnNotification, NotificationName, target);
```

### Warning

This `NotificationCenter` maintains a strong reference to the notification observers.  Therefore it is very important to pair each `AddObserver` with a `RemoveObserver`.  I tend to use the `MonoBehaviour` methods `OnEnable` and `OnDisable` as a good opportunity to add and remove notifications.
