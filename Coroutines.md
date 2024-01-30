# Kotlin Coroutines
> In Kotlin, coroutines are a powerful feature for handling asynchronous programming, allowing you to write asynchronous code in a more sequential and readable manner. The coroutine library in Kotlin provides constructs to work with coroutines. Here, I'll provide an overview of the coroutine library along with syntax and examples.

### Coroutine Basics:

1. **Coroutines Scope:**
   The `CoroutineScope` is a context where you can launch coroutines. It manages the lifecycle of coroutines and cancels them when the scope is canceled.

   ```kotlin
   import kotlinx.coroutines.*

   fun main() {
       runBlocking {
           // create a CoroutineScope
           val myScope = CoroutineScope(Dispatchers.Default)
           // launch coroutine within the scope
           myScope.launch {
               delay(1000)
               println("Coroutine completed")
           }
       }
   }
   ```

2. **Launch:**
   The `launch` function is used to start a coroutine that doesn't return a result.

   ```kotlin
   import kotlinx.coroutines.*

   fun main() {
       runBlocking {
           launch {
               delay(1000)
               println("Coroutine completed")
           }
           println("Main function completed")
       }
   }
   ```

3. **Async and Await:**
   The `async` function is used to start a coroutine that computes a result, and `await` is used to get the result. 

   ```kotlin
   import kotlinx.coroutines.*

   suspend fun getResult(): String {
       delay(1000)
       return "Result from async function"
   }

   fun main() {
       runBlocking {
           val deferredResult = async {
               getResult()
           }
           println("Do some other work")
           val result = deferredResult.await()
           println("Result: $result")
       }
   }
   ```

4. **Coroutine Builders:**
   Coroutine builders like `launch`, `async`, and others help in creating coroutines.

   ```kotlin
   import kotlinx.coroutines.*

   fun main() {
       runBlocking {
           // using launch coroutine builder
           launch {
               println("Launching coroutine")
           }
           // using async coroutine builder
           val result = async {
               delay(1000)
               "Async result"
           }
           println(result.await())
       }
   }
   ```

5. **Structured Concurrency:**
   Structured concurrency ensures that all child coroutines are completed before the parent coroutine completes.

   ```kotlin
   import kotlinx.coroutines.*

   fun main() {
       runBlocking {
           // Structured concurrency
           coroutineScope {
               launch {
                   delay(1000)
                   println("Child coroutine completed")
               }
               println("Parent coroutine completed")
           }
       }
   }
   ```

6. **Cancellation:**
   Coroutines can be canceled explicitly using `coroutineContext.cancel()`.

   ```kotlin
   import kotlinx.coroutines.*

   fun main() {
       runBlocking {
           val job = launch {
               try {
                   repeat(1000) {
                       println("Job is running $it")
                       delay(500)
                   }
               } finally {
                   println("Job is finally completed")
               }
           }

           delay(2500)
           job.cancel()
           job.join()
       }
   }
   ```
   
These are just some basics of Kotlin coroutines. The coroutine library provides more advanced features and tools for handling concurrency and asynchronous tasks in a clean and efficient way. Keep in mind that this information is based on the state of Kotlin and its coroutine library as of my last update in January 2022, and there might be updates or changes after that.

### Parallel Decomposition: 
> Parallel decomposition involves taking a problem and breaking it into smaller subtasks that can be solved in parallel. When the results of the subtasks are ready, you can combine them into a final result.
- Consider the below example program where we use the `async()` and `await()` to achieve the parallel decomposition
```kotlin
import kotlinx.coroutines.*

fun main() {
    runBlocking {
        println("Weather Report")
        println(getWeatherReport())
        println("Have a good day!")
    }
}

suspend fun getWeatherReport() = coroutineScope {
    val forecast = async { getForecast() }
    val temperature = async { getTemperature() }
    "${forecast.await()} ${temperature.await()}"
}

suspend fun getForecast(): String {
    delay(1000)
    return "Sunny"
}

suspend fun getTemperature(): String {
    delay(1000)
    return "30\u00b0C"
}
```
### Cancellation of coroutines:
> A similar topic to exceptions is cancellation of coroutines. This scenario is typically user-driven when an event has caused the app to cancel work that it had previously started.
- Consider above example and observe the `getWeatherReport()` below
```kotlin
import kotlinx.coroutines.*

fun main() {
    runBlocking {
        println("Weather forecast")
        println(getWeatherReport())
        println("Have a good day!")
    }
}

suspend fun getWeatherReport() = coroutineScope {
    val forecast = async { getForecast() }
    val temperature = async { getTemperature() }

    delay(200)
    temperature.cancel() //This is known as the cancelation of coroutine

    "${forecast.await()}"
}

suspend fun getForecast(): String {
    delay(1000)
    return "Sunny"
}

suspend fun getTemperature(): String {
    delay(1000)
    return "30\u00b0C"
}
```

### Access the Kotlin Playground from here : 
[`Kotlin Playground`](https://developer.android.com/training/kotlinplayground)
