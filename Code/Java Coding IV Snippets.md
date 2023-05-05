### Creating test data

#### Primitive  array

```java
int[] myIntArray = new int[]{1, 2, 3};

int[] myIntArray = new int[3];

  

int [] a1 = IntStream.range(1, 20).toArray();

System.out.println(Arrays.toString(a1));

// Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
```

#### Primitive 2D array

```java
int[][] dp = new int[m][n]; //init to all 0's

int[][] multi = new int[][]{

  { 0, 0, 0},

  { 0, 0, 0},

  { 0, 0, 0},

};

 int[][] multD = {{2, 4, 1}, {6, 8, 1}, {7, 3, 1}};
```

#### List
```java
List<String> list = Stream.of("one", "two", "three").collect(Collectors.toList());

List<Integer> list = Arrays.asList(1,2,3); // Returns a fixed-size list, but is sortable 

List<Integer> list = List.of(1,2,3); // immutable. cannot sort!

List<Integer> list = Arrays.asList(primitive int[]); // Will not work! Must be Integer[]

list = new ArrayList<>(list);//mutable copies values over

So, just do it directly:

List<Integer> myList = Arrays.stream(myArray).boxed().collect(Collectors.toList());

Or

Integer[] what = Arrays.stream( data ).boxed().toArray( Integer[]::new );

```

#### 2D Lists

```java
/*Declaring 2D ArrayList*/
List<List<Integer> > x = new ArrayList<List<Integer> >(); 

  

/*Adding values to 2nd row*/ ONLY USE Arrays.asList if list size will not change!! (But that's common in matrices)

x.add(2, new ArrayList<>(Arrays.asList(3, 84))); 

#### Set

Set<String> set = Stream.of("one", "two", "three").collect(Collectors.toSet());

Set<String> set = Set.of("one", "two", "three");//immutable

set  = new HashSet<>(set);//mutable
```


#### Maps

Java 9+ testing
```java
Map<String, Integer> test3 = Map.of("a", 0, "b", 2);//immutable!

test3 = new HashMap<>(test3);//mutable
```


#### computeIfAbsent - (put sub DS into a collection safely)
```java
myMap.computeIfAbsent(someKey, key -> new ArrayList<>()).add("someVal");
```
#### getOrDefault

```java
myMap.getOrDefault(someKey, "DEFAULTVALUE");
```


### Java 8 testing:

```java
//NOTE: This technique below should not be used in prod. It has bad memory usage and creation  according to SO: // https://stackoverflow.com/a/6802502/258896

Map<String, String> myMap = new HashMap<String, String>() {{

        put("a", "b");

        put("c", "d");

    }};

  

Map<String, String> map = Stream.of(new String[][] {

  { "Hello", "World" }, 

  { "John", "Doe" }, 

}).collect(Collectors.toMap(data -> data[0], data -> data[1]));

  
  

Map<String, Integer> map = Stream.of(new Object[][] { 

    { "data1", 1 }, 

    { "data2", 2 }, 

}).collect(Collectors.toMap(data -> (String) data[0], data -> (Integer) data[1]));

```
### Convert int[] to Integer[]
```java

Integer[] boxedArray = Arrays.stream(primitiveArray).boxed().toArray(Integer[]::new);

```

### Convert int[] to List/Set
```java

List<Integer> myList = Arrays.stream(myArray).boxed().collect(Collectors.toList());

```