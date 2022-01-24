# Range Operators

## Convention

Prefer the half-open range operator `(a..<b)` over the closed range operator `(a...b)` when not including the final value.

## Rationale

Much like using `<` instead of `<=`, using the half-open range operator allows you to exclude the final value without the need of additional arithmetic. That being said, if you intend to use the final value, the closed range operator is still suitable.

## Examples

### Array Iteration
```swift
let oneToFive = ["one", "two", "three", "four", "five"]
let count = oneToFive.count

// really bad: off by one
for i in 0...count {
    print("\(i+1) is \(oneToFive[i])")
}
//1 is one
//2 is two
//3 is three
//4 is four
//5 is five
//Fatal error: Index is out of range

// bad: Additional arithemtic makes the end value less clear
for i in 0...count-1 {
    print("\(i+1) is \(oneToFive[i])")
}
//1 is one
//2 is two
//3 is three
//4 is four
//5 is five

// good: Clearly shows that loop will end just before `count`
for i in 0..<count {
    print("\(i+1) is \(oneToFive[i])")
}
//1 is one
//2 is two
//3 is three
//4 is four
//5 is five

## Resources
[Range Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html#ID73)
