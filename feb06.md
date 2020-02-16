# Introduction to Classes / Object Oriented Program

So far, we've really only been able to complete simple tasks with primitive data types. We touched on the Collections framework, but now can take a deeper dive into creating more complex objects. We're at the point where we can start making our own data types. In order to do so, we need to start creating different classes.

## What is Object Oriented Programming

Up until this point, we've created basic command applications that look like this (with some pseudocode):

```java
public static void main(String[] args) {

// get input
// is it valid
// for every arg in args, do some work
// tell the user what I did

}
```

Let's take Amazon, for example. Think about 

Instead of programming procedures, we program behaviors:

- order an item
- view the shopping cart

This allows us to program how they interact with each other and define basic behaviors.

Let's take a cook at some items in a cart:

- toothbrush
- perishable food
- clothes
- holiday decorations

There are unique characteristics to each of the items:

- warehouse location ? may be shared as well, but could be unique
- perishable/non-perishable
- delivery time
- seller

Although they seem very different, behaviors allow us to define how they're common and how they interact. They all have similar characteristics with different values: 

- SKU
- shipping method
- price
- seller

Some of the characteristics may be either unique or shared, and it can change per object. There are *many* different conditions we could test for--many different properties--but think of how *long* that would take. It's just not efficient.

## Benefits of OOP
OOP gives us a way to model real world things in code. We can reuse the objects over and over, and there are many different instances of the object, just like the real world.

## What Are Classes?

Of course, programmers often need to solve problems that Java doesn't have a solution for, such as having an online shopping cart or social media profile. There are no built-in classes for those; we need to create our own classes (*data type*) and define what *behaviors* and *characteristics* it has.

Defining behaviors and characteristics within a class keeps our code clean because it doesn't clutter it and you can reuse it. Think of a class as a *blueprint*; you can create as many objects from it as you want.

Interviewers will more than likely ask us to write a basic class.

## Characteristics/Attributes/Properties of Object Oriented Programming

- encapsulation
- polymorphism
- inheritance

*Encapsulation*: Class behaviors and values are hidden inside the class. Anything outside of the class cannot modify it. If we have an item class, for example, we don't want the shopping cart to be able to modify the properties of it. Encapsulation ensures that for each class, its behaviors and values are hidden. We encapsulate methods and values.

*Polymorphism*: The ability to take on different forms, even though some of the properties may be similar. For example, diamond and coal have similar characteristics--a lot of carbon--but we need to make sure our second form has the the same properties and methods as our base things.

*Inheritance*: You need to make sure that objects can take many forms, and you can accomplish that through inheritance. In order to take many forms (polymorphism), you need to have similar properties and behaviors. They don't necessarily have to be parent/child classes, although it usually is that way.

An easy way to remember all of these, because you may be asked in an interview, is "easy as PIE."

Let's simplify it by creating an item class:

```java
Class Item {
    SKU;
    Location;
    Name;
    Price;
}
```

That class is a basic blueprint from which everything is derived. It is called a *superclass*. Other languages may refer to it as a *base class.* It is the basis for everything. Think of it like this: all of the Amazon items have those variables/qualities, but the specific values may be different. The specific values are defined in *subclasses.* All of the subclasses will share those same attributes/properties.

If we take the `Food` item, we're probably going to inherit something from the `Item` class. The `Food` item would be the *subclass.* It will still have a `SKU`, `Location`, `Name` and `Price`. Everything we derived from the `superclass` item will need those properties. Inheritance ensures that `Food` has all of those attributes within the *superclass*.

`Food` will have unique attributes as well: `Use By Date`, `Refrigeration or Not`, etc.

## Class Behaviors/Methods

Superclasses have methods, as well. In the Amazon items case, there could be methods such as:

- addToCart()
- ship()
- isInStock()
  - this may seem like a property, but it's a value we have to return. in this case, a `boolean`
  - `if (isInStock()) { addToCart; }
  - although we *could* declare this as a property, it would have to 
- quantityInStock()
  - same with the above

Methods are kind of synonymous to *functions*. In a broader sense, a *method*, as it pertains to a behavior, is particular to that class. A *function*, in that sense, does something and returns a value (think: `length * width = area;`).

With our `Food` example, if we have the `ship()` method defined in our *superclass*, we need to have a way to make sure the `Food` item ships differently than the rest of the items if it's perishable.

So, with the *superclass* having a `ship()` method, we can define the unique shipping method within the *subclasses*. As long as we define out superclass in the most generic sense, our subclasses, in ways that are meaningful to their unique type, can have unique values for those attributes and parent methods. If that is the case, and the subclasses have a shipping method different from the default shipping method, we can use something called `@Override`. Example, within the `Food` item, we can say:

```java
Ship() {
    deliverByRefrigeratorDrone;
}
```

That way, the `Food` item's `ship()` method will use its own version of `Ship()`. It's only specific to that item (and all instances of that item).

 So, with that `ship()` method, rather than declaring a specific `ship()` method within each and every item, we can create a simple `for each` loop within the parent class that loops through each item and ships it:

```java
for (Item i : Cart) {
    i.ship();
}
```

In the above, we don't need to specify, and we don't care, about each individual item's ship method. The above code will simply ship it. The subclasses define the shipping method, but they still all need to be shipped.

## Naming Conventions

The name of a class is a noun that is a proper name. That means it is capitalized/pascal case; not camel case. It also means that they are singular. There is one "Alyssa".

Checkout this code below:

```java
public void setHour(int hour) {
        this.hour = hour;
    }
```
Notice the `void` statement, which simply means this particular method doesn't return anything.

## Creating a Class

### Constructors

We can create a class and list all of the properties and methods, but if we try to call it in our main file, nothing is going to happen. We have to include something called a *constructor* to tell us how construct an object from the blueprint. Contructors are public and exposed.

Constructors have the same name as the class they are in. Here's an example of one:

```java
public class Clock {
/// this is the main class

    private int hour;
    private int minute;
    private int second;

    public Clock(int hour, int minute, int second) {
    // this is the constructor that allows you to
    // call/instantiate the class & pass in arguments
    // in this case, when called, a user can pass in
    // arguments that define what time it is

        this.hour = hour;
        this.minute = minute;
        this.second = second;
    }
}
```

## Encapsulation / Access Modifiers

You may have noticed the use of `private` and `public` in the code above. These are called *access modifiers* and they allows you to restrict or hide access to the contents of a class, method or variable.

Here's the textbook definition of *encapsulation*: *Encapsulation lets you restrict access to the internal mechanism of how the class works by hiding or protecting its variables. This way, the values remain consistent and don't contradict each other.

A `public` access modifier means it can be accessed outside* of the class. All top-level classes must be `public`, otherwise the java program wouldn't be able to access any of the other classes within, so the program wouldn't be able to function properly. Other classes, and even other programs, can access it as well.

A `private` access modifier means that the method or variable can only be accessed within the class it is declared. This is considered the best practice because you don't want other places in the code to access it. We wouldn't even be able to access them within an instance of a class. You can only access them through the `getter` and `setter` methods.

## Things in a Class

- package
- import
- private properties
- public properties
- accessors/gets/sets (getName())
- constructors
- public methods
- private methods

```java
public class Animal {

	public String name; // a String property called name; public access modifier so everyone can use it
	
	public String family; // public because this is something outside files/classes can change
	// someone else defined our family, we can't change it
	
	public String genus;

    public Animal() {
        // default constructor. this says that we just
        // want to work with an object called Animal
    }

    public Anima (String dogName, int age) {
        name = dogName
    }
```

## Basic Outline for Building an Application

1) *classes* - blueprints for what variables and methods an object has
2) *variables and properties* - represent the object's state
3) *methods* - indicate an object's behavior

## Creating a Clock

Let's start with a simple application: building a clock. With one clock, we *could* just use the following code and update it:

```java
int hour = 11;
int minute = 23;
int second = 42;
```

However, this code wouldn't be reusable and if you want to use *two* clocks, they would need to be arrays and then you would have to make sure you are updating all of them at the same time... Yeah, it's messy. So, let's make it easy and create a reusable class.

```java
Clock.java // main class needs to match the file name

public class Clock {
    // some code with properties, methods etc
}
```

Using the keyword `class` lets you create your own data type.

## Creating an Instance of a Class

We've obviously declared different data types before:

```java
int x = 10;
boolean raining = true;
String[] str = new String[3];
```

When we're creating an instance of a class, known as an *object*, it's going to look very similar to the `String` array declaration:

```java
Clock clock = new Clock();
```

The above code:

- `Clock` : the data type
- `clock` : the name of the variable
  - a reference to the memory location of the object
- `new Clock()` : the memory location of the new instance
  - memory is allocated to store this object

REMEMBER: When you're working with reference data types, you *must* use the word `new`. You're creating a new instance of an object in the `heap`, so it references a different memory location.

## Giving Our Class Some Properties

Okay, so we've at least created an empty class. Now we can fill it with properties, otherwise known as characteristics. Properties add *state* to the class, meaning every time you create a new instance of it, it will have its own state that can fluctuate.

With our clock, it might be a good idea to add in properties such as the hour, minute and second, because those are the characteristics we want to represent.

```java
// Clock.java
public class Clock {
    private int hour;
    private int minute;
    private int second;

    public void setHour(int hour) {
        this.hour = hour;
    }

    public void setMinute(int minute) {
        this.minute = minute;
    }

    public void setSecond(int second) {
        this.second = second;
    }

    public int getHour() {
        return this.hour;
    }

    public int getMinute() {
        return this.minute;
    }

    public int getSecond() {
        return this.second;
    }
}
```

Great! So we have our class with a few basic properties: `hour`, `minute` and `second`. These properties are stored within the class, so they will be stored in memory for the lifetime of the instance. The above code might look a bit overwhelming, but we'll break it down to understand everything.

The first thing to note would be the use of `this.`. All that keyword means is each instance of this class will have a variable that refers to *this* specific instance.

All of the properties in the clock example are by themselves; none of the three ints are dependent upon each other. What if you *do* need a property that depends on another?

## Dependent Properties

An example of this would be taking user input for a full name. In one box, you might have `firstName` and in another box `lastName`. That's just a minor example. In our clock example, we've separately declared the `hour`, `minute` and `second` properties. Sure, that's useful, but if we want to tell the time with just one property, we could add this near the top of our code:

```java
public String getCurrentTime() {
        return this.hour + ":" + this.minute + ":" + this.second;
    }
```

Now, that would return something like: `02:54:49`.

## Defining Methods

In Java, all properties are accessed via *methods* called *getters* and *setters.* You can see those in the code above: `setHour`, `getHour`, etc. It's very clear which is which--it's in the name. Basically, methods are called when you want to *do* something with the data.

For our clock, we want it to tick. That's a behavior. When a clock ticks, it moves up by one second. How can we represent that in code? The following code will look similar to the big bulk of code above, but pay attention to the method and if statements near the top:

```java
// Clock.java
public class Clock {
    private int hour;
    private int minute;
    private int second;

    // tick() method changes the value of hour,
    // minute, and second

    // void means nothing is returned
    public void tick() {
        this.second += 1;

        if (this.second >= 60) {
            this.minute += 1;
            this.second = 0;
        }

        if (this.minute >= 60) {
            this.hour += 1;
            this.minute = 0;
        }

        if (this.hour >= 24) {
            this.hour = 0;
        }
    }

    public String getCurrentTime() {
        return String.format("%02d:%02d:%02d", this.hour, this.minute, this.second);
    }

    public void setHour(int hour) {
        this.hour = hour;
    }

    public void setMinute(int minute) {
        this.minute = minute;
    }

    public void setSecond(int second) {
        this.second = second;
    }

    public int getHour() {
        return this.hour;
    }

    public int getMinute() {
        return this.minute;
    }

    public int getSecond() {
        return this.second;
    }
}
```

That's certainly a lot to glance at, but what's important is knowing that the `.tick()` method is what changes the clock by the second.

## Overloading

