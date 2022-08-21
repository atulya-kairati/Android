- Place images in `res/drawable`

```xml
<ImageView  
    android:id="@+id/image"  
    android:layout_width="300dp"  
    android:layout_height="300dp"  
    android:layout_alignParentStart="true"  
    android:layout_alignParentTop="true"  
    android:layout_marginStart="54dp"  
    android:layout_marginTop="58dp"  
    android:contentDescription="Image"  
    android:scaleType="fitCenter"  
    app:srcCompat="@drawable/yify" />
```

```java
ImageView image;
image = findViewById(R.id.image);  
  
image.setOnClickListener(v -> image.setImageResource(R.drawable.me));
```