- Declaration
```kotlin
enum class Suit { CLUBS, DIAMONDS, HEARTS, SPADES }
```

- Given a String, we can obtain the corresponding `enum` instance using the `valueOf()` method:
```kotlin
val diamonds = Suit.valueOf("DIAMONDS")
```

- Iterating over an enum
```kotlin
for (suit in Suit.values()) {
  println("${suit.name} -- ${suit.ordinal}") //CLUBS -- 0, etc.
}
```

- Further customizing an enum
```kotlin
enum class Suit(val symbol: Char) {

  CLUBS('♣️'),
  DIAMONDS('♦️'),
  HEARTS('❤️') {
    override fun display() = "${super.display()} $symbol"
  },
  SPADES('♠️'); // ; indicates end of values and the beginning of properties and methods of the `enum` class.

  open fun display() = "$symbol $name"
}
```