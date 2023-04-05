# Flutter Draggable Menu (draggable_menu)
[![Pub](https://img.shields.io/badge/pub-v0.1.0-%237f7eff?style=flat&logo=flutter)](https://pub.dev/packages/draggable_menu)
[![GitHub](https://img.shields.io/badge/GitHub-v0.1.0-%237f7eff?style=flat&logo=github)](https://github.com/emresoysuren/draggable_menu)

With `draggable_menu`, create Draggable Menus as you want and make your app look way better and more convenient.

`draggable_menu` also allows you to customize the UI and the animations. You can use one of the default themes or create your custom UI from scratch.

| Modern | Modern (Expandable) | Classic | Classic (Expandable) |
|---|---|---|---|
|<img height="320" src="https://github.com/emresoysuren/draggable_menu/blob/read-me-assets/modern-1.gif?raw=true">|<img height="320" src="https://github.com/emresoysuren/draggable_menu/blob/read-me-assets/modern-2.gif?raw=true">|<img height="320" src="https://github.com/emresoysuren/draggable_menu/blob/read-me-assets/classic-1.gif?raw=true">|<img height="320" src="https://github.com/emresoysuren/draggable_menu/blob/read-me-assets/classic-2.gif?raw=true">|

# Quick Start
To start as fast as possible, you need to know how to create and open it.

## Create the Draggable Menu
Create a Draggable Menu widget with a child.

```dart
DraggableMenu(
  child: child, // Optional
)
```

## Open the Draggable Menu
Open the menu by calling Draggable Menu's static `open` method.

```dart
DraggableMenu.open(
  context,
  DraggableMenu(
    child: child, // Optional
  ),
)
```

You can use the Draggable Menu inside of another widget, and give it to the `open` method. Like this:

```dart
DraggableMenu.open(
  context,
  MyCustomDraggableMenu(),
)
```

Note: *The `DraggableMenu.open()` shouldn't be in the same place as the `MaterialApp` widget.*


# Parameters of DraggableMenu

| Category | Parameters | Description |
|---|---|---|
| Constraints | double? minHeight | It specifies the min-height of the Draggable Menu. If the child's height is higher, it will take its child's height instead. |
| Constraints | double? maxHeight | It specifies the max-height of the Draggable Menu's minimized status (Not Expanded). When the menu is expanded, it takes its `expandedHeight` parameter's value as its height. To be able to use an expandable draggable menu, the `expandedHeight` parameter must be higher than the `maxHeight` parameter. |
| Constraints | double? expandedHeight | It specifies the height of the Draggable Menu when it's expanded. To be able to use an expandable draggable menu, the `expandedHeight` parameter must be higher than the `maxHeight` parameter, and the `expandable` parameter mustn't be null. |
| Usage | bool? expandable | It specifies whether the Draggable Menu will be expandable or not. The `expandedHeight` parameter must be provided to use an expandable draggable menu. |
| Usage | double? closeThreshold | Specifies the Close Threshold of the Draggable Menu. Takes a value between `0` and `1`. |
| Usage | double? expandThreshold | Specifies the Expand Threshold of the Draggable Menu. Takes a value between `0` and `1`. |
| Usage | double? minimizeThreshold | Specifies the Minimize Threshold of the Draggable Menu. Takes a value between `0` and `1`. |
| UI | Widget? child | Adds a child inside the Draggable Menu's Default UI. |
| UI | Color? color | Specifies the Background color of the Default UIs. |
| UI | Color? accentColor | Specifies the Bar Item color of the Default UIs. |
| UI | double? radius | Specifies the radius of the Default UIs. |
| UI | DraggableMenuUiType? uiType | Specifies the Default UI Type. |
| UI | Widget? barItem | Overrides the Default Bar Item of the Default UIs. |
| UI | Widget? customUi | Overrides the Default UIs. |
| Listener | Function(DraggableMenuStatus status)? addStatusListener | Adds a listener to listen to its Status. |
| Listener | final Function(double menuValue)? addValueListener | Adds a listener to listen to its Menu Value. |
| Animation | Duration? animationDuration | Specifies the duration of the Draggable Menu's animations. |
| Animation | Curve? curve | Specifies the curve of the Draggable Menu's animations. |

# How To Use

## Create a Draggable Menu and Open it
You can create a Draggable Menu by just using this:

```dart
DraggableMenu(
  child: child, // Optional
)
```

After that, you will probably want to push the Draggable Menu to the screen. To do that, use `Navigator`'s methods (e.g. `push`) or the Draggable Menu's `open` or `openReplacement` methods. They are the same with just a little difference. The `openReplacement` method replaces the previous root (e.g. `Navigator.pushReplacement`).

```dart
DraggableMenu.open(
  context,
  DraggableMenu(
    child: child, // Optional
  ),
  barrier: barrier, // Optional. If it's true uses a root with barrier.
  barrierColor: barrierColor, // Optional. Changes the barrier's color.
  animationDuration: animationDuration, // Optional. Specifies its animation's duration.
  curve: animationDuration, // Optional. Specifies its animation's curve.
)
```

---

## Use the Expandable Draggable Menu
To do that, first, you should set the `expandable` parameter to true, and then set the value of the `expandedHeight` parameter.

The `expandedHeight` parameter mustn't be null or smaller than the child's height or the `maxHeight` or the `minHeight` parameters.

```dart
DraggableMenu(
  expandable: true,
  expandedHeight: expandedHeight,// Mustn't be null or smaller than its widget's height or the "maxHeight" or the "minHeight" parameters. 
  maxHeight: maxHeight, // Optional
  minHeight: minHeight, // Optional
  child: child, // Optional
)
```

---

## Use Different UIs
Use different UIs by setting the `uiType` parameter. The `uiType` parameter takes DraggableMenuUiType. And DraggableMenuUiType currently has these:
* Classic
* Modern
* Soft Modern

The `uiType` param is optional, so if you don't use it, its default value is `DraggableMenuUiType.classic`.

```dart
DraggableMenu(
  uiType: DraggableMenuUiType.modern,
  child: child, // Optional
)
```

---

## Using Scrollables
While using scrollable with a Draggable Menu you need to add the `ScrollableManager` widget above the scrollable you want to control Draggable with and set the physics of the Scrollable (e.g. ListView) to `NeverScrollableScrollPhysics`. The `ScrollableManager` widget must be under a `DraggableMenu` widget. You can do it by just simply using your widgets under its `child` or `customUI` parameters.

```dart
DraggableMenu(
  child: ScrollableManager(
    child: ListView(
      physics: const NeverScrollableScrollPhysics(),
    ), // You can use any scrollable widget
  ),
)
```

If there will be more than one `ScrollableManager` at the same time, give each scrollables different controllers.

In short, do not forget to use `ScrollableManager` and set the physics of the scrollable you want to `NeverScrollableScrollPhysics`.

Extra: *Check out the `ScrollableManager`'s `enableExpandedScroll` parameter.*

---

## Using the Status Listener
Use the `addStatusListener` parameter to listen to the Draggable Menu's status. 

### Dragable Menu's status are:
* Closing
* MayClose
* Canceling
* Minimized
* Minimizing
* May Expand
* May Minimize
* Expanding
* Expanded

You can point them out with `DraggableMenuStatus` like:
```dart
DraggableMenu(
  addStatusListener: (status) {
    if (status == DraggableMenuStatus.mayExpand) {
      // Add something to do when its status is mayExpand
    }
    // Add something to do when its status change
  }
  child: child, // Optional
)
```

---

<!-- ## Using Custom UI -->



Note: *You can find more examples in the [Draggable Menu Example](https://github.com/emresoysuren/draggable_menu/tree/main/example) app.*

*For more info, check out the [GitHub Repository](https://github.com/emresoysuren/draggable_menu).*