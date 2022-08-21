  
  
- Set up the `RecyclerView` in the activity.  
- Then, by right-clicking on `res/layout` folder, create a `Layout Resource File`.  
- Specify the custom design for the RecyclerView in the made file.   
	- The root of the Card view should be Constraint layout during the time of creation.  
	- The ConstraintLayout should have height was wrap content.  
	- Refer `res/layout/card_design.xml` to refer the card design for the RecyclerView.  

- Add gradle dependency for Circular ImageView in `app/build.gradle`
```groovy  
implementation 'de.hdodenhof:circleimageview:3.1.0'  
```  


- In `card_design.xml`, the TextViews are chained Vertically.  
  - Ctrl + click on both text views to select.  
  - Right click, Chain ⇾ Chain Vertically.  
  - This arranges them at equal distance in the card vertically.  
```xml
%% card_design.xml %%
<?xml version="1.0" encoding="utf-8"?>  
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content">  
  
    <androidx.cardview.widget.CardView        android:id="@+id/cardView"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_margin="8dp"  
        android:backgroundTint="@color/purple_200"  
        app:cardCornerRadius="8dp"  
        app:cardElevation="4dp"  
        app:layout_constraintBottom_toBottomOf="parent"  
        app:layout_constraintEnd_toEndOf="parent"  
        app:layout_constraintStart_toStartOf="parent"  
        app:layout_constraintTop_toTopOf="parent">  
  
        <androidx.constraintlayout.widget.ConstraintLayout 
		    android:layout_width="match_parent"  
            android:layout_height="80dp">  
  
            <de.hdodenhof.circleimageview.CircleImageView                
	            android:id="@+id/circularImage"  
                android:layout_width="70dp"  
                android:layout_height="70dp"  
                android:layout_marginStart="8dp"  
                android:src="@drawable/polar_bear"  
                app:civ_border_color="#FF000000"  
                app:civ_border_width="2dp"  
                app:layout_constraintBottom_toBottomOf="parent"  
                app:layout_constraintStart_toStartOf="parent"  
                app:layout_constraintTop_toTopOf="parent" />  
  
            <TextView                android:id="@+id/textViewName"  
                android:layout_width="wrap_content"  
                android:layout_height="wrap_content"  
                android:layout_marginStart="24dp"  
                android:text="TextView"  
                android:textSize="20sp"  
                app:layout_constraintBottom_toTopOf="@+id/textViewDetail"  
                app:layout_constraintStart_toEndOf="@+id/circularImage"  
                app:layout_constraintTop_toTopOf="parent" />  
  
            <TextView                android:id="@+id/textViewDetail"  
                android:layout_width="wrap_content"  
                android:layout_height="wrap_content"  
                android:layout_marginStart="24dp"  
                android:text="TextView"  
                android:textSize="14sp"  
                app:layout_constraintBottom_toBottomOf="parent"  
                app:layout_constraintStart_toEndOf="@+id/circularImage"  
                app:layout_constraintTop_toBottomOf="@+id/textViewName" />  
  
		</androidx.constraintlayout.widget.ConstraintLayout>   
	</androidx.cardview.widget.CardView></androidx.constraintlayout.widget.ConstraintLayout>
```
  
- To assign the `card_design` to `RecyclerView`, In recycler view mention in activity_main.xml.  
```xml
tools:listitem="@layout/card_design" /> 
```  

```xml
<androidx.recyclerview.widget.RecyclerView  
    android:id="@+id/recyclerView"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    app:layout_constraintBottom_toBottomOf="parent"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent"  
    tools:listitem="@layout/card_design" />
```

#### Create a custom Adapter for the RecyclerView.  
- Create a java class  
- Add all the List variables needed. And also add an object of `Context` class to use the properties of the Activity in this class  
```java  
public class RecyclerViewAdapter {  
  
	private List<String> nameList;  
	private List<String> detailList;  
	private List<Integer> imgIdList;  
	private Context context;  
  
	public RecyclerViewAdapter(List<String> nameList, List<String> detailList, List<Integer> imgIdList, Context context) {    
		this.nameList = nameList;    
		this.detailList = detailList;    
		this.imgIdList = imgIdList;   
		this.context = context;  
	}
}  
```  
- Add a constructor with all the mentioned objects.  
  
- Now, we will create an inner class in this `RecyclerViewAdapter` class to represent the card design.  
- The inner class will extend `RecyclerView.ViewHolder`.  
  - Create a constructor matching super (Alt + Enter).  
- Define Views and Components that are part of the `card_design` in the inner class such as `TextView` and `ImageView`.  
- Match the components to their IDs in the constructor using `itemView`  
```java  
public class RecyclerViewAdapter {  
  
	//  private List<String> nameList;  
	//  private Lis....  
	//          Not important here (Refer original code)  
	//          ....context;  
	//  }  
	  
	public class AnimalViewHolder extends RecyclerView.ViewHolder {  
	
		TextView nameTextView, 
		DetailTextView;    
		ImageView circularImage;
		
		public AnimalViewHolder(@NonNull View itemView) {      
			super(itemView);      
			// Connecting to their ids, here itemView represents the 
			// card design we defined, so we can refer to its component
			
			nameTextView = itemView.findViewById(R.id.textViewName);      
			detailTextView = itemView.findViewById(R.id.textViewDetail);      
			circularImage = itemView.findViewById(R.id.circularImage);    
		}  
	}
}  
```  
  
- Now extend the outer class `RecyclerViewAdapter` to `RecyclerView.Adapter<T>`  
  - `T` is OuterClass.InnerClass, here it is `RecyclerViewAdapter.AnimalViewHolder`.  
  - Now implement the required methods (Alt + Enter).  
```java  
public class RecyclerViewAdapter extends RecyclerView.Adapter<RecyclerViewAdapter.AnimalViewHolder>{  
	
//    private List<String> nameList;  
//    private Lis....  
//  Not important here (Refer original code)  
//          ....IdList;  
//        this.context = context;  
//    }  
	
	@NonNull    
	@Override    
	public AnimalViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {        
		return null;    
	}  
	
	@Override    
	public void onBindViewHolder(@NonNull AnimalViewHolder holder, int position) {  
	
	}
	  
	@Override    
	public int getItemCount() {        
		return 0;    
	}  
//    public class AnimalViewHolder extends RecyclerView.ViewHolder {  
//  
//        TextView nameT....  
//      Not important here (Refer original code)  
//          ....ndViewById(R.id.textViewDetail);  
//            circularImage = itemView.findViewById(R.id.circularImage);  
//        }  
//    }  
}  
  
```  
  
- Complete the implemented methods (Read the comments in code).  
```java  
public class RecyclerViewAdapter extends RecyclerView.Adapter<RecyclerViewAdapter.AnimalViewHolder>{  
  
//    private List<String> nameList;  
//    private Lis....  
//  Not important here (Refer original code)  
//          ....IdList;  
//        this.context = context;  
//    }  

	@NonNull  
	@Override 
	public AnimalViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType){  
		// here:    
		// parent -> refers to the activity in which the RecyclerView resides, 
		// here it resides in MainActivity  
		// In This method we define the card design that we made    
		// It is called as soon as AnimalViewHolder is instantiated    
		// Create a view then transfer the card design into that    
		View view = LayoutInflater.from(parent.getContext())
								  .inflate(
										R.layout.card_design, 
										parent, 
										false
									);  
		// Returning AnimalViewHolder with card design view in it    
		return new AnimalViewHolder(view);  
	}  
	
	@Override  
	public void onBindViewHolder(@NonNull AnimalViewHolder holder, int position) {
		// It is called when design is created and connected to the recycler view.  
		
		// It recieves AnimalViewHolder holder that was created 
		// in onCreateViewHolder and got attached to RecyclerView  
		
		// Here we transfer the data in the components in the array 
		// into the respective components  
	
		holder.nameTextView.setText(nameList.get(position)); 
		holder.detailTextView.setText(detailList.get(position));    
		holder.circularImage.setImageResource(imgIdList.get(position));  
	}  
	
	@Override  
	public int getItemCount() {
		// Specifies the amount of data to be displayed in the RecyclerView  
		return nameList.size();  
	}  


//    public class AnimalViewHolder extends RecyclerView.ViewHolder {  
//  
//        TextView nameT....  
//      Not important here (Refer original code)  
//          ....ndViewById(R.id.textViewDetail);  
//            circularImage = itemView.findViewById(R.id.circularImage);  
//        }  
//    }  
}  
```  

- Define RecyclerView object in the "main" activity.
- Now, create an object of Custom Adapter class we defined (RecyclerViewAdapter) in the activity where the RecyclerView is specified and pass all the parameters.  
- Set the RecyclerViewAdapter object to the RecyclerView object.  
```java  
@Override  
protected void onCreate(Bundle savedInstanceState) {  
	super.onCreate(savedInstanceState);  
	setContentView(R.layout.activity_main);  

	recyclerView = findViewById(R.id.recyclerView);  

	// to specify how the RecyclerView would be arranged  
	recyclerView.setLayoutManager(new LinearLayoutManager(MainActivity.this));  

	// Create nameList, detailList, imgIdList prior to this
	// The order of the list should correspond
	nameList.add("Bengal Tiger");  
	nameList.add("Polar Bear");  

	detailList.add("Found in the tropical regions of Indian Subcontinent.");  
	detailList.add("Found in the ice caps of the Arctic.");  

	imgIdList.add(R.drawable.bengal_tiger) ;  
	imgIdList.add(R.drawable.polar_bear);  

	// Creating the RecyclerViewAdapter object and passing all the params required.  
	recyclerViewAdapter = new RecyclerViewAdapter(nameList, detailList, imgIdList, MainActivity.this);  
	recyclerView.setAdapter(recyclerViewAdapter);  

}  

```  
  
#### To make all the card views in the RecyclerView Clickable:  
- Add a `CardView` attribute in the inner class of `RecyclerViewAdapter`.  
- And attach it to the corresponding component.  
```java  
public class RecyclerViewAdapter extends RecyclerView.Adapter<RecyclerViewAdapter.AnimalViewHolder> {  
//    .....  
//  ......  

	public class AnimalViewHolder extends RecyclerView.ViewHolder {  
		
		TextView nameTextView, detailTextView;    
		ImageView circularImage;    
		CardView cardView;  
		
		public AnimalViewHolder(@NonNull View itemView) {      
			super(itemView);      
			
			nameTextView = itemView.findViewById(R.id.textViewName);      
			detailTextView = itemView.findViewById(R.id.textViewDetail);      
			circularImage = itemView.findViewById(R.id.circularImage);    
			  
			cardView = itemView.findViewById(R.id.cardView); //cardView is the id of card in the card_design.xml    
		}  
	}
}  
```  
  
- In `onBindViewHolder` method, attach a click Listener on the cardView.  
```java  
  
public class RecyclerViewAdapter extends RecyclerView.Adapter<RecyclerViewAdapter.AnimalViewHolder>{  
  
//    ..................  
  
    @Override    
    public void onBindViewHolder(@NonNull AnimalViewHolder holder, int position) {
    
	    //  It is called when design is created and connected 
	    // to the recycler view.  
	  
		// It recieves AnimalViewHolder holder that was created 
		// in onCreateViewHolder and got attached to RecyclerView  
	    
	    // Here we transfer the data in the components in the array
	    // into the respective components  
	    
		holder.nameTextView.setText(nameList.get(position));     
		holder.detailTextView.setText(detailList.get(position));
		holder.circularImage.setImageResource(imgIdList.get(position));  
		           
		holder.cardView.setOnClickListener(v -> {  
		    Toast.makeText(context, 
						    nameList.get(position), 
						    Toast.LENGTH_SHORT)
						    .show();
	    });  
    }  
//      ................  
}  
  
```


***

### 
`RecyclerViewAdapter` Full code
```java
public class RecyclerViewAdapter extends RecyclerView.Adapter<RecyclerViewAdapter.AnimalViewHolder>{  
  
    private List<String> nameList;  
    private List<String> detailList;  
    private List<Integer> imgIdList;  
    private Context context;  
  
    public RecyclerViewAdapter(List<String> nameList, List<String> detailList, List<Integer> imgIdList, Context context) {  
        this.nameList = nameList;  
        this.detailList = detailList;  
        this.imgIdList = imgIdList;  
        this.context = context;  
    }  
  
    @NonNull  
    @Override    
    public AnimalViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {  
  
        // here:  
        // parent -> refers to the activity in which the RecyclerView resides, here is it resides in MainActivity  
        // In This method we define the card design that we made        // It is called asa AnimalViewHolder is instantiated        // Create a view then transfer the card design into that        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.card_design, parent, false);  
  
        // Returning AnimalViewHolder with card design view in it  
        return new AnimalViewHolder(view);  
    }  
  
    @Override  
    public void onBindViewHolder(@NonNull AnimalViewHolder holder, int position) {  
//        It is called when design is created and connected to the recycler view.  
  
        // It recieves AnimalViewHolder holder that was created in onCreateViewHolder and got attached to RecyclerView  
        // Here we transfer the data in the components in the array into the respective components  
        holder.nameTextView.setText(nameList.get(position));  
        holder.detailTextView.setText(detailList.get(position));  
        holder.circularImage.setImageResource(imgIdList.get(position));  
        holder.cardView.setOnClickListener(v -> {  
	        Toast.makeText(context, nameList.get(position), Toast.LENGTH_SHORT).show();  
        });  
  
    }  
  
    @Override  
    public int getItemCount() {  
//      Specifies the amount of data to be displayed in the RecyclerView  
        return nameList.size();  
    }  
  
    public class AnimalViewHolder extends RecyclerView.ViewHolder {  
  
        TextView nameTextView, detailTextView;  
        ImageView circularImage;  
        CardView cardView;  
  
        public AnimalViewHolder(@NonNull View itemView) {  
            super(itemView);  
            nameTextView = itemView.findViewById(R.id.textViewName);  
            detailTextView = itemView.findViewById(R.id.textViewDetail);  
            circularImage = itemView.findViewById(R.id.circularImage);  
            cardView = itemView.findViewById(R.id.cardView);  
        }  
    }  
}
```

`MainActivity `Full code

```java
public class MainActivity extends AppCompatActivity {  
  
    RecyclerView recyclerView;  
  
    RecyclerViewAdapter recyclerViewAdapter;  
  
    List<String> nameList = new ArrayList<>();  
    List<String> detailList = new ArrayList<>();  
    List<Integer> imgIdList = new ArrayList<>();  
  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
  
        recyclerView = findViewById(R.id.recyclerView);  
  
        // to specify how the RecyclerView would be arranged  
        recyclerView.setLayoutManager(new LinearLayoutManager(MainActivity.this));  
  
        nameList.add("Bengal Tiger");  
        nameList.add("Polar Bear");  
  
        detailList.add("Found in the tropical regions of Indian Subcontinent.");  
        detailList.add("Found in the ice caps of the Arctic.");  
  
        imgIdList.add(R.drawable.bengal_tiger) ;  
        imgIdList.add(R.drawable.polar_bear);  
  
        // Creating the RecyclerViewAdapter object and passing all the params required.  
        recyclerViewAdapter = new RecyclerViewAdapter(nameList, detailList, imgIdList, MainActivity.this);  
        recyclerView.setAdapter(recyclerViewAdapter);  
  
    }  
}
```

