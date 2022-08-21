- Give info and capability to take input

```java
Snackbar.make(constraintLayout, "Heres a snackbar!", Snackbar.LENGTH_INDEFINITE)  
        .setAction("Something", v1 -> {  
            // Doing something
        }).show();
```