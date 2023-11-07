# Kotlin In-Built Functions (Higher Order functions)

> In Kotlin, higher-order functions are functions that can take other functions as arguments or return functions as results. 
Lambdas are anonymous functions that can be used as arguments for higher-order functions. 
Here are some common higher-order functions in Kotlin, along with their syntax and examples:

## forEach()
This function is used to iterate over a collection and perform an action on each element.

Syntax:
```kotlin
collection.forEach { element ->
    // Code to perform an action on each element
}
```

Example:
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
numbers.forEach { println(it) }
```

## map()
It transforms each element of a collection and returns a new collection with the transformed values.

Syntax:
```kotlin
val transformedCollection = collection.map { element ->
    // Code to transform the element
}
```

Example:
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val squaredNumbers = numbers.map { it * it }
```

## filter()
It filters a collection based on a given condition and returns a new collection with the filtered elements.

Syntax:
```kotlin
val filteredCollection = collection.filter { element ->
    // Condition to filter the element
}
```

Example:
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val evenNumbers = numbers.filter { it % 2 == 0 }
```

## groupBy() 
It groups elements of a collection based on a key selector function and returns a map where keys are the results 
of the key selector function and values are lists of elements with the same key.

Syntax:
```kotlin
val groupedMap = collection.groupBy { element ->
    // Key selector function
}
```

Example:
```kotlin
data class Person(val name: String, val age: Int)

val people = listOf(Person("Alice", 25), Person("Bob", 30), Person("Charlie", 25))
val groupedByAge = people.groupBy { it.age }
```

## fold()
It accumulates the elements of a collection starting with an initial value and applying a given operation to each element.

Syntax:
```kotlin
val result = collection.fold(initialValue) { accumulator, element ->
    // Code to combine accumulator and element
}
```

Example:
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val sum = numbers.fold(0) { accumulator, number -> accumulator + number }
```

## sortedBy() 
It sorts a collection based on a specified key selector function.

Syntax:
```kotlin
val sortedCollection = collection.sortedBy { element ->
    // Key selector function
}
```

Example:
```kotlin
data class Person(val name: String, val age: Int)

val people = listOf(Person("Alice", 25), Person("Bob", 30), Person("Charlie", 20))
val sortedByName = people.sortedBy { it.name }
```
