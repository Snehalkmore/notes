## Core Java

### Can we implement the finalize method in java? 
we can overrride the finalize method.Object class contains this method, garbage collector is always calls this method before destroying the object

protected void finalize throws Throwable{}

```
public class demo {
	protected void finalize() throws Throwable
	{
		try {
                        System.out.println("inside demo's finalize()");
		}
		catch (Throwable e) {throw e;
		}
		finally {
			System.out.println("Calling finalize method"+ " of the Object class");
			super.finalize();
		}
	}
	public static void main(String[] args) throws Throwable
	{       demo d = new demo();
		d.finalize();
	}
}
```

### Overriding & overloading in java ?
#### Overrriding -
    1. Run-time polymorphism is also known as dynamic or late binding polymorphism.
    2. Occurs between superclass and subclass
    3. Have the same method signature (name and method arguments)

#### Overloading -
    1. Compile-time polymorphism is also known as static or early binding polymorphism
    2. occurs within class
    3. have same method name but the parameters are different

### What is method hiding ?
if a subclass defines a static method with the same signature as a static method in the super class, in such a case, the method in the subclass hides the one in the superclass.

### Why to write equals and hashcode in java ?

```
1) .equals -> it checks the content equality
2) == operator -> it checks the reference equality


1. If o1.equals(o2), then o1.hashCode() == o2.hashCode() should always be true.
2. If o1.hashCode() == o2.hashCode() is true, it doesn’t mean that o1.equals(o2) will be true.
```

### Exception chaining
```
1.Parent (checked) -child(unchecked) ->working
2.Parent (Unchecked) -child(checked) ->NOT working
3.Parent(Checked)-Child(no exception)->working
4.Parent(UnChecked)-Child(no exception)->working
5.Parent(no Exception)-Child(checked)->NOT working
6.Parent(no exception)-Child(unchecked)->working
7.in case of both checked Exception -> hierachy parent should have higher hierachy exception 
   7.1 parent(Ioexception)->child(FileNotFoundException)-working
   7.2 parent(fileNotFoundException)->child(IOException)-not working
```
![image](https://github.com/Snehalkmore/notes/assets/14993594/e61ecb0c-145c-4cc7-bc13-f87e6d73428b)





### Access Modifiers
```
1. default - variable/methods only accessible within package
2. public - accessible from all packages
3. private - variables/methods only accessible within class
4. protected - accessible within package and outside package, it will accessible by child class
```

### what is marker interface in java can you give some examples of marker interfaces in java ? 
Marker interface does not have any abstract method. but by implementing these interface, JVM get to know the functionality to be performed.
```
1. Clonnable
2. Serializable
3. Remote Interface
4. RandomAccess
```

### Internal working of hashmap?


### How to clone object and diff between Shallow and Deep clone
1. We need to implement marker interface Clonable to achieve the cloning and We need to override the clone method from Object class to achieve cloning
```
 public Object clone() throws CloneNotSupportedException { 
        return super.clone(); 
    } 
```
2. Shallow Copy - When we do copy of some entity to create two objects, but if we change state of one object, then it should get reflected in other object, then this process is called shallow copy
```
class ABC  
{    
int x = 30;  
}  
public class ShallowCopyExample   
{     
    public static void main(String argvs[])   
    {    
	ABC obj1 = new ABC();    
	ABC obj2 = obj1;      ..................shallow copy
	obj2.x = 6;   
        System.out.println("The value of x is: " + obj1.x);  .......it will change value of x for both instances
    }  
}   
```
4. Deep Copy - when we want to copy the enitity to create two objects, but changes in one entity should not affect the other entity, in that case we perform the Deep copy.
```
class ABC  {  
int x = 30;  
}  
public class DeepCopyExample {     
	public static void main(String argvs[])   
	{  
		ABC obj1 = new ABC();   
		ABC obj2 = new ABC();  ...........two seperate objects wont affect properties of each other
                obj2.x = 6;   
		System.out.println("The value of x is: " + obj1.x);  
	}  
}   
```



### what is generic and why to use generic ?
Generics means parameterized types. Using Generics, it is possible to create classes that work with different data types
1. Stronger type checks at compile time.
2. Code Reuse
```
class Test<T> {
	T obj;
	Test(T obj) { this.obj = obj; } 
	public T getObject() { return this.obj; }
}

class Main {
	public static void main(String[] args)
	{	
		Test<Integer> iObj = new Test<Integer>(15);
		System.out.println(iObj.getObject());

		Test<String> sObj = new Test<String>("GeeksForGeeks");
		System.out.println(sObj.getObject());
	}
}

```

We can also pass multiple Type parameters in Generic classes. 
```
class Test<T, U>
{
    T obj1;  
    U obj2; 
 
    Test(T obj1, U obj2)
    {
        this.obj1 = obj1;
        this.obj2 = obj2;
    }
 
    public void print()
    {
        System.out.println(obj1);
        System.out.println(obj2);
    }
}
class Main
{
    public static void main (String[] args)
    {
        Test <String, Integer> obj = new Test<String, Integer>("GfG", 15);
        obj.print();
    }
}
```

Generic Functions
```
class Test {
    static <T> void genericDisplay(T element)
    {
        System.out.println(element.getClass().getName()
                           + " = " + element);
    }
    public static void main(String[] args)
    {
        genericDisplay(11);
        genericDisplay("GeeksForGeeks");
        genericDisplay(1.0);
    }
}
```




### Java 9 Features

1. Try-With Resources -declare resource outside of try block and pass reference to try block
2. Interface Private Methods
3. @SafeVarargs annotation on method and parameterized constructor - used to check wether method performing safe operations or not
4. Java Collection Factory Methods - unmodifiable instances of collections.
An unmodifiable collection provides space efficiency benefits and prevents the collection from accidentally being modified.
```
List<String> stringList = List.of("a", "b", "c");
Set<String> stringSet = Set.of("a", "b", "c");
Map<String, Integer> stringMap = Map.of("a", 1, "b", 2, "c", 3);
```
6. Stream api change - TakeWhile, dropWhile and ofNullable
example
```
//takeWhile- till condition is matched take all elements
System.out.println(courses.stream()
.takeWhile(course->course.getReviewScore()>=95)
.collect(Collectors.toList()));  

//dropWhile - drop all elements until it satisfy condition and take rest of elements once condition satisfied
System.out.println(courses.stream()
.dropWhile(course->course.getReviewScore()>=95)
.collect(Collectors.toList()));
```


### Final keyword - where to use

- to make any class, method or variable in non changable form, we need to make them final.
  1. final variable - cannot change value once assigned
  2. final method - CANNOT override method, can be overloaded
  3. final class - final class can not be extended



### Immutable
```
1. Declare the class as final so it can’t be extended.
2. Make all of the fields private so that direct access is not allowed.
3. Don’t provide setter methods for variables.
4. Make all mutable fields final so that a field’s value can be assigned only once.
5. Initialize all fields using a constructor method performing deep copy.
6. Perform cloning of objects in the getter methods to return a copy rather than returning the actual object reference.
```
example
Since String is immutable, it always does deep copy and create new object in case if we try update the state of object. this just make sure that original object wont change its state.
```
public class StringCopyExample   {     
	public static void main(String argvs[])   
	{  
	String obj1 = new String("JavaTpoint is a very good site.");  
	String obj2 = obj1;                                               ...copy object referance
	System.out.println("The hash code of obj1 is: " + obj1.hashCode());
	System.out.println("The hash code of obj2 is: " + obj2.hashCode());

	obj2 = "JavaTpoint is very good.";  
  
	System.out.println("The hash code is: " + obj1.hashCode());    .... both objects have different hashcode and corresponding string values as well
	System.out.println("The string is: " + obj1 + "\n");  
  
	System.out.println("The hash code is: " + obj2.hashCode());  
	System.out.println("The string is: " + obj2);  
	}  
}

****************Output**********************************************************
The hash code is: -2026030341
The hash code is: -2026030341
The hash code is: -2026030341
The string is: JavaTpoint is a very good site.

The hash code is: 1724527163
The string is: JavaTpoint is very good.

```

Custom immutable class
```
import java.util.HashMap;
import java.util.Iterator;

public final class FinalClassExample {
	private final int id;
	private final String name;
	private final HashMap<String,String> testMap;

	public int getId() {return id;}

	public String getName() {return name;}

	// Getter function for mutable objects
	public HashMap<String, String> getTestMap() {
		return (HashMap<String, String>) testMap.clone();  // clone the exisitng object
	}

	// Constructor method performing deep copy
	
	public FinalClassExample(int i, String n, HashMap<String,String> hm){
		System.out.println("Performing Deep Copy for Object initialization");
		// "this" keyword refers to the current object
		this.id=i;
		this.name=n;

		HashMap<String,String> tempMap=new HashMap<String,String>();   // temp new map
		String key;
		Iterator<String> it = hm.keySet().iterator();
		while(it.hasNext()){
			key=it.next();
			tempMap.put(key, hm.get(key));
		}
		this.testMap=tempMap;                                      //assign temp map to this
	}

	public static void main(String[] args) {
		HashMap<String, String> h1 = new HashMap<String,String>();
		h1.put("1", "first");
		h1.put("2", "second");
		String s = "original";
		int i=10;
		
		FinalClassExample ce = new FinalClassExample(i,s,h1);
		
		System.out.println("ce id: "+ce.getId());
		System.out.println("ce name: "+ce.getName());
		System.out.println("ce testMap: "+ce.getTestMap());

		// change the local variable values
		i=20;
		s="modified";
		h1.put("3", "third");

		// print the values again
		System.out.println("ce id after local variable change: "+ce.getId());
		System.out.println("ce name after local variable change: "+ce.getName());
		System.out.println("ce testMap after local variable change: "+ce.getTestMap());
		
		HashMap<String, String> hmTest = ce.getTestMap();
		hmTest.put("4", "new");
		
		System.out.println("ce testMap after changing variable from getter methods: "+ce.getTestMap());

	}

}
```


### Concept of serializable? When you don’t use serializable then what kind of exception you face.

In Java, a NotSerializableException exception is thrown when an instance of a class must implement the Serializable interface.
The exception is thrown by either the serialization runtime, or by the instance of the class. 
The argument for the NotSerializableException is the name of the class.




### String vs StringBuilder vs StringBuffer

1. String is immutable whereas StringBuffer and StringBuilder are mutable classes.
2. StringBuffer is thread-safe and synchronized whereas StringBuilder is not. That’s why StringBuilder is faster than StringBuffer.
3. String concatenation operator (+) internally uses StringBuffer or StringBuilder class.
4. For String manipulations in a non-multi threaded environment, we should use StringBuilder else use StringBuffer class.



### inner class create seperate .class file



### how overriding internally works?
ava tooling, interestingly, optionally allows use of the @Override attribute on interface methods. By default it is not allowed. But when enabled, will generate a warning or error when a method does not override an existing base class method or interface method.



### How many classloader exists in jvm
1. Bootstrap Class Loader – It loads JDK internal classes. It loads rt.jar and other core classes for example java.lang.* package classes.
2. Extensions Class Loader – It loads classes from the JDK extensions directory, usually $JAVA_HOME/lib/ext directory.
3. System Class Loader – This classloader loads classes from the current classpath. We can set classpath while invoking a program using -cp or -classpath command line option.



### System.out.println() in Java
Where System is the class name, it is declared as final. The out is an instance of the System class and is of type PrintStream. Its access specifiers are public and final. It is an instance of "java.io.PrintStream". When we call the member, a PrintStream class object creates internally.
So, we can call the print() method.








