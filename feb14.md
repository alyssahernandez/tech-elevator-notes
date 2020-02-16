# Module 1 Review Day!

Questions:

1) When to use .getBalance() instead of balance?
   1) Example: In the bank account

### Abstract vs Interface

Abstract: Abstract methods are more of a design preference.
- You will have these methods.
- You will have these properties.

You need to declare a Class as abstract to create abstract methods within it. That is called the *method signature.*

If you have an abstract class and abstract methods, you must have a concrete (not abstract) child class that @Overrides the abstract methods. Someone down the line must instantiate the method.

### Superclass vs Subclass

Do not duplicate code unless you have to. For example, an Animal Class could be a Superclass that has a walking method in it. It may say that the animal walks on four legs. That would be true for a horse subclass, a dog subclass, a cat subclass, etc. There's no reason to rewrite that method for the three specific animals, so you can just leave it in the Superclass and make sure to *extend* it in the child classes.

### Access Modifiers - When to Use Them

`Public`: All classes in the package have access to the method/variable.

`Private`: 

### Getters & Setters - When & Why

What's the difference between using `.getBalance()` in a subclass, versus just `balance`, a variable also stored in the superclass? 

You *always* want to use the getter (`.getBalance` in this case). Our getter methods are not that complex right now, but let's say later down the road our getter method will need to reach out to a database to retrieve the value. Everyone, every method/class that needs to retrieve that variable, will know that the getter method will return it. It's a default. Just using `balance` may return something that hasn't been updated/sent to the database, so it could return the wrong value.

All properties should have getters and setters as appropriate. Let's say you have a bank customer class and a bank teller class. In that case, and for any class that has a name variable, you want it to be private. You don't want any other class to be able to change the name outside of using the specific get/set method that you allow.


### Writing Tests

We are writing tests using the jUnit tests we're familiar with. We will run these tests, just like the other test files we used before in the first few weeks of the course. The bar should return green if all of it is true. Nothing will show in the console.

*src/main/java*

```java
class MathStuff {
    public boolean IsEven(int x) {
        return x % 2 == 0;
    }
}
```

The above is a simple test returning true if a number is even and false if a number is odd.

*src/test/java*

```java
class MathStuffTest() {

    static final int EVEN_NUMBER = 2;
    static final int ODD_NUMBER = 3;
    // you want to avoid magic numbers

    @Test
    public void HappyPath() {

        // arrange
        MathStuff happy = new MathStuff();
        // created an object of the MathStuff Class

        // act
        boolean actualOdd = happy.IsEven(ODD_NUMBER);
        // testing an actual odd number example (false)
        boolean actualEven = happy.IsEven(EVEN_NUMBER);
        // testing an actual even number (true)

        // assert - assert that this is true or false
        // did the thing do what i expected it to do
        assertFalse("Odd numbers should be false", actualOdd);
        // the expected value above is false
        // odd numbers should return false for the IsEven method

        assertTrue("Even numbers should be true", actualEven);
        // the expected value above should return true
        // an even number should return true for the IsEven method

    }
}
```

The above code is known as the *happy path.* That's the most basic test you can do. You should test the basics before doing anything complex.

Another @Test example for an absolute value:

```java
public int absoluteValue(int x) {
    return x < 0 ? x * -1 : x;
    // if x is negative, return the positive (* -1)
    // otherwise, return the already positive value (absolute)
}
```

Now for the test file:

```java
@Test
public void happyAbsoluteTest() {

    // ***ARRANGE***
    MathStuff ms = new MathStuff();

    // ***ACT***
    int actualPos = ms.absoluteValue(1);
    // this will call the absoluteValue method and
    // attempt to return the absolute value of 1
    // it will create a new int, stored in var actualPos
    int actualNeg = ms.absoluteValue(-1);
    // this will call the same method and attempt to
    // return the absolute val of -1, which is 1, and
    // it *should* return positive 1 and store it in
    // the var actualNeg

    // ***ASSERT***
    assertEqual("Positive value should stay positive", 1, actualPos);
    // the expected value will be defined either in the line
    // such as the "1" above, or declared as a constant above
    // followed by the value you're checking for, which we is stored
    // in the variable we defined in the ***ACT*** section using
    // the method we're testing
    assertEqual("Negative value should become positive", 1, actualNeg);
}
```

### Declarations

```java
MathStuff ms = new MathStuff();

int actualPos = ms.absoluteValue(1);
```

Order of declarations:
1) type
2) variable name
3) equals sign
4) instantiation OR object expression
   1) instantiation = new
   2) object expression = ms - methods that we can apply to that object
5) another type
   1) same class
   2) interface followed by something that implements it
   3) superclass followed by subclass
      1) (shouldn't be the other way around)
      2) superclass: restaurants, subclass hipcityveg
         1) all hipcityveg's are restaurants
      3) superclass: hipcityveg, subclass restaurants
         1) NOT all restaurants are hipcityveg's (BAD)
6) constructor arguments

Every time you declare something, you MUST have all of the above.

```java
= Object(...) // reference instance, insert parameters
// or just () to create a new object

= Object.Method(...) // void type
// method acting on the object

= Object.Property // type
// int x = ms.totalVal
```