- Clickable obj with two states (on/off).

```xml
<CheckBox  
    android:id="@+id/male"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:text="Male" />
```


```java
CheckBox checkBox = findViewById(R.id.checkBox);
checkBox.isChecked(); // returns true if its checked
```