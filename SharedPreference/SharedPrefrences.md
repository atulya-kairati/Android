### SharedPreferences Class

- Allows saving and retrieving *primitive* data, in forms of key value pair.
- It is managed by the android framework and can be accessed from anywhere within the application.
- In case an app is abruptly closed, then shared pref can be used to store necessary info in the `onPause` method.
- In a login in page, it can be used to remember the user and pswd.


#### Usage

- Create a `SharedPreferences` object:
```java 
SharedPreferences sharedPreferences;
sharedPreferences = getSharedPreferences("editorTextSave", Context.MODE_PRIVATE);
```

- Save data:
```java
SharedPreferences.Editor editor = sharedPreferences.edit();  
editor.putString("key", "Text to be saved..... lollolololol");  
editor.apply(); // saves all data
```

- Retrieve data:
```java
String savedData = sharedPreferences.getString("key", "Defualt value");
```