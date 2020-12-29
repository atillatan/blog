---
layout: article
permalink: 
name: 
file_type: 
title: Java Quick Reference
description: >-
  Java Quick Reference
tags:  java
category:  
sort_order: 100
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2019-10-23
modified_date: 2019-10-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url: 
toc: false
---

#  Java Quick Reference


![image-20201229160759174]({{site.img}}/java-quick-reference/image-20201229160759174.png)


## Features of Java

- Great Performance: 
The Java compiler is designed for performance. Java code is compiled into bytecode and then compiled by the Java compiler. Post that, it is fed to the JVM (Java Virtual Machine) before it’s converted to machine-level code.

- Platform Independence: 
Java has a philosophy called WORA (Writing Once, Run Anywhere). Java code is compiled into an intermediate format, called bytecode, which is to be executed in the JVM (Java Virtual Machine). Any system that runs a JVM is able to execute the Java code.

- Truly Object-Oriented: 
Build upon C++ which is semi object-oriented, Java extends the functionality to become a fully object-oriented programming language. Some of the most important features that make it an object-oriented puritan are:
Abstraction
Encapsulation
Inheritance
Polymorphism

- Robust
Java guides the programmer to adopt important programming habits required for the creation of highly reliable applications. Unlike C and C++, Java relies on a simple memory management model reinforced by the automatic garbage collection feature.

- Secure
Safety features are built into the language and runtime systems. These include runtime checking and static type-checking at compile time. With such features in place, it becomes a daunting task to invade a Java application from the outside.

- Simple
Ease of reading and writing makes any language simple. This holds true for Java as it has a less ambiguous syntax terminology. Anyone can start right off with Java with an understanding of the basic underlying principles of programming.

## 1. Basics

### Compile a Java Program 


- You need to save your Java Program by the name of the class containing `main()` method along with `.java` extension. Example: `className.java`
- Execution of your program is going to start in the main function by default.

```java
public static void main(String[] args){...}
```

- Call the compiler using javac command.

```shell
# Compile your .java file
javac className

# Execute the program
java className 
```

### Comment

- single line comment: // this is inline comment
- multiline comment: /* ..multiline.. */

```java
 // this is in-line comment
 
 /* ..
  this is multiline comment
  */
```


### "TODO" keyword in comment

you can view your all "TODO" list in the "menu: window/Show view/Tasks" view

### Console

- `System.out.println("...")` it writes your message to output. 


### Define Variable

- `int var1=100;` 
- `int var1, var2, var3;` multiple variables on the same time.


### Keywords Terms/Words


| **Keywords** |                                     **Usage**                                     |
| ------------ | --------------------------------------------------------------------------------- |
| import       | it imports libraries into your application. (import  `java.util.*`)               |
| package      | to create a unique application for avoiding conflicts.                            |
| class        | model of real-world system/object                                                 |
| public       | any one/code that has access to your  property/method/class                       |
| private      | property/method/class is only going to be accessible inside our class             |
| protected    | property/method/class is only going to be accessible inside of our class/subclass |
| static       | function/property belongs to the "Class" (not an instance)                        |
| this         | used to refer to the current object in a method or constructor.                   |
| super        | used to refer to the parent class.                                                |
| final        | indicates a constant, its value is never gonna change                             |
| finally      | used to execute code after the try-catch structure.                               |
| implements   | used to implement an interface.                                                   |
| new          | used to create new objects.                                                       |
| enum         | defines a set of constants                                                        |
| extends      | indicates that class is inherited                                                 |
| abstract     | used to declare an abstract class.                                                |
| throw        | used to explicitly throw an exception.                                            |
| throws       | used to declare an exception.                                                     |
| try          | block of code to handle an exception                                              |
| catch        | used to catch exceptions generated by try statements.                             |

## 2. Data Types

![image-20201228121022354]({{site.img}}/java-quick-reference/image-20201228121022354.png)

```java
System.out.println("Byte Max: "+Byte.MAX_VALUE);
System.out.println("Byte Min: "+Byte.MIN_VALUE);
System.out.println("Short Max: "+ Short.MAX_VALUE);
System.out.println("Short Min: "+ Short.MIN_VALUE);
System.out.println("Char Max: "+ (Character.MAX_VALUE+0)); 
System.out.println("Char Min: "+ (Character.MIN_VALUE+0)); 
System.out.println("Int Max: "+ Integer.MAX_VALUE );
System.out.println("Int Min: "+ Integer.MIN_VALUE );
System.out.println("Float Max: "+ Float.MAX_VALUE);
System.out.println("Float Min: "+ Float.MIN_VALUE);
System.out.println("Double Max: "+ Double.MAX_VALUE);
System.out.println("Double Min: "+ Double.MIN_VALUE);
System.out.println("Long Max: "+ Long.MAX_VALUE);
System.out.println("Long Min: "+ Long.MIN_VALUE);

/* 
Byte Max: 127
Byte Min: -128
Short Max: 32767
Short Min: -32768
Char Max: 65535
Char Min: 0
Int Max: 2147483647
Int Min: -2147483648
Float Max: 3.4028235E38
Float Min: 1.4E-45
Double Max: 1.7976931348623157E308
Double Min: 4.9E-324
Long Max: 9223372036854775807
Long Min: -9223372036854775808
*/
```

### Variable Defininion

There are 3 types of variable in java

Definition: 
```java
{public | private} → [static] → type → name → [= expression | value];
```

```java
	// Some examples
  public String var1;
	public int var2= 3;
	private boolean  var4=false;
	public static float var3=1.34F;

```

### Char

```java
	//define special Character
  	char newline = '\n';
		char tab = '\t';
		char backspace = '\b';
		char returns = '\r';
		char doubleQuotes = '"';
		char singleQuotes = '\'';
		char backslash = '\\';		
```

### Float

```java
// Floating point precision 6 decimals
		float fNum = 1.1111111111111111F;
		float fNum2 = 1.1111111111111111F;
		System.out.println("Float : " + (fNum + fNum2));
```

### Double 

- if you need more precision from float you can use double instead.

```java
// Double precision 15 decimals
		double dblNum = 1.1111111111111111;
		double dblNum2 = 1.1111111111111111;
		System.out.println("Float : " +
				(dblNum + dblNum2));
```
- specific/scientific  notation for double

```java
double thousand = 1e+3;
```

### Long

- You can use long as a big number, and you can use scientific notation

```java
long bigNum=123_456_789;
long bigLong=123123145124L;
```

### Data Conversion

- you can convert smaller types to larger types automatically

```java
int smallData=123;//int--> long
long largeData=smallData; //automatic type conversion

```

- otherwise you must use casting notation `(new-type)old-type`

```java
long lng=123;
int i = (int)lng;

// Narrowing 
double d = 10.02;
long l = (long)d; //explicit type casting

// Numeric values to String (Class.WrapperMethod)
String str = String.valueOf(value);
String str2 = Double.toString(1.234);

// String to Numeric values 
int i = Integer.parseInt(str);
double d = Double.parseDouble(str);

```

- If you cast floating-point variables to other numeric types, you'll lose numbers after the point.

### Wrapper class methods

- Use wrapper class to convert to data: `Wrapper.toTargetType();`
  - Double.toString(1.234);

- Use wrapper class to convert String to primitives: `Wrapper.parseTargetPrimitive();`
  - int a=Integer.parseInt("23");
  
### Increment

- `var++;` → `var = var + 1;` 
- `var += 10;` → `var = var + 10;`;

### Math

```java
System.out.println("abs(-1) = "+Math.abs(-1));
System.out.println("ceil(4.25) = "+Math.ceil(4.25));
System.out.println("floor(4.25) = "+Math.floor(4.25));
System.out.println("round(4.25) = "+Math.round(4.25));
System.out.println("max(4,5) = "+Math.max(4,5));
System.out.println("min(4,5) = "+Math.min(4,5));
System.out.println("exp(1) = "+Math.exp(1));
System.out.println("log(1) = "+Math.log(1));
System.out.println("log10(1) = "+Math.log10(1));
System.out.println("pow(2,2) = "+Math.pow(2,2));
System.out.println("sqrt(4) = "+Math.sqrt(4));
System.out.println("cbrt(4) = "+Math.cbrt(4));
System.out.println("hypot(5,5) = "+Math.hypot(5,5));
System.out.println("PI = "+Math.PI);

System.out.println("sin(1.5708) = "+Math.sin(1.5708));
System.out.println("cos(1.5708) = "+Math.cos(1.5708));
System.out.println("tan(1.5708) = "+Math.tan(1.5708));
System.out.println("asin(1.5708) = "+Math.asin(1.5708));
System.out.println("acos(1.5708) = "+Math.acos(1.5708));
System.out.println("atan(1.5708) = "+Math.atan(1.5708));
System.out.println("sinh(1.5708) = "+Math.sinh(1.5708));
System.out.println("cosh(1.5708) = "+Math.cosh(1.5708));
System.out.println("tanh(1.5708) = "+Math.tanh(1.5708));
System.out.println("toDegrees(1.5708) = "+Math.toDegrees(1.5708));
System.out.println("toRadians(90) = "+Math.toRadians(90));
```

### Random number

```java
// Random number between 5 and 20
int minNum = 5;
int maxNum = 20;
int randNum = minNum + (int)(Math.random() * ((maxNum - minNum) + 1));
System.out.println("Rand : "+randNum);
```

### String 

- String is an object, if you surround a "text" with quotations, java automatically creates a String object.

```java
String str1 = “Welcome”; // Using literal
String str2 = new String(”Edureka”); // Using new

String firstName = "Atilla"; // firstName is the defined String object
String fullName = firstName + "Tanrikulu"; //"Tanrikulu" is automatically created String object
```

- `+=` it can be used for concatenation

```java
String name = "Atilla";
String fullName = name + " Tanrikulu";
fullName += " is my name";```

str1==str2 //compares address;
// You cannot compare values of Strings using "=="
String newStr = str1.equals(str2); //compares the values
String newStr = str1.equalsIgnoreCase() //compares the values ignoring the case
newStr = str1.length() //calculates length
newStr = str1.charAt(i) //extract i'th character
newStr = str1.toUpperCase() //returns string in ALL CAPS
newStr = str1.toLowerCase() //returns string in ALL LOWERvCASE
newStr = str1.replace(oldVal, newVal) //search and replace
newStr = str1.trim() //trims surrounding whitespace
newStr = str1.contains("value"); //check for the values
newStr = str1.toCharArray(); // convert String to character type array
newStr = str1.IsEmpty(); //Check for empty String
newStr = str1.endsWith(); //Checks if string ends with the given suffix
newStr = str1.substring(0,3);
newStr = str1.split(" ") // returns Array
newStr = str1.replace("Atilla", "Ati");
newStr = str1.startWith("Atilla"), .endWith("Atilla");

```


note: If you are using Eclipse, you can click  "⌘ + Click" the feature to see any function definitions.

### StringBuilder : Non-Synchronized: hence efficient.

- StringBuilder is a mutable class that is not thread-safe but is faster and is used in a single-threaded environment. 
- StringBuilder, is more effective then regular String for memory usage.
- StringBuilder support String object methods, and it has additional methods
- `.capacity()` Get size set aside
- `.append(" another String object")` append primitive or String
- `.insert(4, " and");`

### StringBuffer: Synchronized

- use it for multi-thread applications, StringBuffer: It is a mutable class that is thread-safe and synchronized.

- StringBuffer support String object methods, and it has additional methods

### Array

- Arrays are put some containers into memory int[10] means we're going to put 10 containers into memory.
- multiple values

```java
int[] ar = new int[10];
ar[0] = 123;
ar[1] = 456; 
//using Arrrays class wrapper metthods
Arrays.fill(ar, 4); //Fill all containers with 4
Arrays.asList(String, Integer, Object); returns List<Object>
```
- Creating Array with values `int[] ar= {1,2,3,4,5};`
-` Arrays.binarySearch(arr, 4); ` find a value.
- Multidimensional array ` int a2[][] = new [4][4];`
- `Arrays.copyOf(targetArray, 4);` you can copy array to array data
- Sort: sort is a very important functionality and 'sort' is a Class Wrapper method.

```java
int[] arr= {1,2,3,5};
Arrays.sort(arr);
Collections.reverse(arr);
```

- Reverse: "reverse" is a very important functionality and `reverse` is a Class wrapper method

```java
int[] arr= {1,2,3,5};
Arrays.sort(arr);
Collections.reverse(arr);
```
Note: If you use LinkedList, you can reverse your list with using the `.previous()` method.

### ArrayList

- inheritance: ArrayList ← AbstractList:List ← Collection ← Iterable (interface)
- ArrayList is not a synchronized collection. 
- We can create synchronized List from ArrayList like that `List<String> list = Collections.synchronizedList(new ArrayList<String>());`
- `ArrayList<Integer> aL2 = new ArrayList<>(Arrays.asList(1,2,3,4));` generates ArrayList
- `arrList.get(2)` get value with index number.
- `arrList.set(1,3)` add value with index.
- `arrList.remove(3);` remove value with index
- `Iterator it= arrlist.iterator()` ArrayList contains Iterator object
- `.sort(Comperator)`

```java
// Loop using iterator
while(it.hasNext()) {
			System.out.println(it.next());
}

// Loop in Array
for(int i=0; i<arr.length(); i++){ 
   System.out.println("val"+i+": "+ arr[i]);
}
```

### LinkedList

- inheritance: LinkedList ← AbstractSequentialList:List ← Collection ← Iterable (interface)
- Each link has a link, before and next element
- important methods
	- `.listIterator()` provide effective sequential access

![image-20201227224145336]({{site.img}}/java-quick-reference/image-20201227224145336.png)

  - `.addAll(Arrays.asList(1,2,3,4));`  
  - `.addFirst();`  
  - `.contains();`  
  - `.set(0,3);` replace  
  - `.get(4);`  
  - `.remove(3);`  
  - `.size();`  
  - `.toArray();` // for purpose sorting e.g : Arrays.sort();
  - `.sort(Comparator)`

### Enum

```java
public enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY 
}

// Accessing enum
Day myVar = Day.FRIDAY;
```

### Java Collections/Data Structures

- The collections framework contained in the java.util.* package 
- Collection framework contains many interfaces such as Collection, Map and Iterator.
- A Collection can hold a group of objects in different ways which `Set`, `List`, and `Queue` provide.

- Iterable is top of the Collections-framework
- Collection extend Iterable: Collection → Iterable

![image-20201229002505436]({{site.img}}/java-quick-reference/image-20201229002505436.png)


|               **Interface**               |               **Description**                |
| ----------------------------------------- | -------------------------------------------- |
| Iterator                                  | object used to traverse through a collection |
| Collection → Iterable                     | collection of elements                       |
| Set → Collection → Iterable               | collection of unique elements                |
| List → Collection → Iterable              | sequence of elements                         |
| Queue → Collection→ Iterable              | special type of list                         |
| SortedSet→ Set → Collection → Iterable    | sorted collection of unique elements         |
| NavigableSet→ Set → Collection → Iterable |                                              |


![image-20201229003123863]({{site.img}}/java-quick-reference/image-20201229003123863.png)

|      **Interface**       |                     **Description**                     |
| ------------------------ | ------------------------------------------------------- |
| Map                      | collection of key and value pairs, which must be unique |
| SortedMap → Map          | sorted collection of key-value pairs                    |
| NavigableMap → SortedMap |                                                         |



## 3. Operations

### Logical Operators

- `>`, `<`, `>=` , `<=` ,  are all as same as in Math
- `==` : equals,  use for primitive types (for objects you can use `.equals` function)
- `!=` : not equals
- `&&` : and
- `||` : or
- `!` : not

| **Operator Category**            | **Operators**                                      |
| -------------------------------- | -------------------------------------------------- |
| Arithmetic operators             | +,-,/,*,%                                          |
| Relational operators             | <, >, <=, >=,==, !=                                |
| Logical operators                | && , \|\|                                          |
| Assignment operator              | =, +=, −=, ×=, ÷=, %=, &=, ^=, \|=, <<=, >>=, >>>= |
| Increment and Decrement operator | ++ , - -                                           |
| Conditional operators            | ?:                                                 |
| Bitwise operators                | ^, &, \|                                           |
| Special operators                | . (dot operator to access methods of class)        |

### if

```java
// single line
boolean canWatch = (age >= 16) ? true : false;

//multiline
if(age >= 16){
 return true;
} else {
 return false;
}
```

### Switch

- We can use it for limited options

```java
		String lang = "de";
		String labelValue = "Unknown";

      switch (lang) {
      case "en":
        labelValue = "Hello";
        break;
      case "de":
        labelValue = "Hallo";
        break;
      default:
        labelValue = "Hello";
        break;
      }
```


### For

```java
// Single line 
for(Integer item: myList) System.out.println(i); 

// over list item
for (String item : myList) {
    System.out.println(item);
}

// over index
for (int i = 0; i < myList.size(); i++) {
     System.out.println(myList.get(i));
}

// over iterator
for (Iterator<Integer> itr1=myList.iterator(); itr1.hasNext(); ) 
{ 
	 System.out.println(itr1);
} 
	
```

### While

```java
int i=0;
while (i<=10) {
  System.out.println(i);
  i++;
}

// break , continue
while (i<10) {
   if(...){
     continue;  
   }else {
     break;
   }   
}
```

### Do ... While

```java
int secretNum = 7;
		int guess = 0;
		do {
			System.out.println("Guess : ");
			if(sc.hasNextInt()){
				guess = sc.nextInt();
			}
		}while(secretNum != guess);
		System.out.println("You guessed it");
```

### recursive 

```java
   public static long fact(long n) {
      if (n = 1)
         return 1;
      else
         return n * fact(n - 1);
   }
   public static void main(String args[]) {
      System.out.println("The factorial of 6 is: " + fact(6));
      System.out.println("The factorial of 0 is: " + fact(0));
   }
```

### Exceptions

```java
try {
      int[] myNumbers = {1, 2, 3};
      System.out.println(myNumbers[10]);
    } catch (Exception e) {
      System.out.println("Something went wrong.");
    } finally {
      System.out.println("The 'try catch' is finished.");
    }
```

###  User Input

Java provides three ways to take an input from the user/console:

Using BufferReader class
Using Scanner class
Using Console class

- Receive input from keyboard, it is located "java.util.stream.IntStream"
- definition `static Scanner sc=new Scanner(System.in);` 
- "System.in" get information from the keyboard
- Scanner receive user input using these methods
   - nextShort, nextByte, nextBoolean, nextInt, nextFloat, nextDouble, nextLong, nextLine
- to check if a valid type was entered

```java 
System.out.println("type something: ");
if(sc.hasNextLine()){ // wait
	String ln=sc.nextLine();
	System.out.println("Received: "+ ln);
}

// Using BufferReader
BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
String name = reader.readLine();


// Using Console
String name = System.console().readLine();
```

### Method definition

- public: any one/code that has access to your  property/method/class
- protected:  property/method/class is only going to be accessible inside of our class/subclass
- private:  property/method/class is only going to be accessible inside our class

```java
{public | private} [static] {type | void} name(arg1, ..., argN ){statements} 
```

```java
private String color;
  
  // Getter
  public String getColor() {
    return color;
  }
  
  // Setter
  public void setColor(String c) {
    this.color = c;
  }
```

### System.format()

```java

String sf1=String.format("name is %s",name);  
String sf2=String.format("value is %f",32.33434);  
String sf3=String.format("value is %32.12f",32.33434);//returns 12 char fractional part filling with 0  

// Print out a damage report
// printf is for formatted output
// %s : Strings
// %d : Integers
// %f : Floats / Doubles 
// %.2f : To limit to 2 decimals
// %c : Characters
// %e : Scientific Notation
// %t : Dates 
// %b : Booleans
System.out.printf("%s Attacks %s and deals "
+ "%d Damage\n", wA.getName(), 
wB.getName(), dmg2WarB);
		
```
## 4. OOPS Concepts

### Object and Class

- Object:  is basic runtime **Instance** 
- Class : **Model**   of real-world system/object etc.

### Inheritance

- The Car class (subclass) inherits the attributes and methods from the Vehicle class (superclass):

```java
class Vehicle {
  protected String brand = "Ford";         // Vehicle attribute
  public void honk() {                     // Vehicle method
    System.out.println("Tuut, tuut!");
  }
}

class Car extends Vehicle {
  private String modelName = "Mustang";    // Car attribute
  public static void main(String[] args) {

    // Create a myCar object
    Car myCar = new Car();

    // Call the honk() method (from the Vehicle class) on the myCar object
    myCar.honk();

    // Display the value of the brand attribute (from the Vehicle class) and the value of the modelName from the Car class
    System.out.println(myCar.brand + " " + myCar.modelName);
  }
}
```
- Class only inherit one class but implement a lot of Interfaces.
- Constructors cannot be inherited by the subclass. but the constructor of the superclass can be invoked from the subclass.
- Provides the concept of reusability
- Inheritance types in Java
   - 1. Single Inheritance: The child class inherits properties from its parent class, which in turn is a child class to another parent class.
   - 1. Multilevel Inheritance: When a child class has two parent classes. In Java, this concept is achieved by using interfaces.
   - 1. Hierarchical Inheritance: When a parent class has two child classes inheriting its properties.

### Super Class

- If your method overrides one of its superclass's methods, you can invoke the overridden method through the use of the keyword super. You can also use super to refer to a hidden field (although hiding fields is discouraged). Consider this class,

```java

public class Superclass {
    public void printMethod() {
        System.out.println("Printed in Superclass.");
    }
}

public class Subclass extends Superclass {
    // overrides printMethod in Superclass
    public void printMethod() {
        super.printMethod();
        System.out.println("Printed in Subclass");
    }
    public static void main(String[] args) {
        Subclass s = new Subclass();
        s.printMethod();    
    }
}
```

### Encapsulation

- The wrapping or enclosing up of data and methods into a single unit is known as encapsulation. 
- Because of,  using apps people are concerned about its functionality and not the code behind it. real-world example: When we take a medicine, we don’t know what chemical it contains, we are only concerned with its effect.

### Polymorphism

- The ability to take more than one form. (by overriding submethods or overloading existing methods.)
- In Java Polymorphism is achieved by the concept of method **overloading** and method **overriding**, which is the dynamic approach.

### Method Overriding

- In a class hierarchy, when a method in a child class has the same name and type signature as a method in its parent class, then the method in the child class is said to override the method in the parent class.

```java
class Animal {
   public void move() {
      System.out.println("Animals can move");
   }
}

class Dog extends Animal {
   public void move() {
      System.out.println("Dogs can walk and run");
   }
}

public class TestDog {

   public static void main(String args[]) {
      Animal a = new Animal();   // Animal reference and object
      Animal b = new Dog();   // Animal reference but Dog object

      a.move();   // runs the method in Animal class
      b.move();   // runs the method in Dog class
   }
}
```

### Method Overloading

- Java programming can have two or more methods in the same class sharing the same name, as long as their arguments declarations are different. Such methods are referred to as overloaded, and the process is called method overloading.

```java
public void add(int, int)
public void add(int, int, int)
```

### Abstract Class

- Superclass that only defines a generalized form that will be shared by all of its subclasses, leaving it to each subclass to implement its methods.

### Interface

- Class only inherit one class but implement a lot of Interfaces.
- They are similar to class except that they lack instance variables and their methods are declared without anybody.
- Variables are public, final and static.
- Class must create all methods as defined by an interface.


### Constructors

- A constructor initializes an object on creation.
- They have the same name as the class.
- They do not have any return type, not even void.
- The constructor cannot be static, abstract or final.
- Non-Parameterized or Default Constructor: Invoked automatically even if not declared
- Parameterized: Used to initialize the fields of the class with predefined values from the user.

## 5. Advanced Operations

### Streams

- Streams represent groups of objects  you can perform aggregate operations on
```java
    // Streams in Java has `.collect()` method, and it takes `Collectors.wrapperMethod()`.  it defines collecting strategies. 
		List<Integer> oneTo10 = IntStream.rangeClosed(1, 10).boxed().collect(Collectors.toList()); 
    // .rangeClosed() : generates a list from start to finish
    // .boxed() :  returns list boxed to an Integer
		List<Integer> squares = oneTo10.stream().map(x -> x * x).collect(Collectors.toList());
		for (Integer x : squares)System.out.println(x);
		
		// Filter eliminates values based on a condition
		List<Integer> evens = oneTo10.stream().filter(x -> (x % 2) == 0).collect(Collectors.toList());
		for(Integer x: evens) System.out.println(x);
		
		// Limit output to 5
		IntStream limitTo5 = IntStream.range(1, 10).limit(5);
		limitTo5.forEach(System.out::println);
		
		int multAll = IntStream.range(1, 5).reduce(1, (x, y) -> x * y);
		System.out.println(multAll);
		
		// Map to double
		DoubleStream stream = IntStream.range(1, 5).mapToDouble(i -> i);
		
		
		// Generate statistics
		IntSummaryStatistics iStats = IntStream.range(1, 10).summaryStatistics();
		System.out.println("Avg " + iStats.getAverage());
		System.out.println("Sum " + iStats.getSum());
		System.out.println("Min " + iStats.getMin());
		System.out.println("Max " + iStats.getMax());
```
-  Streams in Java has some important methods.
- `.collect()` method, and it takes `Collectors.wrapperMethod()`.  it defines collecting strategies. 
- `.filter()`  eliminates values based on a condition
- `.limit()` Limit output to 5

### Lambda Expressions

-	Lambda expressions are functions that can be passed as if they are objects

```java
ArrayList<Integer> oneTo5 = new ArrayList<>(Arrays.asList(1,2,3,4,5));

oneTo5.forEach(x -> System.out.println(x*2)); // onTo5 object passed into forEach() function as "x".

// Write into a function between {....}
oneTo5.forEach(x -> {
  if (x % 2 == 0)
    System.out.println(x);
});

// Generate Fibonacci numbers
List<Integer> fib = new LinkedList<Integer>();

// iterate creates an infinite stream starting
// with 0, 1 as we define and then create the next
// value by adding the previous 2
// We limit to 10 results
// map stores the result
// collect process the list elements into a
// container
fib = Stream.iterate(new int[] { 0, 1 }, t -> new int[] { t[1], t[0] + t[1] })
    .limit(10)
    .map(n -> n[0])
    .collect(Collectors.toList());

fib.forEach(x -> System.out.println(x));
```

### Managing File		

- A File object is a file or directory
```java
		
File f1 = new File("f1.log"); // Create a file object not a file on the drive
f1.renameTo("");
f1.delete();
File d1 = new File("/"); // File object tied to a directory 
d1.isDirectory(); // Check if we have a directory and print files
File[] files = d1.listFiles();

// A stream is a sequence of characters
// Character Streams are strings
// Binary Streams are bytes of data from
// primitive types
// Create a file for writing
File f2 = new File("f2.txt");
try {
  PrintWriter pw = 
      // Formats the data you are writing
      new PrintWriter(
          // Saves data until it is time to write
          new BufferedWriter(
              // Writes characters to the file
              // Add FileWriter(f2, true) to append
              new FileWriter(f2)), true);
  // Write text to the file
  pw.println("This is sample text");
  // Close the file
  pw.close();
} catch (IOException e) {
  // TODO Auto-generated catch block
  e.printStackTrace();
}

// Reading from a file
f2 = new File("f2.txt");

try {
  // Reads data 1 line at a time
  BufferedReader bR = new BufferedReader(
      // Reads 1 character at a time
      new FileReader(f2));
  
  // Read the line
  String text = bR.readLine();
  
  // Stop when null is received (End of File)
  while(text != null) {
    System.out.println(text);
    text = bR.readLine();
  }
  bR.close();
} catch (IOException e) {
  // TODO Auto-generated catch block
  e.printStackTrace();
}
```
- Binary File operations

```java
// You don't have to nest the constructors
File f3 = new File("f3.dat");

// Connects to file to write raw bytes
FileOutputStream fOS;

try {
  
  // FileOutputStream(f3, true) to append
  fOS = new FileOutputStream(f3);
  
  // Adds buffering t write in bulk
  BufferedOutputStream bOS = new BufferedOutputStream(fOS);
  
  // Allows you to write primitives to the stream
  DataOutputStream dOS = new DataOutputStream(bOS);
  
  String name = "Derek";
  int age = 44;
  double bal = 1234.56;
  
  // Write string
  dOS.writeUTF(name);
  // Write int
  dOS.writeInt(age);
  // Write double
  dOS.writeDouble(bal);
  // Close file
  dOS.close();
} catch (IOException e) {
  // TODO Auto-generated catch block
  e.printStackTrace();
}

// Reading with a DataInputStream
f3 = new File("f3.dat");

// File used for the input stream
FileInputStream fIS;

try {
  fIS = new FileInputStream(f3);
  
  // Adds buffering while pulling data
  BufferedInputStream bIS = new BufferedInputStream(fIS);
  
  // Provides methods for reading data
  DataInputStream dIS = new DataInputStream(bIS);
  System.out.println(dIS.readUTF());
  System.out.println(dIS.readInt());
  System.out.println(dIS.readDouble());
  fIS.close();
  
} catch (IOException e) {
  // TODO Auto-generated catch block
  e.printStackTrace();
}
		        
```

### Generics

- All generic method declarations have a type parameter section delimited by angle brackets (< and >) that precedes the method's return type ( < E > in the next example).
- Generics allow to use **any object type** and perform an operation on it.
- You can write a single generic method declaration that can be called with arguments of different types
- The type parameters can be used to declare the return type and act as placeholders for the types of the arguments passed to the generic method, which are known as actual type arguments.
- A generic method's body is declared like that of any other method. Note that type parameters can represent only reference types, not primitive types (like int, double and char).

```java
// generic method printArray
public static <E> void printArray(E[] inputArray) {
  // Display array elements
  for (E element : inputArray) {
    System.out.printf("%s ", element);
  }
  System.out.println();
}

public void printStuff(ArrayList<?> list){
	for(Object x : list) System.out.println(x);
}

// Generic class example
class MyGeneric<T>{
	T val;
	
	public void setVal(T val){
	  this.val = val;
	}
	
	public T getVal(){
		return this.val;
	}
}

```
### Multi-threading

- Process of executing multiple tasks simultaneously, to utilize the CPU.
- A thread is a block of code that is expected  to execute while other blocks of code execute
- Using threads using a class that implements  the Runnable interface

```java
class A extends Thread {
	public void run() {
		for (int i = 1; i <= 5; i++) {
			System.out.println("From thread A : i " + i);
		}
		System.out.println("Exit from A ");
	}
}

class B extends Thread {
	public void run() {
		for (int i = 0; i <= 5; i++) {
			System.out.println("From thread B : i " + i);
		}
		System.out.println("Exit from B ");
	}
}

class ThreadTest {
	public static void main(String args[]) {
		new A().start();
		new B().start();
	}
}
```

- Methods Of Thread Class

| **Method**                               | **Task Performed**                                           |
| ---------------------------------------- | ------------------------------------------------------------ |
| **public void run()**                    | Inherited by class MyThreadIt is called when thread is started, thus all the action takes place in run() |
| **public void start()**                  | Causes the thread to move to runnable state.                 |
| **public void sleep(long milliseconds)** | Blocks or suspends a thread temporarily for entering into runnable and subsequently in running state for specified milliseconds. |
| **public void yield**                    | Temporarily pauses currently executing thread object and allows other threads to be executed. |
| **public void suspend()**                | to suspend the thread, used with resume() method.            |
| **public void resume()**                 | to resume the suspended thread                               |
| **public void stop()**                   | to cause premature death of thread, thus moving it to dead state. |

-  Runnable Interface
-  The run( ) method that is declared in the Runnable interface which is required for implementing threads in our programs.

```java
class X implements Runnable {
	public void run() {
		for (int i = 0; i <= 10; i++) {
			System.out.println("Thread X " + i);
		}
		System.out.println("End of thread X ");
	}
}

class RunnableTest {
	public static void main(String args[]) {
		X runnable = new X();
		Thread threadX = new Thread(runnable);
		threadX.start();
		System.out.println("End of main Thread");
	}
}
```

- **Thread Class vs Runnable Interface: **

| **Thread Class**                                             | **Runnable Interface**                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Derived class extending Thread class itself is a thread object and hence, gains full control over the thread life cycle. | Runnable Interface simply defines the unit of work that will be executed in a thread, so it doesn’t provide any control over thread life cycle. |
| The derived class cannot extend other base classes           | Allows to extend base classes if necessary                   |
| Used when program needs control over thread life cycle       | Used when program needs flexibility of extending classes.    |

- **Synchronized** 

```java
public synchronized void myFunction(){
  // only one thread here
}
```

### Exception Handling

Exceptions in java can be of two types:

```java
try {
  int x = a[2] / b - a[1];
} catch (ArithmeticException e) {
  System.out.println("Division by zero");
} catch (ArrayIndexOutOfBoundsException e) {
  System.out.println("ArrayIndexError");
} catch (ArrayStoreException e) {
  System.out.println("Wrong data type");
}
finally
{
  int y = a[1]/a[0];
  System.out.println("y = " + y);
}
```
- Finally statement: used to handle exceptions that is not caught by any of the previous catch statements. A finally block in guaranteed to execute, regardless of whether or not an exception is thrown.

- **Checked Exceptions**
  - Handled explicitly in the code itself with the help of try catch block.
  - Extended from java.lang.Exception class

- **Unchecked Exceptions**
  - Not essentially handled in the program code, instead JVM handles such exceptions.
  - Extended from java.lang.RuntimeException class

| **Exception Type**                 | Cause of Exception                                           |
| ---------------------------------- | ------------------------------------------------------------ |
| **ArithmeticException**            | caused by math errors                                        |
| **ArrayIndexOutOfBoundException**  | caused by bad array indexes                                  |
| **ArrayStoreException**            | caused when a program tries to store wrong data type in an array |
| **FileNotFoundException**          | caused by attempt to access a nonexistent file               |
| **IOException**                    | caused by general I/O failures.                              |
| **NullPointerException**           | caused by referencing a null object.                         |
| **NumberFormatException**          | caused when a conversion between strings and number fails.   |
| **OutOfMemoryException**           | caused when there is not enough memory to allocate           |
| **StringIndexOutOfBoundException** | caused when a program attempts to access a non-existent character position in a string. |

- Custom Exception

```java
class MyException extends Exception {
	MyException(String message) {
		super(message);
	}
}

class TestMyException {
	public static void main(String args[]) {
		int x = 5, y = 1000;
		try {
			float z = (float) x / (float) y;
			if (z < 0.01) {
				throw new MyException("Number is too small");
			}
		} catch (MyException e) {
			System.out.println("Caught my exception ");
			System.out.println(e.getMessage());
		} finally {
			System.out.println("I am always here");
		}
	}
}
```

### Memory Management - Garbage collections

- STACK (LIFO) : Methods, local variables, reference variables
- HEAP: objects, instance variables, reference variables
- Illustration Memory Management

![image-20201229144245920]({{site.img}}/java-quick-reference/image-20201229144245920.png)

- When a method is called, frame is created on the top of the stack.
- Once a method as completed execution, the flow of control returns to the calling method and its corresponding stack frame is flushed.
- Local variables are created in stack.
- Instance variables are created in the heap and are part of the object they belong to.
- Reference variable is created in stack.

### Annotations 

- The predefined annotation types defined in java.lang are @Deprecated, @Override, and @SuppressWarnings.
- **@Deprecated:**   indicates that the marked element is deprecated and should no longer be used. The compiler generates a warning whenever a program uses a method, class, or field with the
- **@Override:**  informs the compiler that the element is meant to override an element declared in a superclass. Overriding methods will be discussed in Interfaces and Inheritance.
```java
// mark method as a superclass method that has been overridden
@Override 
int overriddenMethod() { }
```
- **@SuppressWarnings:** annotation tells the compiler to suppress specific warnings that it would otherwise generate. In the following example, a deprecated method is used, and the compiler usually generates a warning. In this case, however, the annotation causes the warning to be suppressed.
- **@SafeVarargs** annotation, when applied to a method or constructor, asserts that the code does not perform potentially unsafe operations on its varargs parameter. When this annotation type is used, unchecked warnings relating to varargs usage are suppressed.
- **@FunctionalInterface** annotation, introduced in Java SE 8, indicates that the type declaration is intended to be a functional interface, as defined by the Java Language Specification.
- **@Retention** annotation specifies how the marked annotation is stored:
	- RetentionPolicy.SOURCE – The marked annotation is retained only in the source level and is ignored by the compiler.
	- RetentionPolicy.CLASS – The marked annotation is retained by the compiler at compile time, but is ignored by the Java Virtual Machine (JVM).
	- RetentionPolicy.RUNTIME – The marked annotation is retained by the JVM so it can be used by the runtime environment.
- **@Documented** annotation indicates that whenever the specified annotation is used those elements should be documented using the Javadoc tool. (By default, annotations are not included in Javadoc.) For more information
- **@Target** annotation marks another annotation to restrict what kind of Java elements the annotation can be applied to. A target annotation specifies one of the following element types as its value: 
  -  ElementType.ANNOTATION_TYPE can be applied to an annotation type.
  - ElementType.CONSTRUCTOR can be applied to a constructor.
  - ElementType.FIELD can be applied to a field or property.
  - ElementType.LOCAL_VARIABLE can be applied to a local variable.
  - ElementType.METHOD can be applied to a method-level annotation.
  - ElementType.PACKAGE can be applied to a package declaration.
  - ElementType.PARAMETER can be applied to the parameters of a method.
  - ElementType.TYPE can be applied to any element of a class.
- **@Inherited** annotation indicates that the annotation type can be inherited from the super class. (This is not true by default.) When the user queries the annotation type and the class has no annotation for this type, the class' superclass is queried for the annotation type. This annotation applies only to class declarations.
- **@Repeatable** annotation, introduced in Java SE 8, indicates that the marked annotation can be applied more than once to the same declaration or type use. For more information

### Connecting to the Database

```java
Connection con;

try
{
  Class.forName("com.mysql.cj.jdbc.Driver");
 
  // Used to issue queries to the DB
  con = DriverManager.getConnection("jdbc:mysql://localhost/db", "admin", "***");

  // Sends queries to the DB for results
  Statement s = con.createStatement();

  // Execute the Query
  s.executeUpdate("INSERT INTO MY_TABLE ......");

  // Cycle through the results
  ResultSet result = s.executeQuery("SELECT * FROM MY_TABLE");

  // Also getBoolean, getDate, getDouble, getInt, getLong
  while (result.next()) {
    System.out.println(result.getString("COLUMN_NAME")); 
  }

  // Close DB connection
  con.close();
}catch(ClassNotFoundException e){
  e.printStackTrace();
}catch(SQLException e)
{
  e.printStackTrace();
}

```

### Regular Expressions

- You can use character codes to search for matching data


### Create Web Application

 

### Create web Services

 

### Create RestFULL Services



### References

https://tobloef.com/text2mindmap/
https://hackr.io/blog/features-of-java
https://hackr.io/blog/java-cheat-sheet#java-ide-and-executing-code
https://www.youtube.com/watch?v=n-xAqcBCws4