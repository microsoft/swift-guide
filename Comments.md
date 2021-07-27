# Comments

In general, follow the comments section in the [official guidelines](https://swift.org/documentation/api-design-guidelines/#fundamentals).

## Convention
Comments should be written in full US English prose, with correct grammar and punctuation.

## Rationale
Correct grammar and punctuation helps the documentation maintain clarity.

## Convention - Documentation
All public declarations in your code base, such as classes, enums, functions, properties should have documentation. The outline of the documentation can be inserted in Xcode by pressing `CMD` + `Option` + `/` when the cursor is immediately above a method, class, etc or by selecting Xcode menu bar -> Editor -> Structure -> Add Documentation.

## Rationale
Clear documentaiton promotes better understanding of the source code. In addition, Documentation automatically shows up in Xcode code completion and Quick Help to help with precise usage.

## Examples

### Bad: Description of the enum is not informational; there is no documentation on the enum cases

``` swift
/// Shimmer style can be either concealing or revealing
public enum ShimmerStyle {
    case concealing
    case revealing
}

```

### Good: clear documentation that explains the different enum cases

``` swift
/// Shimmer style can be either concealing or revealing
/// The style affects how shimmer is animated 
public enum ShimmerStyle {
    /// Concealing shimmer: the gradient conceals parts of the subviews as it moves leaving most parts of the subviews unblocked.
    case concealing

    /// Revealing shimmer: the gradient reveals parts of the subviews as it moves leaving most parts of the subview blocked.
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

### Bad: does not explain why the the expand() function is called under a specific condition

``` swift
class SomeView {
    ...
    override func mouseEntered(with event: NSEvent) {
        if !animationPlaying {
            expand()
        }
    }

    func expand() {
        ...
    }
}
```

### Good: explains why the expand() function is called under a specific condition

``` swift
class SomeView {
    ...
    override func mouseEntered(with event: NSEvent) {
        // There are multiple mouse enter events fired during the expand/collapse animation because the tracking area is constantly changing. Only respond to the initial event.
        // Only respond to the events when animation is not playing
        if !animationPlaying {
            expand()
        }
    }

    func expand() {
        ...
    }
}
```

### Bad: no explanation on how the finalScore is calculated

``` swift
let finalScore = scores.reduce(0, combine: +) / Double(scores.count)
}
```

### Good: explain in an easily understandable way how finalScore is calculated

``` swift
// Compute the final score as the arithmetic mean of the previous scores
let finalScore = scores.reduce(0, combine: +) / Double(scores.count)
}
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
    let defaultDataPath = getDefaultDataPath()
    guard let saveFilePath = defaultDataPath.appendingPathComponent("SaveFile.dat") else {
        return nil
    }

    // Load in the serialized state
    guard let dataContents = try? NSData(contentsOfFile: saveFilePath) else {
        return nil
    }

    // Deserialize, reset to checkpoint and return
    guard let loadedState = GameState.deserialize(dataContents) else {
        return nil
    }

    loadedState.resetToLastCheckpoint()
    return loadedState
}
```
