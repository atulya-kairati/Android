- Usually used in group to take user choice.

```xml
<RadioGroup  
    android:id="@+id/group"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent">  
  
    <RadioButton        
	    android:id="@+id/red"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:text="Red" />  
  
    <RadioButton       
	    android:id="@+id/green"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:text="Green" />  
  
    <Button       
	    android:id="@+id/button"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:text="Change" />  
</RadioGroup>
```

- `RadioGroup` Is used to wrap all separate `RadioButton`s in to one.

```java
RadioButton red, green;  
Button button;

red = findViewById(R.id.red);  
green = findViewById(R.id.green);  
button = findViewById(R.id.change);  
  
button.setOnClickListener(v -> {  
  
    if(red.isChecked()){  
    layout.setBackgroundColor(Color.RED);  
    }  
    
    else if(green.isChecked()){  
        layout.setBackgroundColor(Color.GREEN);  
    }  
    
});
```
