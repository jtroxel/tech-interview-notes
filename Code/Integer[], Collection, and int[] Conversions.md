### Convert int\[\] to Integer\[\]

Integer\[\] boxedArray = Arrays.stream(primitiveArray).boxed().toArray(Integer\[\]::new);

### Convert int\[\] to List/Set

List&lt;Integer&gt; myList = Arrays.stream(myArray).boxed().collect(Collectors.toList());

Set&lt;Integer&gt; mySet = Arrays.stream(myArray).boxed().collect(Collectors.toSet());

### Convert List&lt;Integer&gt; to int\[\] (COMMON)

int\[\] array = myList.stream().mapToInt(myInt-\> myInt).toArray();

list.stream().mapToInt(num -> Integer.parseInt(num)) 

.filter(num -> num % 3 == 0) 

      .forEach(System.out::println); 

### Convert List&lt;Integer&gt; to Integer\[\] (Normally, you probably want the int\[\] solution above)

myList.toArray(new Integer\[0\]);

or

myList.toArray(new Integer\[myList.size()\]);

https://stackoverflow.com/a/5061692/258896