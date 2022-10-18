- It's like a dropdown menu.

- We create the spinner in XML and add items from Java side.
```xml
<Spinner  
    android:id="@+id/genders"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content"  
    android:layout_weight="1" />
```

- Create a `string-array` in `res/values/strings.xml`:  
```xml    
<resources>  
    <string name="app_name">Android_1_Components_9_Spinner</string>    
    <string-array name="gender">        
	    <item>Male</item>        
	    <item>Female</item>        
	    <item>Geh</item>    
    </string-array>
</resources>  
```  
  
- To fill up the spinner with the given values, we need to create an adapter in the java code and pass it to the spinner.  
- Data source (cursor, ArrayList) <--> Adapter <--> Adapter View (ListView, Spinner, GridView).

#### Filling the spinner with values 
- Get the spinner
```java
Spinner gendaSpinner;
gendaSpinner = findViewById(R.id.genders);
```

- Creating an `Adapter` and passing it to `Spinner`
```java
// Creating an Adapter  
adapter = ArrayAdapter.createFromResource(this, R.array.gender, android.R.layout.simple_spinner_dropdown_item);  
  
// specifying dropdown layout  
adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);  
  
// passing the adapter to the spinner  
gendaSpinner.setAdapter(adapter);
```

- Define `setOnItemSelectedListener`

```java
gendaSpinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {  
    @Override  
    public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {  
        String gender = parent.getItemAtPosition(position).toString();  
        if(gender.equals("Geh")){  
            display.setText("Why are you geh?");  
            imageView.setImageResource(R.drawable.mista);  
            return;        }  
  
        display.setText(gender);  
        imageView.setImageResource(R.drawable.img);  
    }  
  
    @Override  
    public void onNothingSelected(AdapterView<?> parent) {  
  
    }  
});
```

- With String array

```java
public class MainActivity extends AppCompatActivity {  
  
    TextView display;  
    Spinner gendaSpinner;  
//    ArrayAdapter adapter;  
    ArrayAdapter<String> adapter;  
    ImageView imageView;  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
  
        display = findViewById(R.id.display);  
        gendaSpinner = findViewById(R.id.genders);  
        imageView = findViewById(R.id.imageView);  
  
        // Creating an Adapter  
//        adapter = ArrayAdapter.createFromResource(this, R.array.gender, android.R.layout.simple_spinner_dropdown_item);  
        String[] gender = {"Male", "Female", "Geh"};  
        adapter = new ArrayAdapter<>(this,
	        android.R.layout.simple_spinner_dropdown_item, 
	        gender);  
  


// passing the adapter to the spinner        
		gendaSpinner.setAdapter(adapter);  
  
  
        gendaSpinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {  
            @Override  
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {  
                String gender = parent.getItemAtPosition(position).toString();  
                if(gender.equals("Geh")){  
                    display.setText("Why are you geh?");  
                    imageView.setImageResource(R.drawable.mista);  
                    return;                }  
  
                display.setText(gender);  
                imageView.setImageResource(R.drawable.img);  
            }  
  
            @Override  
            public void onNothingSelected(AdapterView<?> parent) {  
  
            }  
        });  
  
    }  
}
```