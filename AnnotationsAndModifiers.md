# Annotations and Modifiers

## Annotations

Method/variable annotations should go on the _same_ line as the rest of the definition. i.e.

```swift
@objc func doThing() { }
```

NOT

```
@objc
func doThing() { }
```

Regarding ordering, the rules defined by SwiftLint should be followed.

## Modifiers

Similarly, modifiers should go on the same line and follow SwiftLint conventions for order. e.g.

```swift
override open class func whatever() { }
```
