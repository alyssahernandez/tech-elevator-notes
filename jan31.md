# Command Line Programs

So far, we've learned how to code some basic logic that could be used to run an application, but we haven't learned how to actually make an application run. We can run tests, but we want to make an application that actually interacts with the user and takes input and gives output.

Command line programs take input, does some work, and generates output. Every application is like that, but command line programs are programs that run within the command line. There are no windows, buttons, programs sliders, etc. 

How do we get user input? We need to tell the computer to aside some storage to take this information and do something with it. In order to be able to do this, we have to use a framework called the *standard I/O stream.* In Wikipedia's words: Standard Streams are pre-connected input and output communication channels between a computer program and its environment when it begins execution. In other words: A stream is a flow of information in and out. It's a common term we'll hear a lot. 

The first few programs we're writing are just basic input/output. The programs will run within the command line and accept user input via the keyboard. THe output will, of course, also be within the command line.

*Remember: Integers and arrays are objects.*

The *import* command says that we want to import a package from a library. Example:

```java
import java.util.Scanner
```

The above is just a package we need to take user input. That's all we need to know for now.

## System.out.println vs System.out.print

We're familiar the the command `System.out.println();`. We know that it takes whatever is inside the parentheses and prints it out on its own line. After that, however, the next thing that's printed on the screen--if anyway--is printed on the line after that. If we want to stay on the same line, which is especially useful if we want the user to input something on the same line, we would use `System.out.print();`. This keeps the cursor on the same line. Here's an example:
 
```java
String firstName = "Alyssa";
String lastName = "Hernandez";

System.out.println(firstName);
System.out.println(lastName);
```

The output would be "Alyssa" on one line and "Hernandez" on the next line.

```java
String firstName = "Alyssa";
String lastName = "Hernandez";

System.out.print(firstName);
System.out.print(lastName);
```

The output would be "Alyssa Hernandez" on the same line.

## A Few Basic Key Word Reviews

`main` is the entry point command for every application. That's where you tell the computer to run the program.

Classes are uppercase. A `String` is an array of a characters. `String`s are built-in classes within the framework; it comes with the program. They are *reference* types.

*Control characters* are printed characters that the user doesn't see. Example, if you have `System.out.print(\n);` it will print on the screen as a line break. The user doesn't see `\n`. They only see that the cursor/words/etc are on a new line. Here are a few very common control characters:
- `\t` insert a tab in the text at this point.
- `\b` insert a backspace in the text at this point.
- `\n` insert a newline in the text at this point.
- `\r` insert a carriage return in the text at this point.
- `\f` insert a formfeed in the text at this point.
- `\'` insert a single quote character in the text at this point.
- `\"` insert a double quote character in the text at this point.
- `\\` onsert a backslash character in the text at this point.

## Simple Input from a User - Words

`System.out.println(x)`: We are telling the *system* to *output* a *printed line* of the value of `x`. What is the value of `x` and how can it interact with the user?

After importing the Scanner package, we can use the `input.nextLine()` function to accept user input when we call it.

```java
public static void main(String[] args) {
    Scanner input = new Scanner(System.in);

    System.out.print("Please type your name: ");
    String userName = input.nextLine();
    
    System.out.println("Your name is: ");
    System.out.print(x); // this would print on the same line
}
```

The above code would print a line asking the users name, and allow the user to input it; let's say "Alyssa" The next line would output "Your name is: Alyssa". Maybe we want to add a period onto the end of that. Just like we can concatenate strings, we can do the same thing with user input:

```java
System.out.print("Please type your name: ");
String userName = input.nextLine();

userName.concat(" ."); // this adds a period after the name
```

Back to the *stack* and the *heap*: Primitive data types are stored in the *stack*. They have addresses that point them to their location in the heap. If `int a = 2` and `int b = 2`, they could either have the same location and same address (because it's the same value), OR they could have different locations and different addresses.

## Comparing Strings for Equality

Up until this point, we've been checking to see if two variables are equal using the logical operator `==`. With strings, however, it is much better to use:

```java
String x = "Hello";
String y = "Hello";

if(x.equals(y)) { // this is the function you should use! 
    System.out.println("They are equal!");
}
```

## Splitting User Input to Multiple Lines

Let's say you have the user input their first *and* last name, but all in one input field. How can we separate it? We can take the user input and create an array.

```java
System.out.print("Please type your first and last name: ");
String fullName = input.nextLine(); // user types "Alyssa Hernandez"

String[] splitName = fullName.split(" "); // split at every space

System.out.println("Your first name is: " + splitName[0]);
System.out.println("Your last name is: " + splitName[1]);
}
```

The output in the terminal would be:

```java
Your first name is: Alyssa
Your last name is: Hernandez
```

## Respond Differently to Different Input

```java
public static void main(String[] args) {
    
    Scanner input = new Scanner(System.in);

    System.out.println("Do you drink coffee?");
    String isCoffeeDrinker = input.nextLine();

    if (isCoffeeDrinker.equals("yes") {
        System.out.println("Yum!");
    } else if (isCoffeeDrinker.equals("no")) {
        System.out.println("You're missing out!");
    } else {
        System.out.println("Please say yes or no.");
    }
}
```

## Interrupt User Input with Output

Let's say you ask a user to list their five favorite foods, separated by spaces. If they type something you love, you interrupt and say "I love it too!" If it's something you hate, you interrupt and say "Yuck!" Here's what that would look like:

```java
public static void main(String[] args) { // main class

    Scanner input = new Scanner(System.in);
    // necessary package

    System.out.println("List your five favorite foods: ");

    String userFavoriteFoods = input.nextLine();
    // takes input

    String[] listFoods = userFavoriteFoods.split(" ");
    // wherever there's a space, the foods are split up
    // into an array, each in their own space

    System.out.println("Here are your favorite foods: ");
        // first thing that prints after a user hits enter
        // once they've typed in their five favorite foods

    for (i = 0; i < listFoods.length; i++>) {

        listFoods[i] = listFoods[i] + likeFood(listFoods[i]) 
        + hateFood(listFoods[i]);
        // (split on a new line for clarification)
        // below, we've created two methods: one for liking
        // a certain food and one for hating a certain food
        // that the user may or may not input.

        // remember that in the above line of code, the list
        // of foods that the user input was split up into an
        // array. by setting i to 0 in the for loop, we set 
        // listFoods[i] equal to the first food item listed.
        // notice that after each + sign, we have a method
        // name that we created below the main method. the
        // parentheses next to the method name are the
        // parameters that we're passing into the method.
        // check out the method logic below.


        System.out.println(listFoods[i]);  
        // this will print each food item individually
        // on a new line for each item 

    }
}

public static String likeFood(String food) {
    return (food.equals("tofu")? " LOVE" : "");
    // this is a return statement because in the for
    // loop above, this method is already going to be
    // printed with another command below it.
    
    // remember the x.equals(y) function will check
    // if x is equal to y. the parameter passed when
    // this method is called is listFoods[i], so
    // this method will only apply to one word. the
    // one word that is passed into this method will
    // be referred to as food within this method only.

    // basically, when the for loop executes, this method
    // is called for every iteration of the loop:
    // listFoods[i]. that means it will check, every time
    // the loop is executed, if the word equals "tofu". if
    // so, it will print out "LOVE" next to it.
}

public static String hateFood(String food) {
    return(food.equals("mushrooms")? " YUCK" : "");
    // notice that the parameter food is the same name
    // as the parameter for the likeFood method. that's
    // completely fine because the parameter is within
    // the method, so it doesn't overlap.

    // if a user inputs "mushrooms", this method will
    // print out "YUCK" next to it.
}
```

To make it easier to read, and for review, here is the same block of code written without the comments:

```java
public static void main(String[] args) {

    Scanner input = new Scanner(System.in);

    System.out.println("List your five favorite foods: ");

    String userFavoriteFoods = input.nextLine();

    String[] listFoods = userFavoriteFoods.split(" ");

    System.out.println("Here are your favorite foods: ");

    for (i = 0; i < listFoods.length; i++>) {

        listFoods[i] = listFoods[i] + likeFood(listFoods[i]) 
        + hateFood(listFoods[i]);
    
        System.out.println(listFoods[i]);  
    }
}

public static String likeFood(String food) {
    return (food.equals("tofu")? " LOVE" : "");
}

public static String hateFood(String food) {
    return(food.equals("mushrooms")? " YUCK" : "");
}
```

## Parsing Strings to Integers

What if you ask for the user input as a string, but you want to use the data as an integer if it is an integer? You can't tell a framework to strictly accept numbers. That's what parsing is for. Parsing is basically taking an input, such as a string, and turning it into an integer.

All primitive data types have a `parse()` method that will accept a string and convert it to another data type. Let's say you want to ask a user for their age:

```java
System.out.print("What is your age? ");

String ageString = input.nextLine();
// user inputs age; ex 22

int ageInt = Integer.parseInt(ageString);
// string input converted to integer

System.out.println("Your age is " + ageInt);
// will print: Your age is 22.
```