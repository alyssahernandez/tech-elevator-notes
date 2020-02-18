## File I/O - Input & Exceptions

Make sure you can:
- describe concept of *exception handling*
- implement basic `try`/`catch` structures
- use the `java.io` library and classes
- describe a character stream
- use a `try (with_resources) { Block }`
- handle i/o exceptions and recover from them
- describe uses for file i/o

### Exception Handling

- Try to execute code
- Catch the problem, if there is one, and do something else

```java
try {
    // do some work.. but someone deleted file
} catch {
    // bad things are happening...
    // i meant to do that, but do something else
}
```

The catch feature can also work like a method feature, where you pass in parameters. There's an `Exception` Superclass with hundreds of different methods that apply to different objects (pseudocode):

```java
} catch (Exception ex) { // one, for example
    if (ex.equals(FileNotFoundException)) {
        Prompt user to try again.
    }
} catch (Exception e) { // general ex if
    // you can't think of one

}
```

Note: You can't loop a `try`/`catch` from the `catch` part. You can't say, "catch this and then try again." Instead, you can place the `try`/`catch` in an infinite `for` loop, a `do-while` loop, a `while` loop, etc. There are several different ways to do it.

Stack trace: Invaluable to a developer, but not something you ever want to show a user. It lists a *lot* of info that you don't want the user to see.

Note: Try to fix exceptions with logic first.

### Creating Custom Exceptions

You can create your own `Exception`s if there aren't any in the `Exception` class that fit your needs. You would need to create it outside of the `public static void main` method.

This is where the `throw new ` keywords come into play. Usually, you would say something like `throw new whateverCustomException` at the beginning of a line, followed by the name of your custom method.

### java.io Library and Classes

`java.io` contains hundreds of classes and methods that let you work with imported files.

You *can* load entire files in your program, but depending on the size of the file, it could take several days. Instead, you can import a file `String`. That means you import it bit by bit. For example, with Netflix, if you have to load your entire TV series to watch one episode, it would take up a lot of memory.

This is where the idea of a *buffer* comes in. It takes a few things from the stream (that's why there are *streaming* services), bit by bit, and imports them for use.

You need to import the `java.io.File;` library. You also want to make sure you import the `java.io.FileNotFoundException;`.

```java
file inputFile getInputFileFromUser();

File inputFile = new File(path);
// i think this is where you input the file...
// path is a String var created somewhere above

try (Scanner fileScanner = new Scanner (inputFile)) {
    // some code
}

// some more code

private static File getInputFileFromUser()  {

}
```

To input a file, take input from the user using the `Scanner` and then paste the file path into the console. Example:

```java
C:\data\routingnumbers.txt
```

### Try with Resources

You can try with resources. You try to execute a block of code using a resource, such as a `Scanner` file. What that does is keep you from having a wide open connection to a file in case something goes wrong. If the try block throws an `Exception`, or if it fully executes, it will close the resource and clear it from memory.

```java
try (Scanner fileScanner = new Scanner(inputFile)) {
    // some code to execute using the Scanner
}
```

In the above, we are using the `Scanner` object to execute the code within the `try` statement. The whole point of putting in the `try` block is so that is closes when you're done using it.

Note: It's important the resource/buffer/stream objects can use the `AutoClosable` method from the `Closeable` interface. Most do. You'll know if it doesn't by the red line in the IDE.

### Finally

The `finally` function is added to the end of a `try`/`catch` block. It is optional, and ensures that the code within it is executed every time the `try`/`catch` block is completed--errors or not.

```java
try {
    // some code
} catch (some exception) {
    // some code
} finally {
    // some code
}
```

### Forcing an Exception

For example, let's say we want to purposefully throw a `NullPointerException`, which is something we've created below the `main` method. Notice that the first statement in the `try` block is just a `println`, so it isn't going to throw an error. However, notice that the following line says `throw new` followed by our custom `Exception` name:

```java
try
{
    System.out.println("try block");
 
    throw new NullPointerException("Null occurred");
} 
catch (Exception e) 
{
    System.out.println("catch block");
} 
finally
{
    System.out.println("finally block");
}
```

The `NullPointerException` will `throw` because you told it to, so it will execute and then execude the code in the `catch` block. Finally, the `finally` block will execute, because it always does.