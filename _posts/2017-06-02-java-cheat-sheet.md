---
published: true
comments: true
layout: post
title: Java Cheat Sheet
---

Some notes I made for the Open University M250 Object-oriented Java programming course. Includes bits of code for the fundamentals of Java.

**Start a Class**
public class Example {

**Start a Constructor**
public Example() {

**Get Character at particular location**
variable.charAt(0);

**Example of:**

**-Message**
variable = person.getInitials();
person.printReverse();

**-Reference Variable Declaration**
Person friend;
String name;

**-Primitive Variable Declaration**
int example = 5;
char letter = a;

**-String Creation**
example = new String(“Alice”);
something = “Something”;

**-Object Construction**
example = new String(“Alice”);
something = “Something”;
friend = new Person(first, second);

**-Operators**
first = new String("Alice");
example = 5 + 10;

**-Actual Arguments Used**
example = new String(“Alice”);

**-Formal Parameters Used**
friend = new Person(first, second);

**-Method Names**
variable = person.getInitials();
person.printReverse();


**Primitive vs Reference Types**

**-Primitive**
Primitive types are basic types of data:

byte, short, int, long, float, double, boolean, char

**-Reference**
Reference types are any instantiable class as well as arrays:

String, Scanner, Random, Die, int[], String[], etc.

**Scope**
Scope refers to the region of code within which a variable name is valid.

**Encapsulation**
AKA Data Hiding. Variables are set to private, use getters/setters to access the data.

**Polymorphism**
An object in Java that passes more than one IS-A tests is polymorphic in nature.
Polymorphism occurs when objects of different kinds respond in their own way to the same message.

**Creating an Interface**
public interface Danceable {
	public void pirouette(int anInteger);
	public void prepareToDance();
}

Interfaces are usually used when classes are otherwise unrelated, but their instances have a common set of messages to which they must respond.

**Method Header**
public class DanceableHoverFrog extends HoverFrog implements Danceable

**Inherit from Superclass**
super();

Superclasses are used to specify common behaviour exhibited by subclasses of the same superclass.

**Loops**

**-For Loop**
for (int i = 0; i < anInteger; i++) {

**-While Loop**
while (this.getPosition() > 5) {


**Static Variable**
Belongs to class itself instead of an instance of the class
private static int dancers = 0;

**Final Variable**
Value cannot change
private final int dancerNum;

**Comparable**
The interface Comparable enforces a protocol on classes that implement it.

A class would implement this interface so as to allow objects of that class to be compared with one another for order i.e. implementing this interface defines a natural ordering for objects of the implementing class.

**Map Declaration**
private SortedMap<Integer, Set<String>> gangTable;
this.gangTable = new TreeMap<>();

**Set Declaration**
HashSet<String> gangMembers = new HashSet<>();

**Defensive Programming**
Defensive programming is a form of defensive design intended to ensure the continuing function of a piece of software under unforeseen circumstances.


**Formal Arguments vs Actual Arguments**

int number1 = 10;
int number2 = 15;
int sum = add(number1, number2);

public int add(int x, int y) {
	return (x + y);
}

**Formal** - (int x, int y)
**Actual** - (number1, number2)

**Operators**
| + |  % | != | <= | && |
|:-:|:--:|:--:|:--:|:--:|
| - | ++ |  > |  & | || |
| * | -- |  < |  | |  ! |
| / | == | >= |  ^ |    |



**Overloading**
Overloading is a feature where a class can have more than one method with the same name. However the arguments must be different. They have either:

Different number of arguments
Different data type in the argument

**Overriding**
Overriding is where a subclass has a method with the same name as one declared in the parent class. It must also have the same arguments as the parent class (if applicable).

**Create an Interface**
public interface Example {
    public void method();
    public void anotherMethod();
}
Interfaces are inherited by subclasses.

**Collections Flow Chart**
![](https://i.stack.imgur.com/aSDsG.png)
Source - [StackOverflow](https://stackoverflow.com/questions/21974361/what-java-collection-should-i-use)
