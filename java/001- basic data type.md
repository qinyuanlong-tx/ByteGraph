# Java Programming Basic

## Basic data type in Java
There are 8 data types in Java.
| data type  | use byte | arrange of value |
| ------     | ------   | ------           |
| byte       | 1        | [-128, 127]      |
| short      | 2        | [-2^15, 2^15-1]  |
| int        | 4        | [-2^31, 2^31-1]  |
| long       | 8        | [-2^63, 2^63-1]  |
| char       | 2        | [0, 2^16-1]
| float      | 4        | []
| double     | 8        | 
| boolean    | 1        | true, false      |

These basic types can express precise data in computer except float and double. why is that? 

Let's see how to store float first. We know that computer store digits by binary number, just 0 and 1. The way transfer a decimal number to a binary number is:

-  

## Integer cache pool

## String in deep
String is immutable in Java. An immutable class is simply a class whose instances cannot be modified. All information in an instance is initialized when the instance is created and the information can not be modified. There are many advantages of immutable classes. This article summarizes why String is designed to be immutable. This post illustrate the immutability concept in the perspective of memory, synchronization and data structures.


References:

https://www.1024sou.com/article/487079.html

https://juejin.cn/post/6982381498452148260