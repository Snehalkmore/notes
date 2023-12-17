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
## 12. Remove Duplicate Elements From List/ Get unique element list
```
 List<String> listOfStrings = Arrays.asList("Java", "Python", "C#", "Java", "Kotlin", "Python");
	
 List<String> uniqueStrings = listOfStrings.stream()
		 .distinct()
		 .collect(Collectors.toList());
```

## 13. Print first 10 Even number
```
IntStream.rangeClosed(1, 10)
		.map(i->i*2)
		.forEach(s->System.out.println(s));
```
## 14. Merge Unsorted Arrays Into Single Sorted Array Distinct
```
int[] a = new int[] {4, 2, 5, 1};
 int[] b = new int[] {8, 1, 9, 5};

List list =  IntStream.concat(Arrays.stream(a), Arrays.stream(b))           //concat method takes streams
        .sorted()
        .distinct()
        .boxed()
        .collect(Collectors.toList());
```

## 15. List Of Pair Of 12 Divisible Numbers
```
List<Integer> list = Arrays.asList(6,4,8,6,7,10,5,1,2);
int sum =12;

IntStream.range(0, list.size())
.forEach(i->{
        IntStream.range(1, list.size())
        .filter(j->(list.get(i)+list.get(j)==sum && i<j))
	.forEach(j->System.out.println("{"+list.get(i)+","+list.get(j)+"}"));
		});
```

## 16. Append zeros at the end of elements
// i/p - 1,2,3,0,0,0,4,0,0,0,5
// o/p - 1,2,3,4,5,0,0,0,0,0,0

```
List<Integer> list = Arrays.stream(arr)
                    .filter(s -> (s > 0))
                    .boxed()
                    .collect(Collectors.toList());
		
for(int i=list.size();i<arr.length;i++) {
   list.add(0);
}
```

## 17. Group elements by length of String
```
List<String> list = List.of("Snehal", "Akash", "Priyanka", "Malan", "Kumar");

final Map<Integer, List<String>> lengthToWords = list.stream()
				.collect(Collectors.groupingBy(String::length, TreeMap::new, Collectors.toList()));
```

## 18. Sum of all digits from number
```
 int i = 15623;

 //one way
Integer sum= Stream.of(String.valueOf(i).split(""))
		 .map(a->Integer.parseInt(a))
		 .collect(Collectors.reducing(0, (a,b)->(a+b)));
		 
		 
 //another way
 sum = Stream.of(String.valueOf(i).split(""))
		 .collect(Collectors.summingInt(Integer::parseInt));
```

## 19. Find Strings starts with Digit
```
 List<String> listOfStrings = Arrays.asList("One", "2wo", "3hree", "Four", "5ive", "Six");
		 
List<String> listOfStringStartsWithDigit = listOfStrings.stream()
		   .filter(str->Character.isDigit(str.charAt(0)))
		   .collect(Collectors.toList());
```

## 20. Find Second largest number from list
```
 List<Integer> listOfIntegers = Arrays.asList(45, 12, 56, 15, 24, 75, 31, 89);
		 
 Integer secondLargNumber = listOfIntegers.stream()
				 .sorted(Comparator.reverseOrder())
				 .skip(1)                                  ........use skip(1).findFirst()
				 .findFirst().get();
```

## 21. Find Common elements from two Lists
```
 List<Integer> list1 = Arrays.asList(71, 21, 34, 89, 56, 28);
 List<Integer> list2 = Arrays.asList(12, 56, 17, 21, 94, 34);
	      
//one way
 List l = Stream.concat(list1.stream(), list2.stream())
	     .collect(Collectors.groupingBy(Function.identity(),Collectors.counting()))
	     .entrySet().stream()
	     .filter(t->t.getValue()>1)
	     .map(s->s.getKey())
	     .collect(Collectors.toList());
	     
	     
 //another way
 List listOfCommonElelemnts = list1.stream()
	    		  .filter(list2::contains)
	    		  .collect(Collectors.toList());
```

## 22. Find first 3 Max and min elements from list
```
List minimum3Numbers= listOfIntegers.stream()
		.sorted()
		.limit(3)
		.collect(Collectors.toList());

List maximum3Numbers = listOfIntegers.stream()
		.sorted(Comparator.reverseOrder())
		.limit(3)
		.collect(Collectors.toList());
```

## 23. Fibbonacci series till n number
```
\\java 8
Stream.iterate(new int[]{0, 1}, t -> new int[]{t[1], t[0] + t[1]})
		.limit(10)
		.forEach(x -> System.out.println("{" + x[0] + "," + x[1] + "}"));

\\ first approach
public static int iterativeFibonacci(int number) {
		List<Integer> list = new ArrayList<>();
		list.add(0);
		list.add(1);
		for (int i = 2; i < number + 1; i++) {
			list.add(list.get(i - 2) + list.get(i - 1));
		}
		return list.get(number);
}

\\recursive approach
public static int fibonacci(int n) {
		if (n <= 1) {
			return n;
		} else {
			return fibonacci(n - 1) + fibonacci(n - 2);
		}
	}
```

## 24. Anagram or not
```
String s1 = "racecar";
String s2 = "carrace";
        
s1 = Stream.of(s1.split(""))
        .map(s->s.toLowerCase())
        .sorted()
        .collect(Collectors.joining());
        
s2 = Stream.of(s2.split(""))
        .map(s->s.toLowerCase())
        .sorted()
        .collect(Collectors.joining());
        
if(s1.equals(s2)) {
        System.out.println("Strings are anagram");
 }else {
       System.out.println("Strings are Not anagram");
 }
```

## Add sufix, prefix and deliminator
```
List<String> listOfStrings = Arrays.asList("Facebook", "Twitter", "YouTube", "WhatsApp", "LinkedIn");
		String updatedString = listOfStrings.stream()
				      .collect(
					  Collectors.joining("|", "[", "]")
					);
```

## From inputed list of strings, find strings starting with "aa" and within those filtered strings find out the unique character count

```
List<String> list = Arrays.asList("aaryanna", "aayanna", "airianna",
				"alassandra", "allanna", "allannah", "allessandra", "allianna",
				"allyanna", "anastaisa", "anastashia", "anastasia",
				"annabella", "annabelle", "annebelle");
list.stream()
		.filter(s->s.startsWith("aa"))
		.collect(Collectors.groupingBy(Function.identity(),
				Collectors.flatMapping(t->Stream.of(t.toString().split("")),Collectors.toSet())))
		.entrySet().stream().forEach(s->System.out.println(s.getKey()+" "+s.getValue().size()));;
	
```
## Find map where key- department name, value -sum of salary of each department
```
List<Employee> list = Arrays.asList(new Employee("SM",2000,"IT"),
				new Employee("AM",2000,"CSC"),
				new Employee("LM",2000,"CSC"),
				new Employee("PM",2000,"IT"),
				new Employee("BM",2000,"IT"),
				new Employee("KM",2000,"Civil")
				);
		
		//get map key- department name, value -sum of salary of each department
		
		Map<String,Integer> map = list.stream()
		.collect(Collectors.groupingBy(Employee::getDepartment,Collectors.summingInt(Employee::getSalary)));

```
