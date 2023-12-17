# @FunctionInterface
some of the examplese of function interface are:
1. Callable ->call method
2. Runnable ->run method
3. Comparator ->compare method

## 1. Function<T, R>
```
public interface Function<T, R> {
      R apply(T t);
}
```
example
```
Function < String, Integer > function = (t) -> t.length();
System.out.println(function.apply("Ramesh"));
```


## 2. Predicate<T>
```
public interface Predicate<T> {
    boolean test(T t);           // * @param t the input argument
}
```
example
```
  Predicate < Integer > predicate = (t) -> {
            if (t % 2 == 0) {return true; } else {return false;}
  };
  System.out.println(predicate.test(10));
```



## 3. Consumer <T>
```
public interface Consumer < T > {
    void accept(T t);           //* @param t the input argument
}
```
example
```
 Consumer < String > consumer = (t) -> System.out.println(t);
 consumer.accept("Ramesh");
```


## 4. Supplier<T>
```
public interface Supplier<T> {
    T get();
}
```
example
```
Supplier < LocalDateTime > supplier = () -> LocalDateTime.now();
System.out.println(supplier.get());
```



## 5. BiFunction<T, U, R>
```
public interface BiFunction<T, U, R> {
     R apply(T t, U u); // Other default and static methods
}
```
example
```
BiFunction < Integer, Integer, Integer > multiplication = (t, u) -> (t * u);
System.out.println(multiplication.apply(200, 100));
```

### BiFunction used in Map.replaceAll method
One of the typical examples of using this interface in the standard API is in the Map.replaceAll method, which allows replacing all values in a map with some computed value.
Let’s use a BiFunction implementation that receives a key and an old value to calculate a new value for the salary and return it.
```
Map<String, Integer> salaries = new HashMap<>();
salaries.put("John", 40000);
salaries.put("Freddy", 30000);
salaries.put("Samuel", 50000);

salaries.replaceAll((name, oldValue) -> 
  name.equals("Freddy") ? oldValue : oldValue + 10000);
```
