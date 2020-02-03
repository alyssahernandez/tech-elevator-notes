# Objects and the String Class

What is an object? An object is an instance of a class.

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

Your class is defined in your code with the class name, properties and methods. Once it's instantiated--and possibly initialized--then we can use the class in the rest of our code.

## Summary: Class vs Object

In the house example, the *class* is the blueprint. In the class `House`, the code defines what the properties and methods that any house can have. The class is what you would see in your `.java` files. It only exists in code. The *object* is a manifestation of the that class in memory.

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

Using the class `House` that has properties of `chimney`, `doors`, and `windows`, stacked in order from bottom to top, the object would be likewise stacked from bottom to top: `true`, `1`, `1`.
- `chimney` is on the bottom; so is `true`
- `doors` is on top of `chimney`; `1` on top of `true`
- `windows` is on top of `doors`; `2` on top of `1`

Note: Do NOT confuse a class stack with the regular stack!

The value types are in the stack. The instance of the object is in the heap. Objects are heap references to primitive data types in the stack. They are just an instance in memory when it is being used that is in the heap. When it is not being used, there is kind of like a garbage collector that will come in and delete it in the heap. It will still be there in the stack, but the instance won't be taking up memory.

## Saving Memory by Having the Same Address / String Equality  / .equals()

Let's say you have two variables that have the exact same value: `String hello1 = "HelloWorld";` and `String hello2 = "HelloWorld";` The computer would not want to waste space by allocating two memory slots to the same thing. Instead, it would just create one instance of the variable and give each variable the same address to point to the same object.

If we declare the two variables like this:

```java
String hello1 = "HelloWorld";
String hello2Hello = "World";
String hello2World = hello2Hello + "World";
```

If we printed both variables, both would output "HelloWorld", but are they equal?

Using `==` checks the see if the two have the same address in memory, which they don't because one is a full string and the other is a string plus a variable.

You *must* use `x.equals("y")` to check to see if the values are the same; not the addresses. The equals method is looking at the *contents* of the string, not the reference.

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

## Removing Extra White Spaces / .trim()

If you want to remove the white spaces at the beginning of a string and the end of a string:

```java
String str = " empty white spaces!  ";
System.out.println(str);
System.out.println(str.trim());
```

**REMEMBER:** Strings will *not* change just because you called a value on it. It will only return whatever the result of the method is. If you want to change the string, you have to declare a new variable and assign it to the method you're calling on the original string.

### Programming is an endeavor of creativity and curiosity!!