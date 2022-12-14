- Kotlin’s `sealed` classes are open for extension by other classes defined in the same file but closed—that is, `final` or not `open`—for any other classes.

```kotlin
sealed class Card(val suit: String)


class Ace(suit: String) : Card(suit)

class King(suit: String) : Card(suit) {
  override fun toString() = "King of $suit"
}

class Queen(suit: String) : Card(suit) {
  override fun toString() = "Queen of $suit"
}

class Jack(suit: String) : Card(suit) {
  override fun toString() = "Jack of $suit"
}

class Pip(suit: String, val number: Int) : Card(suit) {
  init {
    if (number < 2 || number > 10) {
      throw RuntimeException("Pip has to be between 2 and 10")
    }
  }
}
```


- The constructors of `sealed` classes aren’t marked `private`, but they’re considered `private`.
- Since the constructors of `sealed` classes are considered to be private, we can’t instantiate an object of these classes. 
- However, we can create objects of classes that inherit from `sealed` classes, assuming their constructors aren’t marked `private` explicitly.

```kotlin
fun process(card: Card) = when (card) {
  is Ace -> "${card.javaClass.name} of ${card.suit}"
  is King, is Queen, is Jack -> "$card"
  is Pip -> "${card.number} of ${card.suit}"
}

fun main() {
    println(process(Ace("Diamond")))    // Ace of Diamond
    println(process(Queen("Clubs")))    // Queen of Clubs
    println(process(Pip("Spades", 2)))   // 2 of Spades
    println(process(Pip("Hearts", 6)))  // 6 of Hearts
}
```