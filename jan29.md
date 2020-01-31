# Expressions, Statements, Blocks, and Logical Branching

## Expressions?

Expression: syntax made up of *multiple* variable operators with concatenation which evaluates to a single value.

Statements vs expressions: Statements are full lines of code / have a semicolon and *do* something. Expressions can stand alone or be part of a statement, but they yield a result:
  - `int x = 5; // expression`
  - `System.out.println(x); // statement`
  - `a * 2  // expression`
  - `b + (a * 2) // expression`
  - `System.out.println(a * b); // statement and expression`
  
Three types of expressions:
- produce a value
- assign a variable
  - `int daysInWeek = 7;`
- no result but might have a side effect
  - increment operators
  - method invocation

## Defining Methods
  
*Signature:* a method name with its parameters. You can have the same method name but different parameters, which means they have different signatures:

```java
getArea (int theLength, int theWidth) { // signature 1
    int area = theLength * theWidth;
    System.out.println("My area is: " + area);
}

getArea (int length, int width) { // signature 2
    int area = length * width;
    return area;
}
```

Example method declarations:

`public static void main`: the core method of the program that must contain every other method // syntax cannot be changed
- `public:` access modifier; you can call this method outside of the class you are currently in
- `static:` return type
- `void:` java may return something that other programs cannot read, so it doesn't make sense to have anything else
- `main:` fixed; called by the JVM as en entry point for an app // all of the other

`public int getArea:` typical format of a method declaration you might see
- `public:` modifier (can also be `private`, more later)
- `int`: type of value returned; int in this class (ex: 2)
- `getArea`: method name

`public double returnADouble`:
- `public`: publicly accessible
- `double`: returns a double (ex: 2.5)
- `returnADouble`: method name

## Conditional Code

*Conditional code:* a path of code that executes only if certain conditions are true.
- if a user has not logged in, show login page
- if the password is wrong, show reset screen

## Comparison Operators

These *always* evaluate to a `boolean` value of `true` or `false`.

- `==`: equal to
- `!=`: not equal to
- `>`: greater than
- `>=`: greater than or equal to
- `<`: less than
- `<=`: less than or equal to

## Logical Operators

Comparison operators are limited in that they can't evaluate variables of different types. This is where logical operators come into play.

- `&&`: AND / true if both are true
- `!`: NOT / true if NOT true
- `||`: OR / true if either are true
- `^`: XOR / exclusive or / true if only ONE is true

## If Statements & Booleans

`if` statements are very common to use. If condition x is true, execute this code. If it's not true, execute this other code.

`boolean` expressions: either `true` or `false`. The default value is `false`.

Combining a `boolean` with an `if` statement:

```java
if (isLightSwitchOn == true) {
    return "Light switch is on."
}
```

NOTE: Technically, you don't *need* to put the `==` operator, as stating `if (isLightSwitchOn) {` is asking the same thing.

### Give dessert if 75+% dinner eaten:

```java
public boolean giveDessert(int pct dinnerEaten) {
    boolean result = false; // default is false! still initialize

    if (pct dinnerEaten >= 75) {
        return true; // now result is true!
    } 

    return result; // if pct < 75, auto returns false
}
```

Another way to write it (without `boolean result`):

```java
public boolean giveDessert(int pct dinnerEaten) {
    if (pct dinnerEaten >= 75) {
        return true; // now result is true!
    } else {
        return false; // executes if pct < 75;
    }
}
```

The simplest way to write it:

```java
public boolean giveDessert(int pct dinnerEaten) {
    if (pct dinnerEaten >= 75){
        return true;
    }
}
```

A way to write it without an `if` statement:

```java
public boolean giveDessert(int pct dinnerEaten) {
    return (pct dinnerEaten >= 75);
}
```

The above doesn't have a `return true` statement because the return type *is* a boolean, *and* there is a conditional operator, which always returns a `boolean`.

### Return a string, "Fizzy" if soda is equal to 1. Return an empty string otherwise:

```java
public String sodaFizzy(int number) {
    if (number == 1) {
        return "Fizzy";
    } else {
        return "";
    }
}
```

Simpler way to write it without needing the `else` statement:

```java
public String sodaFizzy(int number) {
    String result = ""; // now default is empty string

    if (number == 3) {
        result = "Fizzy";
    }

    return result; // must return if declaring ahead of time!
}
```

## Ternary Operators

### Return "pie" if 75+% of dinner was eaten. Otherwise, return "beans."

```java
public String dinnerEaten(int pct dinnerEaten){
    if (pct dinnerEaten >= 75) {
        return "Pie";
    } else {
        return "Beans"
    }
}
```

Rather than writing out `if`/`else` statements, you could use a ternary operator: `if`/`then`/`else`:

```java
public String dinnerEaten(int pct DinnerEaten) {
    return (pct dinnerEaten >= 75 ? "Pie" : "Beans");
    /*
    don't forget that if you're not specifying what to return
    within the block of code: the return type MUST match the
    return type declared in the method declaration.
    */
}
```

The above is super compact. You *need* to add `?` after the `if` statement part, almost like asking a question. You *need* to add `:` after the `then` statement part to provide a second option.

NOTE: It is NOT a good practice to use ternary operators, especially nested ones.