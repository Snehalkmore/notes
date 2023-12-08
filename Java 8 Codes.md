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
Java 7 Prime Number
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

##  3. String Reverse
```
String str = "Snehal More";		

IntStream.range(0, str.length())
.mapToObj(i->str.charAt((str.length()-i)-1))                   //........... eroM lahenS
.forEach(System.out::print);
		
String reversed = Stream.of(str.split(" "))
		.map(s->new StringBuilder(s).reverse())
		.collect(Collectors.joining(" "));                 //........... lahenS eroM
		System.out.println("\n"+reversed);

```
## 4. Reverse Array
```
int[] array = new int[] {5, 1, 7, 3, 9, 6};
		
List list = IntStream.rangeClosed(1, array.length)
		.map(i->array[array.length-i])
		.boxed()
		.collect(Collectors.toList());
```
## 5. Vowels in String
```
String input="Snehal";
		
List<String> vowels=new ArrayList<String>(Arrays.asList("a","e","i","o","u"));

Stream.of(input.split(""))
.filter(e->vowels.contains(e))
.collect(Collectors.toList())
.forEach(s->System.out.println(s));

```

## 6. Sort List of String on basis of length
```
List<String> listOfStrings = Arrays.asList("Java", "Python", "C#", "HTML", "Kotlin", "C++", "COBOL", "C");
		
List listOfStringsWithLengthWiseOrdered = listOfStrings.stream()
		.sorted(Comparator.comparing(String::length))
		.collect(Collectors.toList());
```

## 7. Sort number on basis of occurances and sort by numbers as well in case same number of occurance
Arrange based on No of occurrence If 2 or more element has same number of occurance then it has to sorted ascending
i/p: 5,2,8,8,5,5,8,1,9,0,1,1,0,1 
o/p: 2 9 0 0 5 5 5 8 8 8 1 1 1 1

```
list.stream()
   .collect(Collectors.groupingBy(Function.identity(),Collectors.counting()))
   .entrySet()
   .stream()
   .sorted(Map.Entry.comparingByValue())
   .forEach(s->{
            IntStream.range(0, s.getValue().intValue())
              .forEach(a->System.out.print(s.getKey()+" "));
					
});
```

## 8. Sort Number in DESC order
```
 List<Double> decimalList = Arrays.asList(12.45, 23.58, 17.13, 42.89, 33.78, 71.85, 56.98, 21.12);

 List<Double> sortedList =  decimalList.stream()
                            .sorted(Comparator.reverseOrder())
                            .collect(Collectors.toList());
		 
```

## 9. Seperate Odd and Even Number From List [ use COllectors.partitioningBy(Predicate) ]
```
List<Integer> listOfIntegers = Arrays.asList(71, 18, 42, 21, 67, 32, 95, 14, 56, 87);

		listOfIntegers.stream()
		.collect(Collectors.partitioningBy(i->i%2==0))
		.entrySet()
		.forEach(s->System.out.println(
				(s.getKey().equals(true)?"even = ":"odd = ")
				+s.getValue()));
```

## 10. Swap Two String without third string
```
String a = "abc";
String b = "def";

a = a.concat(b);                                        //...abcdef
b = a.substring(0, a.length() - b.length());            //.....abc
a = a.substring(b.length());                           //......def

```

## 11. Remove Repeatating String
//input - "AA","BB","CC","AA"
//output - BB, CC

```
List<String> listOfString = new ArrayList<String>(Arrays.asList("AA","BB","CC","AA"));		
listOfString =  listOfString.stream()
		.collect(Collectors.groupingBy(Function.identity(),Collectors.counting()))
		.entrySet()
		.stream()
		.filter(e->e.getValue()==1)
		.map(e->e.getKey())
		.collect(Collectors.toList());
```
## 12. 
