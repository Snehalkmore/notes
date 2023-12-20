## What are different ways to create Objects :

### 1. new keyword
```
ClassName c = new ClassName();
```

### 2. Using .forName and getInstance method
```

 Class cls = Class.forName("ClassName");
 ClassName obj = (ClassName)cls.newInstance(); 
```

### 3. Using clone method
```
ClassName c = new ClassName();
Class d = c.clone();
```

### 4. Using deserialization
```
 try{ GFG d = new GFG("GeeksForGeeks"); 
  FileOutputStream f  = new FileOutputStream("file.txt"); 
  ObjectOutputStream oos  = new ObjectOutputStream(f); 
  oos.writeObject(d); 
  oos.close(); 
  f.close(); 
} catch (Exception e) { }
            

Deserialize
try { 
            DeserializationExample d; 
            FileInputStream f  = new FileInputStream("file.txt"); 
            ObjectInputStream oos  = new ObjectInputStream(f); 
            d = (DeserializationExample)oos.readObject(); 
 }catch (Exception e) { }
```

Actual Example
```

public class SerializationDeserializationExample implements Serializable {
	String name;
	public SerializationDeserializationExample(String name) {
		this.name = name;
	}

	public static void main(String[] args) {
		SerializationDeserializationExample s = new SerializationDeserializationExample("Serialization Deserialization Example");
		SerializeMethod(s);
		deserialize();

	}

	private static void SerializeMethod(SerializationDeserializationExample s) {
		try {
			FileOutputStream f = new FileOutputStream("file.txt");
			ObjectOutputStream oos = new ObjectOutputStream(f);
			oos.writeObject(s);
			oos.close();
			f.close();
		} catch (Exception e) {}
	}
	
	private static void deserialize() {
		SerializationDeserializationExample d = null;
		try {
			FileInputStream f = new FileInputStream("file.txt");
      ObjectInputStream oos = new ObjectInputStream(f);
			d = (SerializationDeserializationExample) oos.readObject();
			f.close();
			oos.close();
		} catch (Exception e) {}
 System.out.println(d.name); 
	}
}

```

### 5. 
```
 Constructor<GFG> constructor = GFG.class.getDeclaredConstructor();
GFG r = constructor.newInstance(); 
 r.setName("GeeksForGeeks"); 
```

## How are Java objects stored in memory?

