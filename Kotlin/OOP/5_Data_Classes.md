- Data classes are useful to represent data more than behavior.
- The _data classes_ of Kotlin are specialized classes that are intended to carry mostly data rather than behavior.
-  The primary constructor is required to define at least one property, using either `val` or `var`.
- For each data class, Kotlin will automatically create the `equals()`, `copy()`, `hashCode()`, and `toString()` methods.
- It also creates special methods that start with the word `component` (e.g. `component1()`, `component2()`) and so on, to access each property defined through the primary constructor.
- You may add other properties or methods to the class, within the body `{}`, if you desire.

```kotlin
data class Task(val id: Int, val name: String, val completed: Boolean)
```

```kotlin
data class Task(val id: Int, val name: String, val completed: Boolean){
	var assigned = false
}
```
- Any property defined within the class body `{}`, if present, will not be used in the generated `equals()`, `hashCode()`, and `toString()` methods. Also, no `componentN()` method will be generated for those.

```kotlin
val task1 = Task(1, "Create Project", false)

println(task1)
//Task(id=1, name=Create Project, completed=false)

println("Name: ${task1.name}") //Name: Create Project
```

- For data classes, Kotlin generates a `copy()` method that creates a new object with all the properties of the receiver object copied into the result object. Unlike the `equals()`, `hashCode()`, and the `toString()` methods, the `copy()` method includes any property defined within the class, not just those presented in the primary constructor.
```kotlin
val task1Completed = task1.copy(completed = true, assigned = true)
println(task1Completed)  
//Task(id=1, name=Create Project, completed=true)
```

>The `copy()` function only performs a shallow copy of primitives and references. The objects referenced internally are not deep copied by the method.


##### Destructuring a data class
```kotlin
val (id, _, isCompleted) = task1println("Id: ＄id Assigned: ＄isAssigned")
```


