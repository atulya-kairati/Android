- Create a grid view  
	- Define no of cols  
	- gravity and other properties  
```xml
<GridView  
    android:id="@+id/gridview"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    android:gravity="center"  
    android:numColumns="3"  
    app:layout_constraintBottom_toBottomOf="parent"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" />
```

- Create a layout file and create design for grid card  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:gravity="center"  
    android:orientation="vertical"  
    android:padding="8dp">  
  
    <ImageView        
	    android:id="@+id/cardimg"  
        android:layout_width="150dp"  
        android:layout_height="150dp"  
        android:layout_weight="1"  
        android:scaleType="centerCrop"  
        app:srcCompat="@drawable/fox" />  
  
    <TextView        
	    android:id="@+id/imgLable"  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:layout_weight="1"  
        android:text="TextView" />  
</LinearLayout>
```
  
- Create ArrayLists of the attributes that will be needed for each grid card and fill them.  
- 
- Create a GridAdapter class which extends BaseAdapter and then implement the inherited methods.  
- 
- Define Context object and the ArrayLists needed to fill each card and also a parameterized constructor  
- 
- `getCount` method returns the no of items to be created in the GridView.  
- `getView` method is where we create the grid card layput from by connecting it to the xml design file.  
  - We also connect to the internal components of the card grid and provide them with the data required to display.  
    
```java  
public class GridApadter extends BaseAdapter {  
  
    Context context;  
    List<String> animalNames;  
    List<Integer> animalPics;  
  
    public GridApadter(Context context, List<String> animalNames, List<Integer> animalPics) {  
        this.context = context;  
        this.animalNames = animalNames;  
        this.animalPics = animalPics;  
    }  
  
    @Override  
    public int getCount() {  
        return animalNames.size();  
    }  
  
    @Override  
    public Object getItem(int position) {  
        return null;  
    }  
  
    @Override  
    public long getItemId(int position) {  
        return 0;  
    }  
  
    @Override  
    public View getView(int position, View convertView, ViewGroup parent) {  
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.grid_card_design, parent, false);  
        ImageView cardImg = view.findViewById(R.id.cardimg);  
        cardImg.setImageResource(animalPics.get(position));  
        TextView imgLable = view.findViewById(R.id.imgLable);  
        imgLable.setText(animalNames.get(position));  
        return view;  
    }  
}
```  
  
- In the activity, create an instance of `GridApadter` and connect it to GridView.

```java
public class MainActivity extends AppCompatActivity {  
  
    GridView gridView;  
    List<String> animalNames = new ArrayList<>();  
    List<Integer> animalPics = new ArrayList<>();  
    GridAdapter gridAdapter;  
  
    public void fillLists(){  
        animalNames.add("Cat");  
        animalNames.add("Fox");  
        animalNames.add("Snake");  
        animalNames.add("Tiger");  
  
        animalPics.add(R.drawable.cat);  
        animalPics.add(R.drawable.fox);  
        animalPics.add(R.drawable.snake);  
        animalPics.add(R.drawable.tiger);  
    }  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
  
        fillLists();  
  
        gridView = findViewById(R.id.gridview);  
        gridAdapter = new GridAdapter(MainActivity.this, animalNames, animalPics);  
        gridView.setAdapter(gridAdapter);  
  
        gridView.setOnItemClickListener((parent, view, position, id) -> {  
            Toast.makeText(parent.getContext(), animalNames.get(position), Toast.LENGTH_SHORT).show();  
        });  
        }  
}
```

