### Convert List to String\[\]

String\[\] strArr = myList.toArray(new String\[0\]);

### Convert List&lt;Integer\[\]&gt; to int\[\]\[\]

No shortcuts. Just make a for loop

List&lt;Integer\[\]&gt; out = new ArrayList<>();

int\[\]\[\] primitiveOut = new int\[out.size()\]\[2\];

int idx = 0;

for(Integer\[\] i : out){

    primitiveOut\[idx++\] = new int\[\]{i\[0\],i\[1\]};

 }

 return primitiveOut;

### Convert Character\[\] to String (GOTCHA)

You can't! it only works with primitive char\[\]'s

new String(char\[\]); 

or

String.valueOf(char\[\]);

### Convert Character\[\] to char\[\] (no shortcut, without Apache Commons, etc)

Remember, "abc".toCharArray() returns a primitive char\[\];

Character\[\] chars = new Character\[\]{'a','b', 'c' };

StringBuilder sb = new StringBuilder(chars.length);

for (Character c : chars)

    sb.append(c.charValue());