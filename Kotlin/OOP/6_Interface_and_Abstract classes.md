Being a statically typed language, Kotlin promotes design by contract, where interfaces serve as specifications and classes as implementors of those contracts. You can also reuse implementations, in addition to specifications, by creating abstract classes.

From the safety point of view, classes are `final` by default and you have to explicitly annotate them as `open` to serve as a base class. Further, Kotlin doesn’t work in a binary state of inheritable vs. non-inheritable. You can define classes as `sealed` and thus state which specific classes may extend from those.

## Creating interfaces

As in modern Java, we can declare abstract methods in Kotlin and even provide a default implementation but unlike in Java, we don't need to use `default` keyword.

Also, interfaces can also have `static` methods, but only via companion objects written within the interfaces.

An Interface in Kotlin,
```kotlin
interface Remote {
  fun up()
  fun down()

  fun doubleUp() {
    up()
    up()
  }
}
```

>**For JVM < 1.8**
>To make the Kotlin `default` methods visible as default methods in the bytecode, you can use the `@JvmDefault` annotation.

### Implementing an Interface
```kotlin
class TV {
  var volume = 0
}

class TVRemote(val tv: TV) : Remote {

  override fun up() { tv.volume++ }
  override fun down() { tv.volume-- }

}
```
Here, class `TVRemote` Implement `Remote` interface and provides implementation for the abstract methods.

```kotlin
val tv = TV()
val remote: Remote = TVRemote(tv)

println("Volume: ${tv.volume}") //Volume: 0

remote.up()
println("After increasing: ${tv.volume}") //After increasing: 1

remote.doubleUp()
println("After doubleUp: ${tv.volume}") //After doubleUp: 3
```


In Java, interfaces may have `static` methods too, but in Kotlin we can’t place `static` methods directly in interfaces, just like we can’t place them directly in classes. Use companion objects to create `static` methods in interfaces. 

For example, let’s create a `combine()` method that will bind two remotes so that the operations are performed on both remotes, one after the other:

```kotlin
interface Remote {
  fun up()
  fun down()

  fun doubleUp() {
    up()
    up()
  }

  companion object {
    fun combine(first: Remote, second: Remote): Remote = object: Remote {
        override fun up() {
          first.up()
          second.up()
        }            

        override fun down() {
          first.down()
          second.down()
        }
      }
  }
  
}
```

```kotlin
val tv = TV()
val remote: Remote = TVRemote(tv)

remote.up()
remote.doubleUp()

val anotherTV = TV()
val combinedRemote = Remote.combine(remote, TVRemote(anotherTV)) // "static"

combinedRemote.up()
println(tv.volume) //4
println(anotherTV.volume) //1
```

___

## Creating abstract classes

The classes have to be marked `abstract` to be considered abstract, and abstract methods have to be marked `abstract` in abstract classes.

```kotlin
abstract class Musician(val name: String, val activeFrom: Int) {
  abstract fun instrumentType(): String
}

class Pianist(name: String, activeFrom: Int) : Musician(name, activeFrom) {
  override fun instrumentType() = "Piano"
}

val b = Pianist("Bethoveen", 1800)

println(b.name)
```


The main differences between an abstract class and an interface are these:

- The properties defined within interfaces don’t have backing fields (`field` keyword); they have to rely on abstract methods to get properties from implementing classes. On the other hand, properties within abstract classes can use backing fields.  
- You may implement multiple interfaces but can extend from at most one class, abstract or not.
