
## String
String is declared final, so it can't be inherited.
String use char array to store dara in java 8.
```java
public final class String implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
}
```

In java 9 and later version, String use byte array to store data and use coder to identity the encoding.
```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final byte[] value;
    /** The identifier of the encoding used to encode the bytes in {@codevalue}. */
    private final byte coder;
}
```

String is immutable in Java. An immutable class is simply a class whose instances cannot be modified. All information in an instance is initialized when the instance is created and the information can not be modified. There are many advantages of immutable classes. This article summarizes why String is designed to be immutable. This post illustrate the immutability concept in the perspective of memory, synchronization and data structures.


1. Requirement of String Pool

String pool (String intern pool) is a special storage area in Method Area. When a string is created and if the string already exists in the pool, the reference of the existing string will be returned, instead of creating a new object.


The following code will create only one string object in the heap.
```java
String string1 = "abcd";
String string2 = "abcd";
```
If a string is mutable, changing the string with one reference will lead to the wrong value for the other references.

2. Caching Hashcode

The hashcode of a string is frequently used in Java. For example, in a HashMap or HashSet. Being immutable guarantees that hashcode will always be the same so that it can be cashed without worrying about the changes.That means, there is no need to calculate hashcode every time it is used. This is more efficient.

In String class, it has the following code:
```java
private int hash;   //this is used to cache hash code.
```

3. Facilitating the Use of Other Objects

To make this concrete, consider the following program:
```java
HashSet<String> set = new HashSet<String>();
set.add(new String("a"));
set.add(new String("b"));
set.add(new String("c"));
for(String a: set)
    a.value = "a";
```

In this example, if String is mutable, its value can be changed which would violate the design of set (set contains unduplicated elements). Of curse, the example above is just for demonstration purpose and there is no value field in a real string class.

4. Security

String is widely used as a parameter for many java classes, e.g. network connection, opening files, etc. Were String not immutable, a connection or file would be changed and this can lead to a serious security threat. The method thought it was connecting to one machine, but was not. Mutable strings could cause a security problem in Reflection too, as the parameters are strings.

Here is a code example:

boolean connect(string s){
if (!isSecure(s)) {
throw new SecurityException();
}
//here will cause problem, if s is changed before this by using other references.    
causeProblem(s);
}
5. Immutable objects are naturally thread-safe

Because immutable objects can not be changed, they can be shared among multiple threads freely. This eliminates the requirements of doing synchronization.

In summary, String is designed to be immutable for efficiency and security reasons. This is also the reason why immutable classes are preferred in many cases in general.
