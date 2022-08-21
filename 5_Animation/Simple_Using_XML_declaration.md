- Create a `Android Resource Directory` in `res` folder.  
- Select the type as `anim`.  
- Create a new `Animation Resource File` in `anim` DIR (here `image_anim.xml`).  
- For example, the following is needed to rotate a view by 360 deg, in 3000ms, pivoted at center.  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<set xmlns:android="http://schemas.android.com/apk/res/android">  
    <rotate        
	    android:duration = "3000"        
	    android:pivotX="50%"  
        android:pivotY="50%"       
        android:fromDegrees="0"        
        android:toDegrees="360"/>
</set>  
```

- Now define a view, normally in XML file
```xml
<ImageView  
    android:id="@+id/image"  
    android:layout_width="300dp"  
    android:layout_height="300dp"  
    android:layout_marginTop="100dp"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintHorizontal_bias="0.5"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent"  
    app:srcCompat="@drawable/numbers" />
```

- Then assign the defined animation to the view using Java.
```java
ImageView image = findViewById(R.id.image);

Animation imageAnim = AnimationUtils.loadAnimation(this, R.anim.image_anim);

image.setAnimation(imageAnim);
```