# Immutability

## Convention

Immutability is an important concept in Swift; use constants over variables wherever possible.

## Rationale

The Swift compiler enforces that the constants will not be changed unexpectedly thus making the program safer.

## Examples

### if-statement

#### Good: the constant preserves immutability

```Swift
func spacing(for orientation: NSUserInterfaceLayoutOrientation) -> Int {
    let spacing = orientation = .horizontal ? 25 : 15
    return spacing
}
```

#### Bad: unnecessary use of variable does not preserve immutability

```Swift
func spacing(for orientation: NSUserInterfaceLayoutOrientation) -> Int {
    var spacing: Int
    if orientation = .horizontal {
        spacing = 25
    } else {
        spacing = 15
    }
    return spacing
}
```

### Switch Statement

#### Good: use a closure to calculate the value of the constant

```Swift
enum Direction {
	case north, south, east, west
}

func move(point: (Int, Int), towards direction: Direction) {
	let newPoint = { () -> (Int, Int) in
		switch direction {
		case .north:
			return (point.0, point.1 - 1)
		case .south:
			return (point.0, point.1 + 1)
		case .east:
			return (point.0 + 1, point.1)
		case .west:
			return (point.0 - 1, point.1 - 1)
		}
	}()

	if newPoint == (0,0) {
		print("Success!")
	}
}
```

#### Bad: unnecessary use of variable does not preserve immutability

```Swift
enum Direction {
	case north, south, east, west
}

func move(point: (Int, Int), towards direction: Direction) {
	var newPoint: (Int, Int)
	switch direction {
	case .north:
		newPoint = (point.0, point.1 - 1)
	case .south:
		newPoint = (point.0, point.1 + 1)
	case .east:
		newPoint = (point.0 + 1, point.1)
	case .west:
		newPoint = (point.0 - 1, point.1 - 1)
	}

	if newPoint == (0,0) {
		print("Success!")
	}
}
```
