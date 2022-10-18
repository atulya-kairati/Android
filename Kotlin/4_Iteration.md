### Range Class

- Int range
```kotlin
val oneToFive: IntRange = 1..5
```

- Character range
```kotlin
val aToE: CharRange = 'a'..'e'
```

- String Range
```kotlin
val seekHelp: ClosedRange<String> = "hell".."help"
```

- In `arg1..arg2`, arg1 ≤ arg2 always.

- Methods can be called on Range class as well
```kotlin
println(seekHelp.contains("helm")) //true 
println(seekHelp.contains("helq")) //false
```



### Forward iteration

```kotlin
for (i in 1..5) { print("$i, ") } //1, 2, 3, 4, 5,
```
- This works for `IntRange` & `CharRange` but not `StringRange`.

```kotlin
for (word in "hell".."help") { print("＄word, ") } 

//ERROR //for-loop range must have an 'iterator()' method
```
The reason for the failure is whereas classes like `IntRange` and `CharRange` have an `iterator()` function/operator, their base class `ClosedRange<T>` doesn’t.

	The loop variable is immutable.



### Reverse Iteration

```kotlin
for (i in 5.downTo(1)) { print("$i, ") } //5, 4, 3, 2, 1,
```

Or (Even better)

```kotlin
for (i in 5 downTo 1) { print("＄i, ") } //5, 4, 3, 2, 1,
```
***

#### `until`
- `until` is similar to `..` but it will exclude the end value.
```kotlin
for (i in 1 until 5) { print("＄i, ") } //1, 2, 3, 4,
```


#### `step`

```kotlin
for (i in 1..10 step 3) { print("$i, ") } // 1, 4, 7, 10
```

```kotlin
for (i in 1 until 10 step 3) { print("$i, ") } // 1, 4, 7 
```

```kotlin
for (i in 10 downTo 0 step 3) { print("＄i, ") } //10, 7, 4, 1,
```

#### `filter`

```kotlin
for (i in (1..9).filter { it % 3 == 0 || it % 5 == 0 }) { 

	print("$i, ") //3, 5, 6, 9, 
	
}
```

---

## Iterating over Arrays and Lists

- Iterating over an array.
```kotlin
val array = arrayOf(1, 2, 3)

for (e in array) { print("＄e, ") } //1, 2, 3,
```

- Iterating over list.
```kotlin
val list = listOf(1, 2, 3)

for (e in list) { print("$e, ") } //1, 2, 3,
```

- Iterating over indices.
```kotlin
val names = listOf("Tom", "Jerry", "Spike")
  

for (index in names.indices) {

  println("Position of ${names.get(index)} is $index")

}

/* OUTPUT
Position of Tom is 0 
Position of Jerry is 1 
Position of Spike is 2
*/
```

It can also be written utilizing destructuring:
```kotlin
for ((index, name) in names.withIndex()) {   

	println("Position of ＄name is ＄index")
	
}
```