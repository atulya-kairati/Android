- Usually used to present user with confirmation dialogs.
- Consist of components such as:
	- Title
	- Message
	- NegetiveButton
	- PositiveButton

```java
private void showAlertDialog() {  
    AlertDialog.Builder alertDialog = new AlertDialog.Builder(this);  
  
    alertDialog.setTitle("Confirm")  
            .setMessage("Turn red?")  
            .setNegativeButton("No", (dialog, which) -> {  
                dialog.cancel();  
            })  
            .setPositiveButton("Yes", (dialog, which) -> {  
                constraintLayout.setBackgroundColor(Color.RED);  
            })  
            .show();  
  
    alertDialog.create();  
}
```