## Services
1. Services are application components that can perform long running operation in the background.
2. No UI involved
3. 3 types:
	1. **Foreground**: 
		- User sees the process.
		- Notifications are involved.
		- Must continue even after user leaves the app.
		- Ex: Downloads or Media player

	2. **Background**:
		- User doesn't see
		- No notification
	
	3. **Bound**:
		- Dependent on the component that calls it.
		- Ends when the component that called it ends and doesn't operate in the background.
		- Type of Client - Server relation between service - component


## Services Classes
1. 2 types:
	1. **Service Class** -> Uses main thread of the app, should not be used for resource intensive tasks.
	2. **Intent Service Class**: These run on a different thread than the main thread
		- ==Deprecated since Android 8== -> Use Workmanager 

## Creating a Service (Service Class)

1. Create a class which extends to `Service` class.
2. Implement the required methods (`onBind`, `onCreate`, `onStartCommand` and `onDestroy`).
3. `onBind` -> for Bound Service.
4. Other methods are defined for regular service.
5. Then add the service in the manifest file (in `<application>` tag) as so: 
```xml
<service android:name=".MyService"/>  %% MyService is the name of service class %%
```
6. Start the Service.
```java
Intent i = new Intent(getApplicationContext(), MyService.class);  
startService(i);
```
7. Stop the service.
```java
Intent i = new Intent(getApplicationContext(), MyService.class);  
stopService(i);
```
8. Service can also be stopped by by calling `selfStop()` method in `onStartCommand` method from within the service.
