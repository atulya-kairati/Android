  

- Declare the ListView in the XML file.
```xml
<ListView  
    android:id="@+id/list"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    app:layout_constraintBottom_toBottomOf="parent"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" />
```

- Create a `string-array` in `res/values/strings.xml`.  
```xml
<resources>  
    
    <string name="app_name">Android_4_Views_1_ListView</string>  
  
    <string-array name="alphabets">  
        <item>A</item>  
        <item>B</item>  
        <item>C</item>  
        <item>D</item>   
    </string-array>
    
</resources>
```

- Get the array from `strings.xml` in into java code using and inflate the `ListView`:  
```java  
  
public class MainActivity extends AppCompatActivity {  
  
    ListView list;    
    String[] alphabets;    
    ArrayAdapter<String> adapter; 
     
    @Override    
    protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);        
		setContentView(R.layout.activity_main);
		list = findViewById(R.id.list);  

		// Getting array  
	    alphabets = getResources().getStringArray(R.array.alphabets); 

		// Creating an adapter from array 
		adapter = new ArrayAdapter<String>(
						    this,
						    android.R.layout.simple_list_item_1, 
						    alphabets
						);  

	    list.setAdapter(adapter);  


	    list.setOnItemClickListener((parent, view, position, id) -> {            
		    
		    String text = parent.getItemAtPosition(position).toString();  
		    
		    Toast.makeText(getApplicationContext(), text, 
									    Toast.LENGTH_SHORT).show(); 
		});  
	}
}  
```