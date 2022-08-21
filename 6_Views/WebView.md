- Used to display webpages/HTML.

```xml
<WebView  
    android:id="@+id/web"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    app:layout_constraintBottom_toBottomOf="parent"  
    app:layout_constraintEnd_toEndOf="parent"  
    app:layout_constraintStart_toStartOf="parent"  
    app:layout_constraintTop_toTopOf="parent" />
```

```java
public class MainActivity extends AppCompatActivity {  
  
    WebView webView;  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
  
        webView = findViewById(R.id.web);

		// Setting WebViewClient to be able to render the page
        webView.setWebViewClient(new WebViewClient());  

		// Load a page
        webView.loadUrl("https://google.com");  
    }  

    @Override  
    public void onBackPressed() {  

		// Intercept the back button
		// Go back to previous webpage instead of exiting
		// Only exit if there are no previous web pages
		
		if (webView.canGoBack()){
			webView.goBack();  
		}
	        
	    else {
		    super.onBackPressed();  
		}
    }  
}
```