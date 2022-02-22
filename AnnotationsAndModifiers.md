# Annotations and Modifiers

## Convention

Method/variable annotations and modifiers should go on the _same_ line as the rest of the definition. i.e.

## Rationale

Consistency makes PRs easier to read as well as removing any potential disagreements. 

## Annotations


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

The ordering for the annotations follows [that of SwiftLint](https://realm.github.io/SwiftLint/modifier_order.html). i.e. `@objc`, `@nonobjc`, `@objcMembers`, `@IBAction`, `@IBOutlet`, `@IBDesignable`, `IBInspectable`, `@NSManaged`, `@NSCopying`


## Modifiers

Similarly, modifiers should go on the same line and follow SwiftLint conventions for order. e.g.

Regarding the ordering of the annotations, we again follow SwiftLint. i.e. The order should be:

* `override` - Specify if this is an override or not
* Access level (e.g. `private`, `public`, `open`, etc.)
* Setter access level
* `dynamic` - Specify if dynamic dispatch should be used
* Mutators - `mutating` or `nonmutating`
* `lazy` - Specify if this declaration is lazy or not
* `final` - Specify if this declaration is final
* `required` - Specify if an initializer is required or not
* `convenience` - Specify if a declaration as convenient or not
* `static` - Specify if this is static or not <!-- Swiftlint refers to these as "type methods" but I can't think of any alternatives to static that would be left? -->
* `weak` - Specify if the ownership is weak or not