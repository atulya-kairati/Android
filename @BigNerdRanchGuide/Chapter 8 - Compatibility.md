```
  
android {  
    compileSdk 32  
  
    defaultConfig {  
        applicationId "com.atulya.geoquiz"
        minSdk 23
        targetSdk 32  
        versionCode 1  
        versionName "1.0"  
  
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"  
    }
...
...
}
```

- **Minimum SDK version**: The `minSdk` value is a hard floor below which the OS should refuse to install the app.
- **Target SDK version**: The targetSdk value tells Android which API level your app is designed to run on. Most often this will be the latest Android release.
	- Changing this will change the behaviour of the app.
	- Try to keep it close to the latest Android API.
- **Compile SDK version**:  The compile SDK version specifies which version to use when building your code. When Android Studio is looking to find the classes and functions you refer to in your imports, the compile SDK version determines which SDK version it checks against.
---

#### Jetpack libraries
- Jetpack libraries offer backward compatibility for new features on older devices and provide (or attempt to provide) consistent behavior across Android versions.
- Using them allows us to make the app consitent over various API versions.
---

### Safely adding code from newer APIs

- Annotation `@RequiresApi` can be used to mark a fucntion to be only be executed in compatible Android API.
```java
@RequiresApi(Build.VERSION_CODES.S) // -> S = API 31   
private fun blurCheatButton(){ 
	// Following features are only available after API 31
    val effect = RenderEffect.createBlurEffect(10f, 10f,Shader.TileMode.CLAMP)  
    binding.cheatButton.setRenderEffect(effect)  
}
```

- Now the fucntion can be conditionally called:
```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S) {  
    blurCheatButton()  // Only called if API >= 31
}
```

