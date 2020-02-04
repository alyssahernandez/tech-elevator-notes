# Objects

`Null` is returned when an object is declared but not instantiated. It doesn't reference anything.

Strings are reference types.

## Import / Package

When you see `package com.techelevator;`, we are referencing a package that contains a certain set of classes. We can use those classes in our code. If we have another class, such as `import com.animals;`, but we can use both in our code if we import `com.animals`. `import com.animals` will live in the package.

Notice how one uses `package` and the other uses `import`. *Package:* a logical association of a group of classes where the rest of the code will live. Importing a group of classes allows you to store them in the package. Any class that follows the package, either imported or created within the code, is part of the package.

## Using an Array of Numbers with an Unknown Length

Sometimes a user will feed you an array of numbers, but we won't know how many they'll feed us. With a grocery list, for example, they can list as many items as they want. If we declare `int[] groceryList = new int[5];`, this array will hold a max of five objects. Arrays are static with a specific number of slots; they don't handle collections of objects well, especially if our application doesn't know how much data we need to store in them. To combat this problem, we use something called a *list.*

Lists, while you can type them, can hold whatever object you put in there. A list is not an object; it is an interface. (More on interfaces later.) An interface is a contract that says *I will behave in this way; I will let you do these things to me.*

## Creating a List

Here is a list of type string:

```java
List<String> names = new ArrayList<String>();
names.add("Alyssa");
names.add("Ben");
names.add("Zac");
names.add("Dylan");
names.add("Lydia");
```

 Now we have a collection of strings that we want to have all of the behavior of list objects. We have created a list of type String using `List<String>` and we instantiated it by using `= new ArrayList<String>`. We can put as many items as we want in it. Because `ArrayList` is a class and not an interface, we must use open parentheses.
 
 In arrays we've used in the past, we've used open brackets: `String[]`. With lists, we don't have to state how long it is, so we don't need them.

 Notice how in arrays, we use curly braces: 
 
 ```java
 int[] intArray = new int[3] {
     1, 2, 3
 };
 ```

 We don't have to do that with lists. We just use `.add();` method to add things to the list.

## Looping Through an Array List to Print the Values

Instead of using a `for` loop, we use `for each` loops.

```java
for (String name: names) {
    System.out.println(name + " is " + name.length() + " characters long.");
}
```

With a `for` loop, we often use `i` to determine how many times we loop through it. In a list, we replace `i` with a basic name that kind of describes what each variable/object is. We're basically saying *for each name in the names list, we want to print this.*

Because we declared this list as type `String`, we can manipulate all of the objects in the list as strings.

If we wanted to use a `for` loop to out put the values, we have to treat the list like it is an array:

```java
for (int i = 0; i < names.size(); i++) {
    System.out.println(names.get(i));
}
```

The output of this will be a list of names, just like in the `for each` loop. `i` is still used as the variable to determine how many types the for loop will iterate. Instead of using `[]`, we use `()`, similar to when we declare the list. The method `.get()` can only access an item when it has been added.

Unlike arrays, we can actually print the entire list values with a simple statement: `System.out.println(names);`. If `names` was an array, instead of a list, it would print out some nonsense. With lists, however, we *can* print out the entire list values. When printed, it's important to note that it will actually look like a printed array. So:

```java
List<String> names = new ArrayList<String>();
names.add("Alyssa");
names.add("Ben");
names.add("Zac");
names.add("Dylan");
names.add("Lydia");

System.out.println(names);
```

The above will print: `[Alyssa, Ben, Zac, Dylan, Lydia]`

## Adding Items to the List

If we want to add an item to the list, we can just insert it wherever we want and it will print in that order, rather than at the end. Instead of using `name.add("Caitlyn");`, you can also use `names.add(2, "David");` which will specifically place "David" as the third variable. Everything after that simply moves down one; it is not replaced.

## Removing Items from the List

If you *do* want to remove an item in a specific place, you can use: `names.remove(3)`, which will remove the fourth item in the list.

## Converting Lists to Arrays

Notice that we can access the data using indexes. That means that we *are* able to convert lists to arrays. Because the list we created is of type `String`, we need to create a string array. Remember that arrays need to be declared with a specific length.

```java
String[] namesArray = names.toArray(new String[names.size()]);
```

Here, we're combining several things that we already know. When we declare a string array from scratch, we use: `String[] stringArray = new String[5];`. We still need the three expressions (declaration, instantiation and initialization.), so we need to use them in the conversion statement:

- `String[] namesArray' declares the data type with its variable name.
- `= names.toArray()` is the method that converts the list to an array
- `new String[]` creates an instance of the array
- `[names.size()]` initializes the array with the variables it needs to get the array ready for use with the needed specified size

## Checking if a List Item Exists

To see if an item exists, we obviously just want a true or false return type. That's a boolean, of course. We would use the `.contains()` method:

```java
boolean isHeThere = names.contains("David");
System.out.println("Is he there? " + isHeThere);
```

If "David" exists in the list, the output would be: `Is he there? true`.

## Using Primitive Data Types in Lists ***

So, primitive data types cannot be used in lists. They need to be reference types because a list *is* a reference type. In order to use them, we must wrap them in something that *looks* like a reference type, then they can be pumped into a list. EVery primitive data type has an equivalent *primitive wrapper class.* It is an object representation of a primitive value. This* is because a `list` is an object, and objects are not primitive data types; they are references.

- `int` -> `Integer`
- `boolean` -> `Boolean`
- `double` -> `Double`
- `byte` -> `Byte`
- `char` -> `Character`
- `float` -> `Float`
- `long` -> `Long`
- `short` -> `Short`

To convert, we must simply do something we refer to as boxing the data type:

```java
Integer employees = new Integer(25);
Integer buffetSpots - new Integer("22");
```

In the code above, what is in the parentheses are the *constructors.* 

## Queues

Let's say someone is in line at the Apple store to buy a phone. They will be the first one to purchase the phone and the first one to leave the store. Months later when that person comes back for the new phone, they will enter the back of the line. Basically, first in, first out. Lists are the same way. How does that apply to a list? We declare a queue:

```java
Queue<String> priorities = new LinkedList<String>();
```

Now, we've declared a new interface. Because it is an interface, we still have to declare a type. In this case, it is type `String`. It is no longer a list; it is a different interface. With interfaces, we have to declare an object. They look very similar, but they obviously have a different interface type and a new interface name (`priorities` here).

```java
Queue<String> priorities = new LinkedList<String>();

priorities.offer("Go shopping");
priorities.offer("Go for a walk");
priorities.offer("Brush teeth");
priorities.offer("Go to sleep");
```

Let's say instead of a `String` container, you want to use a class that you declared elsewhere. In the following example, we've created a `Dog` class with different methods and objects. `Dog` is the class, `.offer` is a method that comes with the `Queue` data type, `dogOne` etc are objects We want to create a program that tells you which dog to watch in which order in the form of a queue:


## Clarify Later *******

```java
Dog jimmy = new Dog("Jimmy");
jimmy.walk();

***

Queue<Dog> myDogWalk = new LinkedList<Dog>();
// Queue is the type. Dog is the class name.
// myDogWalk is the name/variable.

Dog dogOne = new Dog("name here"); // predefined elsewhere

***

Queue<Integer> myIntQueue = new LinkedList<Integer>();

int x = 5;

myIntQueue.offer(x);

***

myDogWalk.offer(dogOne);
// dogOne is an instance/object of the Dog class
// .offer is a method that comes with the Queue type
myDogWalk.offer(dogTwo);
myDogWalk.offer(dogThree);

while (myDogWalk.size() > 0) {
// this will loop through every instance/object of Dog
    Dog walkingDog = myDogWalk.poll();
    // .poll is a method that comes with the Queue stack
    // that uses the first-in-first-out approach
    walkingDog.call();
    // this is a method/behavior that we created; when called
    // it will execute for each instance/object via loop
    walkingDog.walk();
    // same with this one
}
```

## List Items in a Queue in Order

You don't have to use indexes with queues. You can just use the `.priorities` method:

```java
while (priorities.size() > 0) {
    String nextPriority = priorities.poll();
    System.out.println("NEXT PRIORITY" + nextPriority);
}
```

The `.poll` method will take the next item in the code without worrying about how many items are in the queue or how many items have been added.

In a practical example, maybe you have 20 tickets that you want to give away in order of first-come-first-serve. You can use the queue `.priorities` and `.poll` methods, with the `while` loop, to give the tickets away to the first 20 people in the list:

```java
while (priorities.size() < 21) {
    String nextTicket = priorities.poll();
    System.out.println("NEXT PRIORITY" + nextTicket);
}
```

The above code will poll the people in the queue, one by one, until we've reached 20 people. Then it will stop.

## Stacks

Let's say you have four Amazon boxes stacked on your porch. The bottom one was put there first, of course, and you can't reach it until you've removed the other three boxes on top of it. Whereas a `queue` is first-in-first-out, with a `stack`, it is last-in-last-out. A `stack` is another interface type. Here's how you declare it:

```java
Stack<String> amazonBoxesStack = new Stack<String>();
```

## Adding Items to a Stack

To add items to a stack, we push them:

```java
Stack<String> amazonBoxesStack = new Stack<String>();
amazonBoxesStack.push("toothbrushes");
amazonBoxesStack.push("gloves");
amazonBoxesStack.push("face wash");
amazonBoxesStack.push("spiralizer");
```

In the above code, the Amazon box on the bottom of the stack will be the box that contains toothbrushes.

## Removing Items from a Stack

We can use a while loop, so that while there are items in the stack, we remove them. Removing an item from a stack uses the `.pop` method. 

```java
while (amazonBoxesStack.size() > 0) {
    String mostRecentBox = amazonBoxesStack.pop();
    System.out.println("MOST RECENT STACK: " + mostRecentBox);
}
```

In the above code, the first output of the loop will be: `MOST RECENT STACK: spiralizer`. Last in, first out.

Notice that we created a container variable, `String mostRecentBox`. We technically don't *have* to in this case, since we are just printing it out onto the screen. Here's another way to write it to simplify the code:

```java
while (amazonBoxesStack.size() > 0) {
    System.out.println("MOST RECENT STACK: " + amazonBoxesStack.pop());
}
```