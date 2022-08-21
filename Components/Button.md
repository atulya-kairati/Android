- Similar to a push button.

#### Default
```xml
<Button  
    android:id="@+id/hider"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:layout_marginStart="160dp"  
    android:layout_marginTop="320dp"  
    android:text="Hide"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" />
```

#### To create a custom button  
- Create a file `res/drawable/custom_button.xml`.  
- Add the follow to create an oval button.  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<shape xmlns:android="http://schemas.android.com/apk/res/android"  
    android:shape="oval">    
    
    <solid android:color="@color/purple_200"></solid>
</shape>
```

- Set the shape of the button as the custom button.
```
android:background="@drawable/custom_button"
```
```xml
<Button  
    android:id="@+id/adder"  
    android:layout_width="wrap_content"  
    android:layout_height="80dp"  
    android:layout_marginStart="160dp"  
    android:layout_marginTop="204dp"  
    android:background="@drawable/custom_button"  
    android:text="+"  
    android:textSize="40sp"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" />
```