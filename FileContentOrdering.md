# File Content Ordering

## Convention

Most "important" stuff at the top; and least "important" stuff at the bottom. The importance is usually determined by the [access level](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html); the less restrictive the access level, the more "important" it is.

## Rationale

Ordering file contents by access level ensures that the entities with the least restrictive access level get the most visibility, which are likely the components that developers interact with the most.

## Example

```swift
// public enums, classes, interfaces etc.
public class House {

    // public functions
    public init {
    // ...
    }

    // public variables
    public static let continent = "Westeros"

    // internal functions
    internal func addHouseMember() {
    // ...
    }

    // internal variables
    internal let sigil: Animal

    // fileprivate functions
    fileprivate func updateHouseAllegiance() {
    // ...
    }

    // fileprivate variables
    fileprivate var hasAllies: Bool

    // private functions
    private func reorganizeHouse() {
    // ...
    }

    // private variables
    private var size: Int = 0

}

// internal functions
internal func updateUnalliedHouses(_ houses: [House]) {
    houses.forEach { house in
        // since this top-level function is in the same file, it can access fileprivate funcs and vars
        if !house.hasAllies {
            house.updateHouseAllegiance()
        }
    }
}

// private extensions or constants
private maximumHouseSize: Int = 50
```

## Convention - Constants

Use nested structs to group constants when possible.

## Rationale

This reduces verbosity and provides structure.

## Example

```swift
class FruitSellerView: UIView {
    ...

    // bad: no separation between rotation and fade animation constants, long constant names are harder to read

    static let rotationAnimationangle: CGFloat = .pi / 45.0
    static let rotationAnimationdelay: CGFloat = 0.15
    static let rotationAnimationduration: CGFloat = 0.3
    static let rotationAnimationspeed: CGFloat = 100
    static let fadeAnimationdelay: CGFloat = 0.1
    static let fadeAnimationduration: CGFloat = 0.25
    static let fadeAnimationspeed: CGFloat = 200
}

class FruitSellerView: UIView {
    ...

    // good: split rotation and fade animation constants into different groups

    private struct RotationAnimationConstants {
        static let angle: CGFloat = .pi / 45.0
        static let delay: CGFloat = 0.15
        static let duration: CGFloat = 0.3
        static let speed: CGFloat = 100
    }

    private struct FadeAnimationConstants {
        static let delay: CGFloat = 0.1
        static let duration: CGFloat = 0.25
        static let speed: CGFloat = 200
    }
}
```
