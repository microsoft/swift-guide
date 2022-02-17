# Annotations and Modifiers

## Annotations

Method/variable annotations should go on the _same_ line as the rest of the definition. i.e.

```swift
// good: On the same line
@objc func doThing() { }

// bad: Not on the same line
@objc
func doThing() { }
```

There is an exception for when you are renaming for Objective-C. In that case, the annotation _may_ go on the preceeding line. e.g.

```swift
@objc(XYThing)
enum Thing: Int {
...
}
```

Regarding ordering, the rules defined by SwiftLint should be followed.

## Modifiers

Similarly, modifiers should go on the same line and follow SwiftLint conventions for order. e.g.

```swift
override open class func whatever() { }
```
