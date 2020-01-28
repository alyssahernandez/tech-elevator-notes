# Java Basics

## Terminology

*IDE*: integrated development environment (for java: *eclipse*)
- allows you to edit files, create projects & launch websites & data servers

*JVM*: java virtual machine
- basically turns our code into a machine language that can be read by multiple machines (phones, pc, mac, etc)
- binary code
- there is a loss of performance in terms of speed but chips are faster now

*byte code*: intermediate translation between java and machine language
- strips down meaningless white spaces & comments
- translates commands to open windows, processing instructions, etc
- compacted & readable by the JVM
- you won't be able to read it

Steps:
1) write filename.java using a text editor like vscode
2) use eclipse, an IDE to compile the code to get byte code
3) byte code is interpreted by the JVM to machine language

## Example of a Java Class

- *public*: who has access to the class
- *class*: self-contained collection of behaviors
- HelloWorld: name of class
- *args*: arguments/parameters, like cd/fruits (fruits is param) 
```java
public class HelloWorld {
    public static void main(String[] args) {
        // print Hello World to the console
        System.out.println("Hello World");
    }
}
```

## Binary

1 or 0 // signal or no signal

because there are only two possible values, 1 and 0, you can only do 2^# when counting, and you go left or right:
- a byte is 8 digits long: 2^7, 2^6, 2^5, ... 2^0
  - 128 - 64 - 32 - 16 - 8 - 4 - 2 - 1
  - the number 126 would be 11111111

## Variables

*variable*: basically a container
- computers need to know what type of var so they can allocate memory to it, either the *stack* or the *heap*
  - *stack*: one area of memory that the pc allocates as to vars that are being used; last in is first out

Declaring a variable: 

```java
int myAge = 23;
```

## Variable Data Types

- `boolean` true or false // 1 or 0 (bit)
- `byte` -128 to 127 // 128 slots but one needs to rep +/-
- `char` 'a', \u0000, \uffff // represents a single character
- `int` whole numbers
- `float` -3.4x10^38 to 3.4x10^38 // can use fractions
- `double` similar to float, but with float you lose precision and that can cause errors. doubles are much longer so the chance of precision errors is significantly lower
- `long` large whole numbers

*string:* a whole bunch of characters strung together 

## Operators

- `+` adds two operands
- `-` subtracts two operands
- `*` multiplies two operands
- `/` divides two data types but rounds down (15/2 = 7)
  - 15 and 7 are integers; they don't have decimals
- `%` gives you the remainder of a division (15/2 = 1)

## Type Conversion

What if you do 15/2 and you don't want the answer of 7? You want 7.5? That's where data type conversion comes in.

Integers to floats:

```java
int myInt = 15;
float myFloat = myInt/2; // wrong, neither 15 or 2 is a float
float myFloat = (float)myInt/2; // right, 15 is 15.0 here
```

Simplifying floats:

```java
float myFloat = 2000.0000; // if you don't want to write 0s,
float myFloat = 2000f; // represents a float of up to 7 decimal places
```

Making doubles easier to read:

```java
double myDouble = 483674386.4234; // hard to read, no commas
double myDouble = 483_674_386.4234; // doesn't print _, easier to read in code
```

## Storing Money in a System Debate

Let's say you have $10.25, $3.10 and $1.05. If you add all of them, you get $14.40. That basically looks like an integer divided by 100.

However, with stocks, you don't have just two digits. You might have 0.0000035 share in a stock and with the integer method, that translates to 0 shares.

(predictive stock app; automatically sells all of your shares when the price is high, based on market predictions and relative price, and then automatically buys them again when it's predictively/relatively low)