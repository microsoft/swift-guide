# File Organization

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

## Convention - Grouping
Use `// MARK: Some text comment` to group related methods into sections. For example, in a view controller class, there might be `Setup`, `Layout`, and `Event Handlers` sections. 
When marking a section of methods belonging to a superclass or a protocol, use the actual name of the superclass or protocol type instead of a loose translation. If there are multiple protocols, methods should be grouped by individual protocols. Note: this convention only applies to protocol adoption without extensions because the keyword `extension` will automatically put the protocol section in its own group.

## Rationale
Grouping related methods into sections help with code organization and navigation.

## Examples

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

// MARK: - UITableViewDelegate

public func tableView(_ tableView: UITableView, viewForHeaderInSection section: Int) -> UIView? {
	...
}

// MARK: - UITableViewDataSource

public func numberOfSections(in tableView: UITableView) -> Int {
	...
}

public func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
	...
}
```
