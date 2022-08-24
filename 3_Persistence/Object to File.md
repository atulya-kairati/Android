- Save object to a local file.

```java
public class FileHandler {  
    final static String FILENAME = "task_list.dat";  
  
    public static void writeData(Set<String> list, Context context){  
        try {  
  
            FileOutputStream fileOutputStream = context.openFileOutput(FILENAME, Context.MODE_PRIVATE);  
            ObjectOutputStream oos = new ObjectOutputStream(fileOutputStream);  
            oos.writeObject(list);  
            oos.close();  
  
        } catch (IOException e) {  
            e.printStackTrace();  
        }  
    }  
  
    public static Set<String> readData(Context context){  
  
        try {  
            FileInputStream fileInputStream = context.openFileInput(FILENAME);  
            ObjectInputStream ois = new ObjectInputStream(fileInputStream);  
            return (Set<String>) ois.readObject();  
        } catch (ClassNotFoundException | IOException e) {  
            e.printStackTrace();  
        }  
        return new HashSet<>();  
    }  
}
```