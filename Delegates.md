# Delegates

In general, follow the delegation section in the [official guidelines](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html).

## Convention

Implementing delegate methods should be optional.

## Rationale
Delegates augment existing behavior in the delegating object, they don't provide it directly. The delegating object must be fully self-sufficient, even if there is no delegate to augment its default behavior. It follows that if the delegate itself is not a required property on the delegating object that none of the methods on the delegate should be required. The delegate can implement as many or as few delegate callbacks as it cares about based on the context of that individual delegate.

## Implementation
### Default Implementations (preferred)
Provide an extension with default implementations after the protocol definition. This is preferred because the conforming types don't have to be Objective-C compatible.

#### Example
``` Swift

protocol DiceGameDelegate {

    func gameShouldStart(_ game: DiceGame)

    func game(_ game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int)

    func gameDidEnd(_ game: DiceGame)
}

extension DiceGameDelegate {

    func gameShouldStart(_ game: DiceGame) -> Bool {
        return false
    }

    func game(_ game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int) {}

    func gameDidEnd(_ game: DiceGame) {}
}

```

### Optional methods
Define all the methods as optional. This can only be done if the protocol is available from Objective-C (has the `@objc` attribute). All conforming types will need to be Objective-C compatible.

#### Example
``` Swift
@objc protocol DiceGameDelegate {

    @objc optional func gameShouldStart(_ game: DiceGame)

    @objc optional func game(_ game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int)

    @objc optional func gameDidEnd(_ game: DiceGame)
}

```
