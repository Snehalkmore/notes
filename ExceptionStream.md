
```
@FunctionalInterface
public interface CheckedFunction<T,R> {
    R apply(T t) throws Exception;
}
```


implementation
```
public static <T,R> Function<T,R> wrap(CheckedFunction<T,R> checkedFunction) {
  return t -> {
    try {
      return checkedFunction.apply(t);
    } catch (Exception e) {
      throw new RuntimeException(e);
    }
  };
}
```

utilize
```
myList.stream()
       .map(
              wrap(item -> doSomething(item)))
       .forEach(System.out::println);
```
