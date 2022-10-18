- Similar to `static` in Java, **but not the same**.
- If a property or a method is needed at the class level and not on a specific instance of the class, we can’t drop them into the class. Instead, place them in a companion object.

```kotlin
class MachineOperator(val name: String) {

  fun checkin() = checkedIn++
  fun checkout() = checkedIn--

  companion object {
    var checkedIn = 0
    fun minimumBreak() = "15 minutes every 2 hours"
  }
}


MachineOperator("Mater").checkin() // method called using Instance 
println(MachineOperator.minimumBreak()) // method called Using class name
println(MachineOperator.checkedIn) //1
```

- The `companion object` can be accessed using `Companion` keyword.
```kotlin
val ref = MachineOperator.Companion
```

- We can also name the companion object
```kotlin
class MachineOperator(val name: String) {

  fun checkin() = checkedIn++
  fun checkout() = checkedIn--

  companion object MachineOperatorFactory{
    var checkedIn = 0
    fun minimumBreak() = "15 minutes every 2 hours"
  }
}


val MOF = MachineOperator.MachineOperatorFactory

```

- Whether you give an explicit name or not, the companion object can serve as a factory to create instances of the class they are part of.
- The constructors initialize an object to a valid state, but there are times when we may have to perform some extra steps before an object becomes available for use.
-  The companion object for the class, acting as a factory, can help with this design concern.
- To use a companion as a factory, provide a private constructor for the class. Then, provide one or more methods in the companion object that creates the instance and carries out the desired steps on the object before returning to the caller.
```kotlin
class MachineOperator private constructor(val name: String) {
    //...
    companion object {
        //...
        fun create(name: String): MachineOperator {
            val instance = MachineOperator(name)
            instance.checkin()
            return instance
        }
    }
}

val operator = MachineOperator.create("Mater")
println(MachineOperator.checkedIn) //1
```


> This not same as marking methods or attributes with `static` in Java.
> Use `@JvmStatic` for that. 

