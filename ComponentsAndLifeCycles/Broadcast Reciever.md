**Important Note**: For Android Oreo (API 26) and later, you must create the "Broadcast Receiver" from java class, not from Manifest File. 


## What is Broadcast Reciever?

1.  A broadcast receiver is **an Android component that allows an application to respond to messages (an Android Intent ) that are broadcast by the Android operating system or by an application**.
2. Broadcast Receivers allow us to register for the system and application events, and when that event happens, then the register receivers get notified.
3. Apps have to subscribe to the Android OS for specific alerts to recieve system msgs.
4. **When the broadcast is sent the system automatically routes broadcasts to appsthat have subscribed to recieve that particular type of update.**


## Creating a Broadcast Reciever

1. Create a class and extend it to `BroadcastReceiver` and implement the inherited methods.
2.  Declaring Reciervers:
	1. Manifest Declared Recievers ( < API 26):
		- Mention the following in the `<application>` tag in the manifest folder.
		```java
		<receiver android:name=".MyBroadcastReciever" android:exported="true">  
		    <intent-filter>  
		    
		        <action android:name="android.intent.action.AIRPLANE_MODE" />  
						   <!-- name -> specifies the type of subsciption -->
		    </intent-filter>  
		</receiver>
		```
	
	2.  Context Registered Recievers ( >= API 26):
		- In the Activity Java class, make an object of your Reciever class.
		- Make an `IntentFilter` obj and add the type of Broadcast by invoking `.addAction` method. 
		- And then register the filter to the Activity by using `this.registerReciever` method.
		- And ungerister in the `onStop` method. 

	```java
	public class MainActivity extends AppCompatActivity {  
  
    MyBroadcastReciever reciever = new MyBroadcastReciever();  
  
    @Override  
    protected void onStart() {  
        super.onStart();  
  
        // Registering the Reciever  
        IntentFilter filter = new IntentFilter();  
        filter.addAction(Intent.ACTION_AIRPLANE_MODE_CHANGED);  
        this.registerReceiver(reciever, filter);  
    }  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {...}  
  
    @Override  
    protected void onStop() {  
        super.onStop();  

		// Unregistering the Reciever  
        this.unregisterReceiver(reciever);  
    }  
}
	```

3. Now you will get the broadcast in `onReceive` method in the Receiver Class.
```java
public class MyBroadcastReciever extends BroadcastReceiver {  
    @Override  
    public void onReceive(Context context, Intent intent) {  
	    
	    boolean isPlaneMode = intent.getBooleanExtra("state", false);  
		String msg = "Is device in Airplane mode: " + isPlaneMode;  
		Toast.makeText(context, msg, Toast.LENGTH_SHORT); 
	
    }  
}
```
