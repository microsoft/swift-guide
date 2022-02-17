# File Organization

## MARK Comments

The special `// MARK: Some text` comment should be used to group related methods into sections (`#pragma mark` in objc).

<img width="529" alt="Example of using the MARK syntax in comments to split the navigator into sections" src="https://user-images.githubusercontent.com/1363082/154284314-33610b82-62c0-4840-a037-7eba8b8a3269.png">

This menu can be revealed either by tapping the name of the current method in the "jump bar" at the top of your source editor or by pressing `^6` (you can rebind this to something more convenient). One great feature of this method list is that you can type to fuzzy filter the list and press `[Return]` to jump to the selected method.

You may also use `// MARK: - Some text` to insert a dividing line (such as you can see for "Notifications" and "UIScrollViewDelegate")

Xcode is flexible with whitespace here, but our rules are:

1. There should be a single space between `//` and `MARK`
2. There should be no space between `MARK` and `:`

3. There should be a single space after the `:`
4. If using a line, it should be after the space from point #3 and should have a space afterwards if using text as well

Please attempt to follow these recommendations when marking groups of methods:

1. When marking a section *within* a type declaration or extension, use `// MARK: Some label` (no hyphen). If the section is *outside* a type declaration, use `// MARK: - Some label` (with a hypen).
2. When separating the methods within a `UIViewController`, attempt to use these standardized section names:
    - "Init" (grouping together `init()` and `deinit()`, if any)
    - "Setup"
    - "Layout"
    - "Notifications" and "Actions" (event handlers)
    - "Helpers"
3. When marking a section of methods belonging to a superclass or a protocol, use the actual name of the superclass or protocol type instead of a loose translation
    - :white_check_mark: `// MARK: - UITableViewDelegate`
    - :x: `// MARK: - Table view delegate`
4. In some cases it may make more sense for a method to be moved to a functional section instead of just being grouped based on class hierarchy
    - for instance, `becomeFirstResponder` should belong to a `UIResponder` mark section
    - `sizeThatFits:` should probably belong to a `Layout` section rather than `UIView` since the functionality trumps where it was inherited from


### Example

``` swift

// bad: does not use the name of the protocol as the name of the section
// MARK: - Table view delegate
...

// good: use the name of the protocol directly as the name of the section
// MARK: - UITableViewDelegate
...

// bad: using the same section for UITableViewDelegate and UITableViewDataSource protocols

// MARK: - UITableViewDelegate and UITableViewDataSource

public func tableView(_ tableView: UITableView, viewForHeaderInSection section: Int) -> UIView? {
	...
}

public func numberOfSections(in tableView: UITableView) -> Int {
	...
}

public func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
	...
}

// good: using different sections for UITableViewDelegate and UITableViewDataSource protocols

// MARK: UITableViewDelegate

public func tableView(_ tableView: UITableView, viewForHeaderInSection section: Int) -> UIView? {
	...
}

// MARK: UITableViewDataSource

public func numberOfSections(in tableView: UITableView) -> Int {
	...
}

public func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
	...
}
```


## Convention - Ordering

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

Use structs or nested structs to group constants when possible; the grouping should be based on logical use instead of structure or type of the constants.

## Rationale

This reduces verbosity and provides structure.

## Example

```swift
class FruitSellerView: UIView {
    ...

    // bad: no separation between rotation and fade animation constants, long constant names are harder to read
    private struct Constants {
        static let rotationAnimationAngle: CGFloat = .pi / 45.0
        static let rotationAnimationDelay: CGFloat = 0.15
        static let rotationAnimationDuration: CGFloat = 0.3
        static let rotationAnimationSpeed: CGFloat = 100
        static let fadeAnimationDelay: CGFloat = 0.1
        static let fadeAnimationDuration: CGFloat = 0.25
        static let fadeAnimationSpeed: CGFloat = 200
    }

    // bad: the name "Strings" does not provide helpful about how the constants are used.
    private struct Strings {
        static let rotationAnimationIdentifier: String = "FruitSellerViewRotationAnimationIdentifier"
        static let fadeAnimationIdentifier: String = "FruitSellerViewFadeAnimationIdentifier"
    }
}

class FruitSellerView: UIView {
    ...

    // good: split rotation and fade animation constants into different groups

    private struct RotationAnimationConstants {
        static let angle: CGFloat = .pi / 45.0
        static let delay: CGFloat = 0.15
        static let duration: CGFloat = 0.3
        static let speed: CGFloat = 100
        static let identifier: String = "FruitSellerViewRotationAnimationIdentifier"
    }

    private struct FadeAnimationConstants {
        static let delay: CGFloat = 0.1
        static let duration: CGFloat = 0.25
        static let speed: CGFloat = 200
        static let identifier: String = "FruitSellerViewFadeAnimationIdentifier"
    }
}
```
