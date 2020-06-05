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
    ...
    }

    // public variables
    public static let continent = "Westeros"

    // internal functions
    internal func addHouseMember() {
    ...
    }

    // internal variables
    internal let sigil: Animal

    // private functions
    private func reorganizeHouse() {
    ...
    }

    // private variables
    private var size: Int = 0

}

// fileprivate extensions or constants
fileprivate maximumHouseSize: Int = 50
```

