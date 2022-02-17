# Singletons

## Convention

If a singleton must be used (and effort should be taken to avoid this where possible), then they should always be implemented as a class with a shared reference to an instance of itself, with instance properties, rather than static properties.

## Rationale

Following this convention makes it clear that this class is a singleton and should be used that way. More importantly, it makes testing significantly simpler as new versions can be instatiated and passed around. 

## Examples

```swift
// good: The singleton has no static properties
class MyManager {
  static let shared = MyManager()
  var someVar: String = "Hello"
}

// bad: The singleton only has static properties
class MyManager {
  static var someVar: String = "Hello"
}

// A more complete example
public class OurDefaults {
  // Called throughout the application
  public static let shared = OurDefaults(userDefaults: .standard)

  private let userDefaults: UserDefaults

  // Called during test case set up
  // Initializer also makes it clear how many dependencies this class has.
  init(userDefaults: UserDefaults) {
    self.userDefaults = userDefaults
  }

}
```
