# Range Operators

## Convention

Prefer the half-open range operator `(a..<b)` over the closed range operator `(a...b)` when not including the final value.

## Rationale

Much like using `<` instead of `<=`, using the half-open range operator allows you to exclude the final value without the need of additional arithmetic. That being said, if you intend to use the final, the closed range operator is still suitable.

## Examples

### Array Iteration
```swift
let oneToFive = ["one", "two", "three", "four", "five"]
let count = oneToFive.count

// really bad: off by one
for i in 0...count {
    print(oneToFive[i])
}
//one
//two
//three
//four
//five
//Fatal error: Index is out of range

// bad:
for i in 0...count-1 {
    print(oneToFive[i])
}
//one
//two
//three
//four
//five

// good:
for i in 0..<count {
    print(oneToFive[i])
}
//one
//two
//three
//four
//five

// good: One-Sided Ranges can also be used
for number in oneToFive[..<count] {
    print(number)
}
//one
//two
//three
//four
//five

// fine:
for i in 1...5 {
    print(i)
}
//1
//2
//3
//4
//5
```

### Repeated Actions
```swift
// bad:
let tenRandomNumbers: [Float] = (1...10).map {_ in Float.random(in: 0..<1)}

// good:
let tenRandomNumbers: [Float] = (0..<10).map {_ in Float.random(in: 0..<1)}
```

## Resources
[Range Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html#ID73)
