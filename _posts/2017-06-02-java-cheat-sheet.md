---
published: true
comments: true
layout: post
title: Java Cheat Sheet
---

Some notes I made for the Open University M250 Object-oriented Java programming course. Includes bits of code for the fundamentals of Java.

_Start a Class_
public class Example {

_Start a Constructor_
public Example() {

_Get Character at particular location_
variable.charAt(0);

_Example of:_

_-Message_
variable = person.getInitials();
person.printReverse();

_-Reference Variable Declaration_
Person friend;
String name;

_-Primitive Variable Declaration_
int example = 5;
char letter = a;

_-String Creation_
example = new String(“Alice”);
something = “Something”;

_-Object Construction_
example = new String(“Alice”);
something = “Something”;
friend = new Person(first, second);

_-Operators_
first = new String("Alice");
example = 5 + 10;

_-Actual Arguments Used_
example = new String(“Alice”);

_-Formal Parameters Used_
friend = new Person(first, second);

_-Method Names_
variable = person.getInitials();
person.printReverse();


_Primitive vs Reference Types_

_-Primitive_
Primitive types are basic types of data:

byte, short, int, long, float, double, boolean, char

_-Reference_
Reference types are any instantiable class as well as arrays:

String, Scanner, Random, Die, int[], String[], etc.

_Scope_
Scope refers to the region of code within which a variable name is valid.

_Encapsulation_
AKA Data Hiding. Variables are set to private, use getters/setters to access the data.

_Polymorphism_
An object in Java that passes more than one IS-A tests is polymorphic in nature.
Polymorphism occurs when objects of different kinds respond in their own way to the same message.

_Creating an Interface_
public interface Danceable {
	public void pirouette(int anInteger);
	public void prepareToDance();
}

Interfaces are usually used when classes are otherwise unrelated, but their instances have a common set of messages to which they must respond.

_Method Header_
public class DanceableHoverFrog extends HoverFrog implements Danceable

_Inherit from Superclass_
super();

Superclasses are used to specify common behaviour exhibited by subclasses of the same superclass.

_Loops_

_-For Loop_
for (int i = 0; i < anInteger; i++) {

_-While Loop_
while (this.getPosition() > 5) {


_Static Variable_
Belongs to class itself instead of an instance of the class
private static int dancers = 0;

_Final Variable_
Value cannot change
private final int dancerNum;

_Comparable_
The interface Comparable enforces a protocol on classes that implement it.

A class would implement this interface so as to allow objects of that class to be compared with one another for order i.e. implementing this interface defines a natural ordering for objects of the implementing class.

_Map Declaration_
private SortedMap<Integer, Set<String>> gangTable;
this.gangTable = new TreeMap<>();

_Set Declaration_
HashSet<String> gangMembers = new HashSet<>();

_Defensive Programming_
Defensive programming is a form of defensive design intended to ensure the continuing function of a piece of software under unforeseen circumstances.


_Formal Arguments vs Actual Arguments_

int number1 = 10;
int number2 = 15;
int sum = add(number1, number2);

public int add(int x, int y) {
	return (x + y);
}

_Formal_ - (int x, int y)
_Actual_ - (number1, number2)

_Operators_
| + |  % | != | <= | && |
|:-:|:--:|:--:|:--:|:--:|
| - | ++ |  > |  & | || |
| _ | -- |  < |  | |  ! |
| / | == | >= |  ^ |    |



_Overloading_
Overloading is a feature where a class can have more than one method with the same name. However the arguments must be different. They have either:

Different number of arguments
Different data type in the argument

_Overriding_
Overriding is where a subclass has a method with the same name as one declared in the parent class. It must also have the same arguments as the parent class (if applicable).

_Create an Interface_
public interface Example {
    public void method();
    public void anotherMethod();
}
Interfaces are inherited by subclasses.

_Collections Flow Chart_
![](https://i.stack.imgur.com/aSDsG.png)
Source - [StackOverflow](https://stackoverflow.com/questions/21974361/what-java-collection-should-i-use)
