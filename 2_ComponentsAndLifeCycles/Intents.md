## What is Intent?
1. An Intent is an object which provides runtime binding between seprate components, such as two activities.
2. It represents the apps "intent" to do something.
3. It can be used to pass around data from one object to another.


## Using Intent two open other Activities

1. To open open `OtherActivity` from lets say `CurrentActivity`:
```java
Intent intent = new Intent(CurrentActivity.this, OtherActivity.class);
// to pass data
intent.putExtra("keyword", "Some data I want to pass to other activity");

startActivity(intent);
```

2. To get data in the `OtherActivity`:
```java
Intent intent = getIntent();

String data = intent.getStringExtra("keyword");

```