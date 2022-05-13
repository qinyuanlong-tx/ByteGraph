## Is Java "pass-by-reference" or "pass-by-value"?

I always thought Java uses pass-by-reference. However, Java uses pass-by-value. What is the explanation?

Java is always pass-by-value. Unfortunately, when we deal with objects we are really dealing with object-handles called references which are passed-by-value as well. This terminology and semantics easily confuse many beginners.

It goes like this:

```java
public static void main(String[] args) {
    Dog aDog = new Dog("Max");
    Dog oldDog = aDog;

    // we pass the object to foo
    foo(aDog);
    // aDog variable is still pointing to the "Max" dog when foo(...) returns
    aDog.getName().equals("Max"); // true
    aDog.getName().equals("Fifi"); // false
    aDog == oldDog; // true
}

public static void foo(Dog d) {
    d.getName().equals("Max"); // true
    // change d inside of foo() to point to a new Dog instance "Fifi"
    d = new Dog("Fifi");
    d.getName().equals("Fifi"); // true
}
```
In the example above aDog.getName() will still return "Max". The value aDog within main is not changed in the function foo with the Dog "Fifi" as the object reference is passed by value. If it were passed by reference, then the aDog.getName() in main would return "Fifi" after the call to foo.

## compound assignment operators
Compound assignment oprators such as +=, -=, *=, /=, they don't require casting. For example:
```java
i += j;
```
Was just a shortcut for:
```java
i = i + j;
```
But if we try this:
```java
int i = 5;
long j = 8;
```
Then i = i + j; will not compile but i += j; will compile fine.

it mean that in fact i += j; is a shortcut for something like this i = (type of i) (i + j).

## Swith statement
switch does not support long, float, and double, because the original design of switch is to perform equivalence judgment on those types with only a few values. If the values are too complex, it is more appropriate to use if statement.
```java
// long x = 111;
// switch (x) { // Incompatible types. Found: 'long', required: 'char,
byte, short, int, Character, Byte, Short, Integer, String, or an enum'
//
// }
case 111:
    System.out.println(111);
    break;
case 222:
    System.out.println(222);
    break;
```