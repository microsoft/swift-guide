# Comments

In general, follow the comments section in the [official guidelines](https://swift.org/documentation/api-design-guidelines/#fundamentals).

## Convention
Comments should be written in full US English prose, with correct grammar and punctuation.

## Rationale
Correct grammar and punctuation helps the documentation maintain clarity.

## Convention - Documentation
All public declarations in your code base, such as classes, enums, functions, properties should have documentation. The outline of the documentation can be inserted in Xcode by pressing `CMD` + `Option` + `/` when the cursor is immediately above a method, class, etc or by selecting Xcode menu bar -> Editor -> Structure -> Add Documentation.

## Rationale
Clear documentation promotes others' better understanding of the source code and facilitates reviews and usages. In addition, Documentation automatically shows up in Xcode code completion and Quick Help to help with precise usage.

## Examples

### Bad: Insufficient enum description; there is no documentation on the enum cases

``` swift
public enum ShimmerStyle {
    case concealing
    case revealing
}

```

### Good: clear documentation that explains the different enum cases

``` swift
/// The style affects how shimmer is animated 
public enum ShimmerStyle {
    /// The gradient conceals parts of the subviews as it moves leaving most parts of the subviews unblocked.
    case concealing

    /// The gradient reveals parts of the subviews as it moves leaving most parts of the subview blocked.
    case revealing
}
```

## Convention - Inline Comments
There are three main purposes of inline comments:
- Explain why the code is implemented in a certain way and give extra context.
- Explain complex code that's not obvious.
- Break up code blocks into chunks (when refactoring is not desirable).

## Rationale
Adding inline comments brings clarity and readability to complex code and logic.

## Examples

### Bad: does not explain why the property someEventBridge is a weak reference.

``` swift
class SomeView: NSView {
    private weak var someEventBridge: EventBridge?
}
```

### Good: explains why the property someEventBridge is a weak reference.

``` swift
class SomeView: NSView {
    // Using weak here because lifetimes of SomeView and someEventBridge
    // are not related. It is possible that someEventBridge outlives SomeView.
    private weak var someEventBridge: EventBridge?
}
```

### Bad: no explanation on how the finalScore is calculated

``` swift
let finalScore = scores.reduce(0, combine: +) / Double(scores.count)
```

### Good: explain in an easily understandable way how finalScore is calculated

``` swift
// Compute the final score as the arithmetic mean of the previous scores
let finalScore = scores.reduce(0, combine: +) / Double(scores.count)
```

### Bad: one big chunk of code

``` swift
func loadLastCheckpoint() -> GameState? {
    let defaultDataPath = getDefaultDataPath()
    guard let saveFilePath = defaultDataPath.appendingPathComponent("SaveFile.dat") else {
        return nil
    }
    guard let dataContents = try? NSData(contentsOfFile: saveFilePath) else {
        return nil
    }
    guard let loadedState = GameState.deserialize(dataContents) else {
        return nil
    }
    loadedState.resetToLastCheckpoint()
    return loadedState
}
```

### Good: break up code blocks into chunks

``` swift
func loadLastCheckpoint() -> GameState? {
    // Determine the path to the file on disk
    guard let saveFilePath = defaultDataPath.appendingPathComponent("SaveFile.dat") else {
        return nil
    }

    // Load in the serialized state
    guard let dataContents = try? NSData(contentsOfFile: saveFilePath) else {
        return nil
    }

    // Deserialize
    guard let loadedState = GameState.deserialize(dataContents) else {
        return nil
    }

    // Reset to checkpoint and return
    loadedState.resetToLastCheckpoint()
    return loadedState
}
```
