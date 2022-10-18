- Unlike in Java, Kotlin nested classes can’t access the private members of the nesting outer class. But if you mark the nested class with the `inner` keyword, then they turn into inner classes and the restriction goes away.

- Inner classes are defined using `inner` keyword inside a class to create a component for that specific class.
```kotlin
class TV {

  private var volume = 0
  
  val remote: Remote
    get() = TVRemote()

  override fun toString(): String = "Volume: ${volume}"
  
  inner class TVRemote : Remote {
  
    override fun up() { volume++ }
    override fun down() { volume-- }
    override fun toString() = "Remote: ${this@TV.toString()}"
    
  }                    
}


val tv = TV()
val remote = tv.remote

println("$tv") //Volume: 0

remote.up()
println("After increasing: $tv") //After increasing: Volume: 1

remote.doubleUp()
println("After doubleUp: $tv") //After doubleUp: Volume: 3
```


- If a property or method in the inner class shadows a corresponding member in the outer class, you can access the member of the outer class from within a method of the inner using a special `this` expression. You can see this in the `toString()` method of `TVRemote`, shown here again for convenience:
```kotlin
override fun toString() = "Remote: ＄{this@TV.toString()}"
```
Here, `this@TV` refers to the instance of the outer class `TV`.


- To get access to the methods or properties of base class of the Outer class use `super@Outer` syntax (here. Outer = TV).
```kotlin
override fun toString() = "Remote: ＄{super@TV.toString()}"
```
Accessing the `toString` method of `Any` which is base class of TV.



## Anonymous inner class

```kotlin

fun main() {
   val tv = TV()
   val r = tv.remote
   r.up()
   print(r)
}

interface Remote {
    fun up()
    fun down()
}

class TV {
    private var volume = 0
    val remote: Remote 
        get() = object: Remote { 
            override fun up() { volume++ } 
            override fun down() { volume-- }
            override fun toString() = "Remote: ${this@TV.toString()}" 
        }
    override fun toString(): String = "Volume: ${volume}" 
}
```

