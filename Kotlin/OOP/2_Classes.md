
### Simplest Class
```kotlin
class Car
```


#### Class with Read only properties using Primary Constructors
```kotlin
class Car(val yearOfMake: Int)
```

- Since the attribute is declared as `val` it cal only be read, once the object has been created.

- For the above line, Kotlin compiler wrote a constructor, defined a field, and added a getter to retrieve the value of that field.

- `this` functions same as in Java.

- That line can be expanded as
```kotlin
public class Car public constructor(public val yearOfMake: Int)
```

By default, the access to the class and its members is public, and the constructor is public as well. 

In Kotlin, the line that defines the class is actually defining the primary constructor. The keyword `constructor` isn’t needed unless we want to change the access modifier or place an annotation for the primary constructor.
___

#### Creating instances
```kotlin
val car = Car(2019) 
println(car.yearOfMake) //2019
```

```kotlin
car.yearOfMake = 2019 //ERROR: val cannot be reassigned
```

___

#### Read-write properties

```kotlin
class Car(val yearOfMake: Int, var color: String)

val car = Car(2019, "Red")
car.color = "Green"
println(car.color) //Green
```

- The `car` object is itself immutable and so is its attribute `yearOfMake` but since the attribute `color` is marked a `var` it is *mutable* and hence **writable**.

- The above  `Car` class when decompiled to Java byte code 
```java

public final class Car {  
	private final int yearOfMake;  
	private java.lang.String color;  
	public final int getYearOfMake();  
	public final java.lang.String getColor();   
	public final void setColor(java.lang.String);   
	public Car(int, java.lang.String);
}
```

- When we call `car.color` we are not directly accessing the property but a getter or setter which Kotlin internally creates.

___

#### Controlling changes to properties

- Even though the Kotlin Compiler provides us with default getters and setters without us declaring it, we can create our own default getters and setters in Kotlin.

###### Setter
```kotlin
class Car(val yearOfMake: Int, theColor: String) {

  var fuelLevel = 100
  
  var color = theColor
    set(value) {
      if (value.isBlank()) {
        throw RuntimeException("no empty, please")
      }

      field = value
    }
}
```

Here:
- We created a property named `color` and assigned it to the value in the constructor parameter `theColor`. Both names can be the same, but it's recommended to keep them different to avoid confusion. 
- `set(value)` is the setter. 
- `value` is the parameter which receives the new value that is being assigned to the property (`color`).
- `field` inside the setter refers to the actual property and any changes done to `field` will reflect in the actual property (`color`).
- Kotlin Compiler creates getter and setter for `fuelLevel` but only creates getter for `color` and uses the setter provided by us.


The above class can be used is such ways:
```kotlin
val car = Car(2019, "Red")
car.color = "Green"
car.fuelLevel--  

println(car.fuelLevel) //99

try {
    car.color = ""
} catch(ex: Exception) {
    println(ex.message) //no empty, please
}

println(car.color) //Green
```


###### Getter

```kotlin
class Rectangle(val width: Int, val height: Int) {
// property type is optional since it can be inferred from the getter's return type
    val area: Int 
        get() = this.width * this.height
}
```

---

## Access modifiers

The properties and methods of a class are public by default in Kotlin. The possible access modifiers are: `public`, `private`, `protected`, and `internal`. The first two have the same meaning as in Java. The protected modifier gives permission to the methods of the derived class to access that property. The `internal` modifier gives permission for any code in the same module to access the property or method, where a module is defined as all source code files that are compiled together. The `internal` modifier doesn’t have a direct bytecode representation. It’s handled by the Kotlin compiler using some naming conventions without posing any runtime overhead.

- The access permission for the **getter** is the same as that for the property.
- The access permission for the **setter** can be declared as following,
```kotlin
var fuelLevel = 100   
	private set

var d = 2
	private set(c){
		field = c
	}
```
___

## Initialization code

- In case, primary constructor isn't enough to initialize the class, we can use `init` block.
- A class may have zero or more `init` blocks. 
- These blocks are executed as part of the primary constructor execution. The order of execution of the `init` blocks is top-down. 
- Within an `init` block, you may access only properties that are already defined above the block.
```kotlin
class Car(val yearOfMake: Int, theColor: String) {

  var fuelLevel = 100
    private set

  var color = theColor
    set(value) {
      if (value.isBlank()) {
        throw RuntimeException("no empty, please")
      }
  
      field = value
    }

  init {
    if (yearOfMake < 2020) { fuelLevel = 90 }
  }
}
```

> Write `init` blocks only when necessary

___
## Secondary constructors

If you don’t write a primary constructor, then Kotlin creates a no-argument default constructor. If your primary constructor has default arguments for all parameters, then Kotlin creates a no-argument constructor in addition to the primary constructor. In any case, you may create more constructors, called secondary constructors.

Your secondary constructors are required to either call the primary constructor or call one of the other secondary constructors. Also, secondary constructors’ parameters can’t be decorated with `val` or `var`; they don’t define any properties. Only the primary constructor and declarations within the class may define properties.

```kotlin
class Person(val first: String, val last: String) {

  var fulltime = true
  var location: String = "-"

  constructor(first: String, last: String, fte: Boolean): this(first, last) {
    fulltime = fte
  }

  constructor(
    first: String, last: String, loc: String): this(first, last, false) {
    location = loc
  }

  override fun toString() = "$first $last $fulltime $location"
  
}
```

Here:
- The first secondary constructor is using `this` to call the **primary constructor**.
- And the 2nd secondary constructor is using `this` to call the **first secondary constructor**.
- What constructor is called when invoking `this()` is determined by the parameters used.

> Any secondary constructor may call either the primary constructor or any of the other secondary constructors, as long as the call doesn’t fall into a cyclic chain that leads up to the constructor being defined.

Using the above defined class,
```kotlin
println(Person("Jane", "Doe"))         //Jane Doe true -
println(Person("John", "Doe", false))  //John Doe false -
println(Person("Baby", "Doe", "home")) //Baby Doe false home
```

___

## Defining instance methods

- Define methods in classes using the `fun` keyword.
- By default, methods are `public`, but you may mark them as `private`, `protected`, or `internal` before the `fun` keyword if you want to change the access permission.

```kotlin
class Person(val first: String, val last: String) {

  internal fun fullName() = "$last, $first"

  private fun yearsOfService(): Int = throw RuntimeException("Not implemented yet")
  
}

val jane = Person("Jane", "Doe")
println(jane.fullName()) //Doe, Jane
jane.yearsOfService() //ERROR: cannot access...private in 'Person'
```
___

## Inline Classes

- When using Inline Classes, you get the benefit of classes at compile time, but you get the benefits of using a primitive at runtime, the class is transformed into a primitive in the bytecode.
-  `inline` classes are expanded or replaced by their underlying member where they are used.

```kotlin
inline class SSN(val id: String)  

fun receiveSSN(ssn: SSN) {
  println("Received $ssn")
}

receiveSSN(SSN("111-11-1111"))
```


`inline` classes may have properties and methods and may implement interfaces as well. Under the hood, methods will be rewritten as `static` methods that receive the primitive types that are being wrapped by the `inline` class. inline classes are required to be `final` and aren’t allowed to extend from other classes.
