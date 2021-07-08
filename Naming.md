# Naming

In general, follow the [official guidelines](https://swift.org/documentation/api-design-guidelines/#naming).

## Conventions

### Naming a file

- All Swift files should use the `.swift` extension.
- The name of a file should make it clear what the contents are. For example, if there is a single class named `EasyTapButton` then the file should be called `EasyTapButton.swift`. If you have a view controller, along with some helper types, then using the name of the view controller will likely be the best choice. A good heuristic to use is that if it's ever unclear what to name a file, it may be worth splitting that file up.
- There's no three-letter prefix in Swift file naming. For example, if an Objective-C file named XYZEvent.m is to be converted to Swift, it should be renamed to Event.swift.
- If a file contains extensions, then the file name should be `MyType+Extensions.swift` unless the extension is purely adopting a protocol; in that case the extension should be named `MyType+ProtocolBeingConformedTo.swift`, for example `MyDictionary+NSCopying`.swift

### Naming a class, a struct or a protocol

- Naming should be `UpperCamelCase`
- No Objective-C style prefixes should be used

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

- There is no need to add a prefix to a Swift protocol in order to distinguish it from a Swift class or struct. 
- A protocol that describes what something is should read as nouns (e.g. Collection).
- A protocol that describes a capability should be named using the suffixes able, ible, or ing (e.g. Equatable, ProgressReporting)."

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

### Naming a delegate method

The first parameter should always be the item that is calling the delegate method.

#### Rationale

Dedicating the first parameter to be the item that is calling the delegate method follows Apple's API [design pattern](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html#//apple_ref/doc/uid/20001282-1001803-BCIDAIJE).

#### Example:

```swift
// really bad: there's no parameter for the item that is calling the delegate method.
func didDeleteDraft()

// bad: the delegate method caller is not the first parameter
func didDeleteDraft(draft: Draft, draftManager: DraftManager)

// good
func draftManager(_ manager: DraftManager, didDeleteDraft draft: Draft)
```

### Naming an event handler method

An event handler method should be name following this pattern:

`handle<EventSource>[<Action>]`

where `EventSource` is the UIControl or NSNotification which fired the event and `Action` is a past-tense verb described what happened.

#### Example:

```swift
// bad: unclear what was the event source
// An NSNotification handler (EventSource=KeyboardDidShowNotification, Action=NULL)
didShowKeyboardNotification()

// good: the event source is clearly part of the function name
// An NSNotification handler (EventSource=KeyboardDidShowNotification, Action=NULL)
handleKeyboardDidShowNotification()

// bad: unclear that this function is handling the notification
// A UIButton handler (EventSource=ConfirmButton, Action=Tapped)
confirmButtonWasTapped()

// good: the function clearly handles the notification
// A UIButton handler (EventSource=ConfirmButton, Action=Tapped)
handleConfirmButtonTapped()
```
### Variables and Properties

- Naming should be `lowerCamelCase`.
- Variable names should always be descriptive with the exception of counter/index variables e.g. `index` and `counter`.
- Include the name of the type if the naming is ambiguous; e.g. `let confirm: Button` is bad, but `let confirmButton: Button` is good.
- For booleans, use prefixes such as `is` and `has` make it clear that a variable is a boolean.
