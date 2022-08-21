- Used to display text on screen

```xml
<TextView  
    android:id="@+id/textex"  
    android:layout_width="wrap_content"  
    android:layout_height="100dp"  
    android:layout_margin="100dp"  
    android:background="@color/black"  
    android:gravity="bottom"  
    android:padding="24dp"  
    android:text="Heee Heeee"  
    android:textColor="@color/purple_200"  
    android:textSize="24sp"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" 
/>
```

- Can be customized from XML as well as Java

```java
TextView text;  
text = findViewById(R.id.textex);  
  
text.setAllCaps(true);  
  
text.setOnClickListener(v -> {  
    text.setTextColor(Color.BLUE);  
    text.setBackgroundColor(Color.DKGRAY);  
});
```