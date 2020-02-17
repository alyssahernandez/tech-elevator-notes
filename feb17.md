# Review / Test Driven Development (TDD)

With a static method, you do not need an instance of the class to call the method. Example:

```java
public static Class Hello() {

    public String printHello() {
        System.out.println("Hello");
    }
}

Hello helloInstance = new Hello();

helloInstance.printHello(); // this is unnecessary

Hello.printHello(); // this is the way to do it
```

### Unit Testing

- after coding
- developer defined in context
  - can skew results
- time/project burn down

### TDD

- before coding
- outside of coding development paradigm
  - not locked into the thought process of how something is supposed to behave while you're designing a test on how it's supposed to stay
- saves time on the backend and in agile methodology
  - it might seem like it takes longer, but if you write a test *after* you code, you can fall into a cycle of going back and forth between coding and testing
- you're coding *to* the test
- you kind of know the problems ahead of time
- it gives you a direction
  - you're listing all of the problems you need to solve before you write solutions
- you write the tests first. then you change the code and ~usually~ don't have to rewrite the tests.
  - you don't have to worry about the tests
  - you're free to be a developer and just code away

### TDD Life Cycle

- write the test
- code to test
- test the code
- repeat if needed

### Coding to Test

- does the test pass?
  - yes - is it clean?
    - yes - continue coding to test
    - no - refactor
  - no - keep trying - code to test again
- repeat

### Refactor: How and When (Makes Code Cleaner)

1) eliminate duplicate code
2) extract methods from your code
3) simplify complex operations
   1) nesting ternaries within ternaries... not good
   2) maybe better to nest some things within a loop
   3) or maybe you need a whole conversion class that has these methods
   4) some things could end up being 400+ lines when you could just write them in a separate method
4) identify opportunities to objectify

### General Strategy for TDD

1) create a list of tests
   1) write the potential problems to solve
2) write just enough to pass the tests
   1) don't want to over-complicate it
   2) (even if it means hard coding it)
   3) a *lot* of coders when they start out write too much code
3) test each change/iteration

### Recursion

Calling a method inside itself. It's tricky... use it with care. Do NOT first set out to create recursion. It's kind of like a for-loop.