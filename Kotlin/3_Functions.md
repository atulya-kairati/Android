- KISS (Keep it simple, stupid) functions.
```kotlin
fun greet() = "Hello" 
println(greet())
```
- If the function body contains a single expression, then it can be converted in a KISS function.
- `return` keyword is not allowed here.
- Return type is inferred.

- We can also specify return type
```kotlin
fun greet(): String = "Hello" 
```


- All functions are expressions.
- `void` in Java ⇾ `Unit` in Kotlin.
- All functions return something "void" functions return `Unit`

#### Function Parameters

```kotlin
fun greet(name: String): String = "Hello $name" 

println(greet("Eve")) //Hello Eve
```

- Parameters are `val` implicitly and can't be declared otherwise.
- Kotlin will give compile time error if the value of the parameter is being changed in side the function. 

- Default Parameters
```kotlin
fun greet(name: String, msg: String = "Hello"): String = "$msg $name" 

println(greet("Eve")) //Hello Eve 

println(greet("Eve", "Howdy")) //Howdy Eve
```

-  You may compute the default arguments for a parameter using the parameters to its left.
```kotlin
fun greet(name: String, msg: String = "Hi ${name.length}") = "$msg $name" 

println(greet("Scott", "Howdy")) //Howdy Scott 

println(greet("Scott")) //Hi 5 Scott
```

- Named Arguments

```kotlin
fun createPerson(name: String, age: Int = 1, height: Int, weight: Int) {    
	println("＄name ＄age ＄height ＄weight")
}

createPerson(name = "Jake", age = 12, weight = 43, height = 152)

```

- `varargs`
```kotlin
fun max(vararg numbers: Int): Int { 

	// numbers is an Int array here

	var large = Int.MIN_VALUE 
	
	for (number in numbers) { 
		large = if (number > large) number else large 
	} 
	
	return large 
}

max(23, 56, 34, 865, 343) // 865
```

```kotlin
fun greetMany(msg: String, vararg names: String) { 
	println("$msg ${names.joinToString(", ")}")
} 

greetMany("Hello", "Tom", "Jerry", "Spike") //Hello Tom, Jerry, Spike
```


- Spread Operator `*`

```kotlin
val arr = intArrayOf(1, 21, 3)
```

- If we need to pass the values in `arr` as individual parameters, we can use the spread operator `*`.
```kotlin
println(max(*values))
```

##### Destructuring

```kotlin
fun getFullName() = Triple("John", "Quincy", "Adams")
```

- If a function is returning either a `Pair` or `Triple`, it can be destructured into different variables.
	- Pair and Triple are data classes.

```kotlin
val (first, middle, last) = getFullName() 

println("$first $middle $last") //John Quincy Adams
```

- Values can be skipped is needed
```kotlin
val (first, _, last) = getFullName()

val (_, _, last) = getFullName()

val (_, middle) = getFullName()
```

