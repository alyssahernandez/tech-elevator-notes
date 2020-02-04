# Objects and the String Class

## What is an object?

An object is an instance of a class. From the book: *An object is an in-memory data structure that combines state and behavior into a usable and useful abstraction. In other words, objects are a collection use variables and methods that make your job easier.*

An object is called upon by a method as many times as you want to use it.

Think of it like a house. A house has windows, doors, maybe a chimney, etc. Those are the properties of a house. Similarly, an object has *attributes*, which are the *properties.*

The house also has actions. You can open a door/window, light a fire, etc. Similarly, there are *actions* and *behaviors* in an object that are known as the *methods.*

What about the house itself? What defines how the house is built? A blueprint. With objects, that blueprint is known as the *class.* It's basically how the class is built.

Here's an example:

- attributes/properties of a house:
  - int windows;
  - int doors;
  - boolean windows;
- we don't know how many windows because we don't have the blueprint yet, but we do know that the action/behavior options, known as the methods, are:
  - open a window
  - open a door
  - start a fire

Basically, we know that whatever house we build, the actions could have windows, a door, and a chimney. Since this is just a basic blueprint, we don't know how many windows/doors the house will have and if it has a chimney, so we can't list specific numbers of attributes. What we can do, however, is list different methods for different possible attributes:

- openWindow (int windowNbr, pctOpen)
- openDoor (int doorNbr, pctOpen)
- fireStart (string typeOfWood)

## What is a Class?

Technically, you don't actually write objects in your code. Objects are just in-memory data structures, so they are only running when the code is executed. What you you are writing in the code is a class, which creates the object when called. It is a group of methods and variables in a source code file that generates objects.

Your class is defined in your code with the class name, properties and methods. Once it's instantiated--and possibly initialized--then we can use the class in the rest of our code.

## Summary: Class vs Object

In the house example, the *class* is the blueprint. In the class `House`, the code defines what the properties and methods that any house can have. The blueprint can be used over and over to create new instances of the house, which are called objects. It's important to note that each house/object has its own atrributes, properties etc. House 1 does not shrae a bathtub with house 2, though the overall structure is the same. The *object* is a manifestation of the that class in memory The class is what you would see in your `.java` files. It only exists in code when it is executed.

From the book: *These are three expressions that make up one very common statement - the creation and initialization of a new object and putting it into a variable where it can be accessed.*

## Creating a Class

Let's see another example. Here, we've created a class:

```java
class Person {
    String firstName;
    String lastName;
}
```

The above code has the option to store two different variables, but it does not exist in memory yet. This is just a blueprint for objects to be created.

## Creating an Object

To create an object, we must use three expressions:

1) declaration: defines a new variable name with its data type. ex: `House houseOnMainSt`. `houseOnMainSt` is a variable of data type `House`. We're assuming the `House` class has already been created.
2) instantiation: creates a new instance of the object and returns the address to it. ex: `new House()`. This creates a new object in heap memory from the `House` class when the code is executed. This creation of the object returns the memory address to the variable we declared.
3) initiation: this starts the object out with initial values in its instance variables. The instance variables are the variables we assigned to the class object that are required to be passed when calling the class. Initiation creates the object, sets its variables and gets it ready for use.

## Naming a Class

You have to name the class to show what "blueprint" you're working with. Just like when you declare an integer as `int x;`, you need to declare the method. You also need to *instantiate* it, which means creating a new *instance* of it.

```java
House mainStreet = new House();
```
The left side of the equation is declaring the house. The right side of the equation is the instantiating the house.

We are physically going to create a house on Main Street, a new house, based on the blueprint/class we just created. 

If you know the number of doors and windows and whether or not you want a chimney, you can do:

```java
House mainStreet = new House(1, 2, true);
```

- Class name: `House`
- Instance name: `mainStreet`
- New object created in memory: `new House`
- Property values: `(1, 2, true)`

The blueprint already tells us what the values are; we just need to put them in. Not only have we declared in the code above, but we've instantiated it as a new house and now, finally, we've initialized it. We've stated that we want to create a house in our program, we've created a new house and passed in the property values.

If you don't know how many doors/windows you want and whether or not you want a chimney, you can prompt the user to enter the values.

## Stack and Heap

Let's review the difference, which is especially relevant to how objects are stored. When an application returns, there is memory allocated for it in the stack. The stack stores basic/primitive data types, such as integers. It knows exactly how much space it will take up, depending on the data type. Integers take up less space than doubles, for example.

When you get into more complicated things, such as an integer array, your computer doesn't know how much space to allocate for the values because it could be any size. Things like arrays, with unknown sizes, cannot be stored in the stack. They have to be stored in the heap, which is flexible and dynamic.

The heap stores objects and arrays because they have unknown sizes. So, an object created is *stored* in the heap, but the *memory address*, known as the variable, is stored in the stack. The address is the only thing stored in the stack. When we use a variable of type array or object in our code, we're simply using the address.

So, all variables are stored in the stack, but their values may be stored in the heap. Data types that are *primitive*, which specific sizes, are stored in the stack. Data types with unknown sizes are called *reference* types. For reference variables, the value stored in the variable (variable located in the stack) is just the memory address.

Using the class `House` that has properties of `chimney`, `doors`, and `windows`, stacked in order from bottom to top, the object would be likewise stacked from bottom to top: `true`, `1`, `1`.
- `chimney` is on the bottom; so is `true`
- `doors` is on top of `chimney`; `1` on top of `true`
- `windows` is on top of `doors`; `2` on top of `1`

Note: Do NOT confuse a class stack with the regular stack!

The value types are in the stack. The instance of the object is in the heap. Objects are heap references to primitive data types in the stack. They are just an instance in memory when it is being used that is in the heap. When it is not being used, there is kind of like a garbage collector that will come in and delete it in the heap. It will still be there in the stack, but the instance won't be taking up memory.

## Two Variables Storing the Same Exact Data

We often see something like this:

```java
int[] a = new int[] { 1, 2, 3 };
int[] b = a;
```

`a` and `b` have the exact same value. There are two variables stored in the stack, but only one array stored in the heap. The variables in the stack, remember, are simply a memory address. Since the values of each variable are exactly the same, the heap saves space by having just one object and multiple address pointing to that object.

Because `a` and `b` point to the same object, if you change the value of one array, such as `b[0] = 100;`, then the value of `a` changes as well because they have the same address.

## Checking Objects for Equality

Previously, we've used the `==` operator to determine if the *value* of two variables is the same. However, this operator behaves differently depending on if the variable is a primitive data type or a reference data type.

If we are comparing the equality of value/primitive variables, the `==` operator is just fine. The variables store a simple value.

If we are comparing the equality of reference variables, the `==` operator may not work the way you want it to. Instead of comparing the values, it compares the two variables to see if they hold the same address. The following code will return true:

```java
String lowerCaseName = new String("java");
String anotherName = lowerCaseName;
lowerCaseName == anotherName;
```

This returns true because `anotherName` points to the exact same object value in the heap as `lowerCaseName`; they have the same address pointing to the same object.

What if instead of assigning the value of `lowerCaseName` to the variable `anotherName`, you assign them the same value separately? Take a look below:

```java
String lowerCaseName = new String("java");
String anotherName = new String("java");
lowerCaseName == anotherName;
```

The above code will return false. Although they have the same values, we've created two new string objects. That means that they have two different address to two similar objects. That's where the `==` falls short. If we want to check if two variables contain the same *content*, it's better to use the `.equals()` method. This applies to reference types:

```java
String lowerCaseName = new String("java");
String anotherName = new String("java");
lowerCaseName.equals(anotherName);
```

The above method would return true, whereas using `==` would make it return false.

## Saving Memory by Having the Same Address / String Equality  / .equals() / .equalsIgnoreCase()

Let's say you have two variables that have the exact same value: `String hello1 = "HelloWorld";` and `String hello2 = "HelloWorld";` The computer would not want to waste space by allocating two memory slots to the same thing. Instead, it would just create one instance of the variable and give each variable the same address to point to the same object.

If we declare the two variables like this:

```java
String hello1 = "HelloWorld";
String hello2Hello = "World";
String hello2World = hello2Hello + "World";
```

If we printed both variables, both would output "HelloWorld", but are they equal?

Using `==` checks the see if the two have the same memory address in memory, which they don't because one is a full string and the other is a string plus a variable.

You *must* use `x.equals("y")` to check to see if the values are the same; not the addresses. The equals method is looking at the *contents* of the string, not the reference.

Let's say we have two strings:

```java
String a = "Hello";
String b = "hello";
boolean aEqualsB = a.equals(b); // false
```

Although they both have the same word, the `.equals()` method requires the words to have the same capitalization as well. If you want to ignore the cases, you would use the `.equalsIgnoreCase()` method:

```java
String a = "Hello";
String b = "hello";
boolean aEqualsB = a.equalsIgnoreCase(b); // returns true
```

## String Equality with Different Capitalization / .toUpperCase() / .toLowerCase()

```java
String hello1 = "HELLO";
String hello2 = "hello";
if (hello1.equals(hello2)) {
    System.out.println("They are equal.");
} System.out.println("They are not equal.");
```

The above output would be `They are not equal.`, even though they're the same word. If the capitalization doesn't matter, you can use the `x.toUpperCase(x)` method, *or* the `x.toLowerCase(x)` method.

```java
String hello1 = "HELLO";
String uppercaseHello1 = hello1.toUpperCase();

String hello2 = "hello";
String uppercaseHello2 = hello2.toUpperCase();

if (hello1.equals(hello2)) {
    System.out.println("They are equal.");
} System.out.println("They are not equal.");
```

Strings are immutable. The methods you call upon them create new instances of the object in memory, and you have to do something with it. That is why you see the declaration of *another* variable. You are not *changing* the value of the variables; you're creating a new instance and need to assign it to something. If you were to omit the declaration of new variables and just used: `hello1.toUpperCase();`, nothing would happen and they would output as unequal.

## See if a String is Within Another String / .contains()

```java
String breakfastSandwich = "vegan sausage and cheese";
boolean containsCheese = breakfastSandwich.contains("cheese");
return containsCheese;
```

The above code would return true. You can do individual characters too.

## See if a String Starts With or Ends With a Letter / .startsWith() / .endsWith()

```java
String hamAndCheese = "ham and cheese sandwich";
boolean startsWithHam = hamAndCheese.startsWith("ham");
return startsWithHam;
```

The above code would return true. Just like the `.contains()` method, you can also check for individual characters.

The same goes for the `.endsWith()`. It works just like the `.startsWith()` method.

## Giving the Position of a Letter in a Word / .indexOf() / .lastIndexOf()

```java
String hello = "hello";
int indexOfL = hello.indexOf("l)";
System.out.println(indexOfL);
```

The output of the above statement would be `2`. However, there are two L's, so how would we give the position of the last L?

```java
String hello = "hello";
int indexOfL = hello.indexOf("l)";
int secondIndexOfL = hello.lastIndexOf("l");
System.out.println(indexOfL);
System.out.println(secondIndexOfL);
```

The above output would be `2`, `3`.

You are also able to check for entire words:

```java
String name = "Java Jones";
int firstJFound = name.indexOf("J"); //  0
int firstLetterOfJones = name.indexOf("Jones"); // 5
```

## Replace Words in a String / .replace()

```java
String name = "Java Jones";
String nameWithReplacements = name.replace("Java", "Justin");
// nameWithReplacements will equal "Justin Jones"
// name will still equal "Java Jones"
```

Strings are immutable. To change the value, you must declare/create a new string when using `.replace()`

## Giving Length of a String / .length()

With `integers` and `arrays`, we've been able to give the length of the variable by using the `.length` method. For example:

```java
int num = 543;
int[] numArray = {
    4, 6, 3, 5, 6
};

System.out.println(num.length);
System.out.println(numArray.length);
```

The above code would print: `3`, `5`. Now, technically the `.length` method can work on strings...

```java
String word = "hello";
System.out.println(word.length);
```

It will output: `5`. But what if you want to give the total number of letters in a string array?

```java
String[] goodMorning = {
    "Hello!", "Buenos", "dias!"
};

System.out.println(goodMorning.length);
```

The above code will output `3`, which is not what we're looking for right now. It's important to note that using `.length` with several words in one variable (`String hello = "Hello to you!";) would throw an error. If you want to know the number of letters, you can use:

```java
String[] goodMorning = {
    "Hello!", "Buenos", "dias!"
};

System.out.println(goodMorning.length());
```

The above code will output: `17` because it's counting the total number of characters.

## Removing Part of a String with Indexes / .substring()

Let's say you want to create a new variable with *part* of a string. You would call this method:

```java
String name = "Alyssa";
String nickname = name.substring(1, 4);
System.out.println(name);
System.out.println(nickname);
```

The above code will output: `lys`. This method is index-based. You might be wondering why the `l` is at the first index, similar to an array, but the `s` is at the fourth index instead of the third, unlike an array. This is because of the way the default class is written:

```java
String str = str.substring(beginIndex, endIndex - 1);
```

Notice instead of `endIndex`, we have `endIndex - 1`. This is just within the methods of the class, so accept it. It's important to note that even though `"Alyssa"` has indexes from 0-5, we would still need to write: `name.substring(1, 6)` if we want to cut out the last letter `"a"`. It will not throw an error because it's taking the value immediately to the left.

#### Spit Out Last Two Letters in a String

There are two ways to do this:

```java
public String extraEnd(String str) {
    
	String toCopy = str.substring((str.length() - 2));
    // this returns everything after this index
	return toCopy + toCopy + toCopy;
}
```

*Or:*

```java
public String extraEnd(String str) {
		
	int startIndex = str.length() - 2;
	int endIndex = str.length();
		
	String toCopy = str.substring(startIndex, endIndex);
    return toCopy + toCopy + toCopy;	
}
```

## Splitting a String Class Into an Array / .split()

If you have a user input an unknown series of numbers separated by spaces, it would seem impossible to split them into a String array if you don't know the number of numbers the user has input. Thankfully, there is a `.split()` method that allows you to pass in a parameter to tell the program where to split the numbers/words into a String array.

```java
String fullName = "Alyssa Marie Hernandez";
String[] fullNameArray = fullName.split(" ");
```

The above code will create an array with three values: "Alyssa, Marie, Hernandez"

## Joining an Array of Strings Into One String / .join()

Oppositely, let's say we have a string array and we want to join it into one string. With the `.split()` method, we have to pass a parameter that declares where we want to separate the original string. When we're joining strings, we need to pass a parameter that declares what we should place between the things we're combining, such as a space, comma, etc.

```java
String[] friendNames = new String[] {
    Lydia, Elizabeth
};

String friendsAltogether = String.join(", ", friendNames);
```

The above code would output: "Lydia, Elizabeth"

## Removing Extra White Spaces / .trim()

If you want to remove the white spaces at the beginning of a string and the end of a string:

```java
String str = " empty white spaces!  ";
System.out.println(str);
System.out.println(str.trim());
```

**REMEMBER:** Strings will *not* change just because you called a value on it. It will only return whatever the result of the method is. If you want to change the string, you have to declare a new variable and assign it to the method you're calling on the original string.

### Programming is an endeavor of creativity and curiosity!!