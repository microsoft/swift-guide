# Property observers

In general, follow the [official guidelines](https://docs.swift.org/swift-book/LanguageGuide/Properties.html).

## Convention

Use guard statements to check if the property has changed in property observers.

## Rationale

Checking whether the property value has actually changed can help avoid potentially expensive work.

## Examples

### Good: with `guard` statement, avoid doing unnecessary work

``` Swift
var propWithAnObserver: Bool {
    didSet {
        guard oldValue != propWithAnObserver else {
            return
        }
        expensiveWork(propWithAnObserver)
        needsLayout = true
    }
}
```

### Bad: without `guard` statement, do unnecessary work

``` Swift
var propWithAnObserver: Bool {
    didSet {
        expensiveWork(propWithAnObserver)
        needsLayout = true
    }
}
```

## Convention - Use `defer` statement to trigger property observers after the initializer executes
Swift does not call property observers when a class is setting its own properties in the initializer. Use a `defer` statement to wrap the property setting statements so that the property assignment and property observers are called after the initializer has been called. This can reduce duplicate code in the initializer.

### Exceptions
Since the property assignment happens after the initializer with the use of `defer`, this cannot be used on non-optional stored properties because non-optional stored properties require an assigned value before the initializer finishes. However, turning a non-optional stored property into an optional property just to avoid duplication is not recommended.

### Good: Avoid unnecessary duplicate calls to announceSymbol()

``` Swift
class House {
    init(symbol: String?) {
        defer {
            self.symbol = symbol
        }
    }

    var symbol: String? {
        didSet {
            guard oldValue != symbol else {
                return
            }
            announceSymbol()
        }
    }
}
```

### Bad: Unnecessary duplicate calls to announceSymbol()

``` Swift
class House {
    init(symbol: String?) {
        self.symbol = symbol
        announceSymbol()
    }

    var symbol: String? {
        didSet {
            guard oldValue != symbol else {
                return
            }
            announceSymbol()
        }
    }
}
```
