- Like an electric switch.

```xml
<ToggleButton  
    android:id="@+id/toggle"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:text="Hello World!"  
    android:textOff="RED"  
    android:textOn="GREEN"  
    app:layout_constraintBottom_toBottomOf="parent"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" />
```

- `android:textOff="Off Text"` & `android:textOn="On Text"` define the text corresponding to the state of the button.

```java
ToggleButton toggle;

toggle = findViewById(R.id.toggle);  
  
toggle.setOnCheckedChangeListener((buttonView, isChecked) -> {  
	if(isChecked){  
//                ON  
		layout.setBackgroundColor(Color.GREEN);  
	}  
	else {  
//                OFF  
		layout.setBackgroundColor(Color.RED);  
	}  
});
```