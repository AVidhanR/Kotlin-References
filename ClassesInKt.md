### Enum Classes :
An `enum` class is used to represent a fixed set of related constants. It's a way to define a type that consists of a limited number of distinct values.

**Syntax:**

```kotlin
enum class Color {
    RED, GREEN, BLUE
}
```

**Example:**

```kotlin
fun main() {
    val selectedColor = Color.RED
    when (selectedColor) {
        Color.RED -> println("You chose Red")
        Color.GREEN -> println("You chose Green")
        Color.BLUE -> println("You chose Blue")
    }
}
```

In this example, we define an `enum` class `Color` with three constant values. We can use `when` to perform different actions based on the selected color.

----

### Sealed Classes :
A `sealed` class is used to represent a restricted hierarchy of classes, where all subclasses are known. It's often used for modeling restricted states or types.

**Syntax:**

```kotlin
sealed class Result
data class Success(val data: String) : Result()
data class Error(val message: String) : Result()
```

**Example:**

```kotlin
fun processResult(result: Result) {
    when (result) {
        is Success -> println("Success: ${result.data}")
        is Error -> println("Error: ${result.message}")
    }
}

fun main() {
    val successResult = Success("Data received")
    val errorResult = Error("Connection error")
    
    processResult(successResult)
    processResult(errorResult)
}
```

In this example, we define a `sealed` class `Result` with two subclasses: `Success` and `Error`. The `processResult` function uses `when` to handle different result types.

-----

### Data Classes :
A `data` class is used to represent data and typically contains data, not behavior. It generates useful functions like `equals()`, `hashCode()`, `toString()`, and `copy()` automatically.

**Syntax:**

```kotlin
data class Person(val name: String, val age: Int)
```

**Example:**

```kotlin
fun main() {
    val person1 = Person("Alice", 30)
    val person2 = Person("Bob", 25)

    println("Person 1: $person1")
    println("Person 2: $person2")

    val updatedPerson = person1.copy(age = 31)
    println("Updated Person 1: $updatedPerson")
    
    if (person1 == person2) {
        println("Person 1 and Person 2 are the same.")
    } else {
        println("Person 1 and Person 2 are different.")
    }
}
```

In this example, we define a `data` class `Person` with two properties. 
We can easily create, copy, and compare instances of `Person` thanks to the generated functions.

### KeyPoints:
- `enum` classes are for defining a limited set of constant values.
- `sealed` classes are used to represent a restricted hierarchy of related classes.
- `data` classes are designed for modeling data and come with automatically generated functions for easy data manipulation.
