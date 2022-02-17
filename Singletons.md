# Singletons

If a singleton must be used, then they should always be implemented as a class with a shared reference to an instance of itself, with instance properties, rather than static properties. i.e.

```swift
// Good
class MyManager {
  static let shared = MyManager()
  var someVar: String = "Hello"
}

// Bad
class MyManager {
  static var someVar: String = "Hello"
}
```

This is enforced for 2 main reasons:

1. It makes it clear that this class is a singleton and should be used that way.
2. It allows easier testing (as new versions can be instantiated)


Here's an example:

```swift
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
