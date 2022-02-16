# Type Inference

## Convention

Use type annotation as little as possible when declaring a constant or a variable; instead let the compiler infer the variable type. This convention does not apply to properties.

## Rationale

Type inference helps reduces line noise and maintain clearer code.

## Shorthand Dot Syntax

When assigning an enum or a static property to a variable or a constant, if the type of the variable or the constant is known, use the shorthand dot syntax to access the enum or static property.

### Examples

#### Good: use shorthand dot syntax

``` swift
func layout(with direction: NSUserInterfaceLayoutOrientation) {
    switch direction {
    case .horizontal:
        layoutHorizontally()
    case .vertical: 
        layoutVertically()
    }
}

```

#### Bad: unnecessarily verbose without shorthand dot syntax

``` swift
func layout(with direction: NSUserInterfaceLayoutOrientation) {
    switch direction {
    case NSUserInterfaceLayoutOrientation.horizontal:
        layoutHorizontally()
    case NSUserInterfaceLayoutOrientation.vertical: 
        layoutVertically()
    }
}

```

## Constants and Variables

Let the compiler infer the type of a constant or variable whenever possible. 

### Examples

#### Good: no left-hand-side type annotations

``` swift
let horizontalMargin = 10

let font = NSFont.systemFont(ofSize: 15.0)
```

#### Bad: with unnecessary left-hand-side type annotations

``` swift
let horizontalMargin: Int = 10

let font: NSFont = NSFont.systemFont(ofSize: 15.0)
```

## Properties

Use type annotations instead of type inference for properties for API clarity.

### Examples

#### Good: property use type annotations 

``` swift
class CustomLabel {
    let textColor: UIColor = .white
}
```

#### Bad: property does not use type annotations 

``` swift
class CustomLabel {
    let textColor = UIColor.white
}
```

## Casting

### The `as` keyword

There are 3 forms of the `as` keyword:

- `as`: static typecast
- `as?`: runtime, conditional typecast
- `as!`: runtime, forced typecast

The first form, `as`, should only be used as a sub-expression within a larger expression, such as
```swift
let baseFilename = (fullPath as NSString).stringByDeletingPathExtension
```

It should not be used in a simple expression such as:
```swift
let padding = 42 as CGFloat
```

Instead, the constant on the left-hand side should be declared to be of `CGFloat` type
```swift
let padding: CGFloat = 42
