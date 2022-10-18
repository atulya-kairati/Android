### Anonymous objects with object expressions


#### Anonymous Object Expressions

```kotlin
val circle = object { //an expression
	val x = 10
	val y = 20
	val radius = 30
}

println("Circle x: ${circle.x} y: ${circle.y} radius: ${circle.radius}")
```

- Can be used to group variables when making an actual class might be overkill.

- Limitations of Anonymous objects
	- The internal type of anonymous objects can’t stand as return types to functions or methods.
    - The internal type of anonymous objects can’t be used as types of parameters to functions or methods.
    - If they’re stored as properties in classes, they’ll be considered `Any` type and none of their properties or methods will then be available for direct access.
    
> In short, the most rudimentary object expression is useful only to group a few local variables together.

- Anonymous classes can also extend to other interfaces or classes.
	- If the Anon implements an interface, then its type is the type same as that of the Interface.
	- If it extends a class, then the class will serve as the type.

