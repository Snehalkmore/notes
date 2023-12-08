## 1. Palindrome Example ROTATOR ->ROTATOR

```
boolean isPalindrome = IntStream.range(0, str.length()/2)
                    .noneMatch(i->str.charAt(i)!=str.charAt(str.length()-i-1));
```

## 2. Prime Number
```
List<Integer> primeNumbers = IntStream.rangeClosed(2, 100)
				.filter(
						number -> IntStream.range(2, number)
						.noneMatch(divider -> number % divider == 0)
						).boxed().collect(Collectors.toList());

```
Java 7
```
ArrayList<Integer> a = new ArrayList<>();
		for (int j = 1; j <= 100; j++) {
			int c = 0;
			for (int i = 1; i <= j; i++)
				if (j % i == 0)
					c++;
			if (c == 2)
				a.add(j);
			else
				continue;
		}
		System.out.println(a);
```



