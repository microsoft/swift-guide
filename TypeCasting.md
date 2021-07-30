# Type Casting

In general, follow the [official guidelines](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html).

## Convention - Static casting
Use keyword `as` for static casting. Only use static casting when automatic type casting is not available or when the compiler's inferred type does not match the intended type.

## Rationale
Compiler can infer most types correctly so static casting is not necessary in most cases.

## Examples 

``` swift
// Bad: unnecessary type casting
let padding = 42 as CGFloat

// Good: use type annotations instead
let padding: CGFloat = 42
```

### Necessary type casting

``` swift
// setTelemetryID is an Objective-C function that takes an NSNumber as the argument
// id is of type Int, the casting to NSNumber is not automatic
button.setTelemetryID(id as NSNumber)

let x = 10
switch x {
// Without the type cast, 1...Int.max would be interpreted as Range type
case 1...Int.max as ClosedInterval:
    ...
case Int.min..<0 as HalfOpenInterval:
    ...
case 0:
    ...
}

```
