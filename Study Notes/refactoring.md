## Data Class

A data class refers to a class that contains only fields and crude methods for accessing them (getters and setters). These are simply containers for data used by other classes.

## Encapsulate Field

Encapsulate fields, private, unless is a class like the Java Point class where values can be constants and easy to access to save to cpu cycles.

## Encapsulate Collection

If a class has a collection of objects, like a List<Student> list... Tne encapsulate it and when returning it, return a copy. Defensive Copy.

## Extract Method

If there is a code fragment that can be grouped together, that you can put a name to it, then move it to a new method and put that name to it and call it.

## Replace Temp with Query

Instead of doing a calculation and saving it in a local variable to be used multiple times in the method, put that calculation in a method and call it when you need it.

## Split Temporary Variable

Don't use a local temp variable to be assigned multiple values, but have one constant variable for each of the values you will use, with the right variable name.

## Separate Query from Modifier

If a method sets something and then gets, separate that logic into 2 different methods, one that sets and the other that gets.

```java

class

```
