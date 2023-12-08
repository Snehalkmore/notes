## 1. Palindrome Example ROTATOR ->ROTATOR

```
boolean isPalindrome = IntStream.range(0, str.length()/2)
                    .noneMatch(i->str.charAt(i)!=str.charAt(str.length()-i-1));
```

## 2. Prime Number
```
List<Integer> primeNumbers =
	            IntStream
	                    .rangeClosed(2,100)
	                    .filter(number -> IntStream.range(2,number/2)
	                            .noneMatch(divider -> number % divider == 0))
	                    .boxed()
	                    .collect(Collectors.toList());

```
Java 7
```
ArrayList<Integer> a = new ArrayList<>();
		for (int n = 1; n <= 100; n++) {
			int c = 0;
			for (int i = 1; i <= n; i++)
				if (n % i == 0)
					c++;
			if (c == 2)
				a.add(n);
			else
				continue;
		}
		System.out.println(a);
```
