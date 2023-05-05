```Java
//Arrays.asList(t.toCharArray(), new char[1]); // Something weird here

charsToMatch = t.chars().mapToObj(c -> (char)c).collect(Collectors.toSet()); // This resulted in a List that  prints
```