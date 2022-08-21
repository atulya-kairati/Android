- Used to take text input from user.

Examples
```xml
<EditText  
    android:id="@+id/name"  
    android:layout_width="300dp"  
    android:layout_height="wrap_content"  
    android:layout_marginTop="40dp"  
    android:ems="10"  
    android:hint="Enter Name"  
    android:inputType="textPersonName"  
    android:minHeight="48dp"  
    android:textColorHint="#757575"  
    android:autofillHints="" />  
  
<EditText  
    android:id="@+id/password"  
    android:layout_width="300dp"  
    android:layout_height="wrap_content"  
    android:layout_marginTop="16dp"  
    android:ems="10"  
    android:hint="Enter Pasword"  
    android:inputType="numberPassword"  
    android:minHeight="48dp"  
    android:textColorHint="#757575" />
```

```java
EditText name;  
EditText password;  
Button submit;  
TextView result;

name = findViewById(R.id.name);  
password = findViewById(R.id.password);  
submit = findViewById(R.id.submit);  
result = findViewById(R.id.result);  
  
submit.setOnClickListener(v -> {  
    Editable nameText = name.getText();  
    Editable passText = password.getText();  
  
    result.append(nameText.toString() + " " + passText.toString() + "\n");  
  
    nameText.clear();  
    passText.clear();  
  
});
```