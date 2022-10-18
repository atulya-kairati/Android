	expression returns something whereas statement does not. 

## `when` as an expression

- Can be used either as an expression or a statement. As shown below
```kotlin
fun whatToDo(dayOfWeek: Any) =  when (dayOfWeek) {  
    "Saturday", "Sunday" -> "Relax"  
    in listOf("Monday", "Tuesday", "Wednesday", "Thursday") -> "Work hard"  
    in 2..4 -> "Work hard"  
    "Friday" -> "Party"  
    is String -> "What?"  
    else -> "No clue"  
}  
  
println(whatToDo("Sunday")) //Relax  
println(whatToDo("Wednesday")) //Work hard  
println(whatToDo(3)) //Work hard  
println(whatToDo("Friday")) //Party  
println(whatToDo("Munday")) //What?  
println(whatToDo(8)) //No clue
```

## `when` as a statement

```kotlin
fun printWhatToDo(dayOfWeek: Any) {  
    when (dayOfWeek) {  
        "Saturday", "Sunday" -> println("Relax")  
        in listOf("Monday", "Tuesday", "Wednesday", "Thursday") ->  
            println("Work hard")  
        in 2..4 -> println("Work hard")  
        "Friday" -> println("Party")  
        is String -> println("What?")  
    }  
}  
  
printWhatToDo("Sunday") //Relax  
printWhatToDo("Wednesday") //Work hard  
printWhatToDo(3) //Work hard  
printWhatToDo("Friday") //Party  
printWhatToDo("Munday") //What?  
printWhatToDo(8) //
```

## `when` and variable scope

```kotlin
fun systemInfo(): String {  
    val numberOfCores = Runtime.getRuntime().availableProcessors()  
  
    return when (numberOfCores) {  
        1 -> "1 core, packing this one to the museum"  
        in 2..16 -> "You have $numberOfCores cores"        
        else -> "$numberOfCores cores!, I want your machine"    
    }  
}
```

In the above snippet, `numberOfCores` variable is only needed in the when expression and hence we should try and limit its scope to when, it can be rewritten as:

```kotlin
fun systemInfo(): String =
    when (val numberOfCores = Runtime.getRuntime().availableProcessors()) {  
        1 -> "1 core, packing this one to the museum"  
        in 2..16 -> "You have $numberOfCores cores"        
        else -> "$numberOfCores cores!, I want your machine"    
    }
```
Here, `numberOfCores` is with in the scope of when expression and ASA when expression has been evaluated, the `numberOfCores` variable is disposed.


---

- Checking multiple conditions
```kotlin
when(n) {    
	n != 17 && n != 42 -> doThis()  // checking multiple conditions  
	else -> doThis()
}
```
