# Early Return

## Convention

It's recommended to use `guard ... else` statements and early exits on top of a function to validate parameters or other variables.

## Syntax
``` Swift
func someFunction(argumentLabel parameterName: parameterType) {
    guard condition else {
        // log error or other actions
        return
    }
}
```
For more information about `guard ... else`, follow the [language guide](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID525).

## Rationale

Using a guard statement to return early prevents parentheses nesting and better preserves variable immutability.

## Examples

### Good: with early return, return value is a constant

```Swift
class ElementList {

    func index(of element: Element) -> Int? {
        guard let elements = self.elements else {
            return nil
        }

        let elementIndex = elements.index(of: element)
        guard elementIndex != NSNotFound else {
            log("Element not found")
            return nil
        }

        return elementIndex
    }

}

    var elements: ElementList?
}

```

### Bad: without early return, return value is a variable

```Swift
class ElementList {

    func index(of element: Element) -> Int? {
        // The following variable is a variable
        var index: Int? = nil
        if let elements = self.elements {
            let elementIndex = elements.index(of: element)
            if elementIndex != NSNotFound {
                index = elementIndex
            } else {
                log(("Element not found")
            }
        }

        return index
    }
}

    var elements: ElementList?
}

```
