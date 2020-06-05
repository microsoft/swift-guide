# Naming

In general, follow the [official guidelines](https://swift.org/documentation/api-design-guidelines/#naming).

## Conventions

### Naming a file

There's no three-letter prefix in Swift file naming. For example, if an Objective-C file named XYZEvent.m is to be converted to Swift, it should be renamed to Event.swift.

### Naming a class or a protocol available in Objective-C

Provide a pre-fixed Objective-C name before the class or protocol definition. 

#### Example
``` swift
@objc class Event {
    // bad: exported to Objective-C as class Event without a prefix
}

@objc(XYZEvent)
class Event {
    // good
}
```

### Naming a protocol

There is no need to add a prefix to a Swift protocol in order to distinguish it from a Swift class or struct. 

- Protocols that describe what something is should read as nouns (e.g. Collection).

- Protocols that describe a capability should be named using the suffixes able, ible, or ing (e.g. Equatable, ProgressReporting)."

#### Example
``` swift
protocol IFooEventHandler {
    // bad: the "I" prefix is not necessary
}

protocol FooEventHandler {
    // bad: "er" is not a good suffix for a protocol
}

protocol FooEventHandling {
    // good
}
```
