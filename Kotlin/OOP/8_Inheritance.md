- Classes in Kotlin are `final` by default—that is, you can’t inherit from them. Only classes marked `open` may be inherited from. 
- Only open methods of an open class may be overridden in a derived class and have to be marked with `override` in the derived. 
- A method that isn’t marked `open` or `override` can’t be overridden. 
- An overriding method may be marked `final override` to prevent a subclass from further overriding that method.

- You may override a property, either defined within a class or within the parameter list of a constructor. A `val` property in the base may be overridden with a `val` or `var` in the derived. But a `var` property in the base may be overridden only using `var` in the derived. The reason for this restriction is that `val` only has a getter, and you may add a setter in the derived by overriding with `var`. But you shouldn’t attempt to withdraw the setter that’s for a base’s `var` by overriding with a `val` in the derived.

### Creating a base class

```kotlin
open class Vehicle(val year: Int, open var color: String) { // can be Inherited

  open val km = 0  // can be overriden

  final override fun toString() 
	  = "year: $year, Color: $color, KM: $km" //can't be overriden

  fun repaint(newColor: String) { //can't be overriden
    color = newColor
  }
}
```
Here:
- `Vehicle` class can be Inherited
- `year`: can't be overridden 
- `color`: can be overridden
- `km`: can be overridden
- `toString()`: can't be overridden
- `repaint()`: can't be overridden

```kotlin
open class Car(year: Int, color: String) : Vehicle(year, color) { // can be Inherited

  override var km: Int = 0  // can be overriden further
    set(value) {
      if (value < 1) {
        throw RuntimeException("can't set negative value")
      }
      field = value
    }

  fun drive(distance: Int) { // can't be overriden
    km += distance
  }  
}
```
Here:
- `Car` class can be Inherited
- `km`: can be overridden 
- `drive`: can't be overridden

>Unlike Java, Kotlin doesn’t distinguish between `implements` and `extends`—it’s just inheritance.



## Further extending the `Car` class

```kotlin
class FamilyCar(year: Int, color: String) : Car(year, color) {

  override var color: String
    get() = super.color
    set(value) {
      if (value.isEmpty()) {
        throw RuntimeException("Color required")
      }

      super.color = value
    }
}


val familyCar = FamilyCar(2019, "Green")
println(familyCar.color) //Green

try {
  familyCar.repaint("")
} catch(ex: RuntimeException) {
  println(ex.message) // Color required
}
```

Unlike the `km` property in `Car`, which kept its value locally in its backing field, the `FamilyCar` doesn’t store the value of `color` locally. Instead, by overriding both getter and setter, it fetches and forwards the value in these methods, respectively, from the base class. Since `Car` doesn’t override `color`, the `FamilyCar` uses the `color` from `Vehicle`.

When `familyCar.repaint()` is called, it use the new setter created for the `FamilyCar` class to assign `color` a value.


