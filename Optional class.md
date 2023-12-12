
```
Optional<String> opn = Optional.ofNullable(null);	
		System.out.println(opn.isEmpty()+ "\t "+opn.isPresent());
		
		Optional<String> ope = Optional.empty();
		System.out.println(ope.isEmpty()+ "\t "+ope.isPresent());
		
		Optional<String> op = Optional.of(null);
		System.out.println(op.isEmpty()+ "\t "+op.isEmpty());
```
output
```
true	 false
true	 false
Exception in thread "main" java.lang.NullPointerException
	at java.base/java.util.Objects.requireNonNull(Objects.java:208)
	at java.base/java.util.Optional.of(Optional.java:113)
	at practice.OptionalImpl.main(OptionalImpl.java:14)

```
