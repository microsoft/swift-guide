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

// bad: Additional arithemtic makes the end value less clear
for i in 0...count-1 {
    print(oneToFive[i])
}
//one
//two
//three
//four
//five

// good: Clearly shows that loop will end just before `count`
for i in 0..<count {
    print(oneToFive[i])
}
//one
//two
//three
//four
//five

// good: One-Sided Ranges can also be used to show the range is from the start to just before `count`
for number in oneToFive[..<count] {
    print(number)
}
//one
//two
//three
//four
//five

## Resources
[Range Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html#ID73)
