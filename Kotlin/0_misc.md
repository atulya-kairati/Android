#### String template
```kotlin
val name = "Manus Chaubey"

print("My name is ${name}")  // My name is Manus Chaubey
```

- Whole expression (even multiline exp) can be written in the template.


 
#### Raw and Multiline String
- Triple `"` can be used to create a raw or multiline comment.

```kotlin
val escaped = "The kid asked, \"How's it going, ＄name?\""
```

```kotlin
val raw = """The kid asked, "How's it going, ＄name?""""
```

```kotlin
val name = "Eve" val memo = """Dear $name, a quick reminder about the party we have scheduled next Tuesday at the 'Low Ceremony Cafe' at Noon. | Please plan to...""" println(memo)
```


- `if else` blocks can be used as expressions.
```kotlin
val status = if (age > 17) "yes, please vote" else "nope, please come back" 
```

