# More File I/O: Review Input & Output

## Stuff to Import Before You Start

```java
import java.io.File;
import java.util.Scanner;
import java.io.IOException;
import java.io.PrintWriter;
```

## Reading Files

### Asking the User Which File to Open

Just like we use the `Scanner` class to read input from a user, we use it to read input from a resource:

```java
Scanner userInput = new Scanner(System.in);
    
    System.out.print("Enter the path of a file or directory >: ");
    String path = userInput.nextLine();
```

Opening a file from user input requires that you know the path to the file you want to read.

### Opening the File Yourself in the Code

```java
Scanner existingFileName = new Scanner(fileType);
```

### Importance of Using the Try/Catch Method

It's recommended that you open/use files in try/catch methods. You want to make sure the file is only open for as long as you need to use it. That prevents it from locking up the file and disallowing other applications to use it. It's also just generally a waste of memory.

Here's an example:

```java
try (Scanner fileName = new Scanner(dataType)) {
    ...
} catch (FileNotFoundException ex) {
    System.err.println("The file does not exist.");
}
```

The above code will close the file (well, do nothing) if it doesn't exist. It's also important to use a try/catch method when *writing* to files as well. Although this will be explained later, here's an example:

```java
try (PrintWriter dataOutput = new PrintWriter(dataFile)) {
    ...
} catch (FileNotFoundException ex) {
    System.err.println("Can not open the file for writing.");
}
```

### See if a File/Directory/Resource Exists

```java
System.out.println("File exists? : " + f.exists());
```

You can take it one step further and do something like:

```java
if (f.exists()) {
    if (f.isFile()) {
	    System.out.println("Type is: File");
    } else {
        System.out.println("This is another type.");
    }
} else {
	    System.out.println(f.getAbsolutePath() + " Does not exist!");
}
```

### To see what type of resource we're importing, you can do a few checks:

```java
if(f.isDirectory()) {
    System.out.println("Type is: Directory");
    // folder in which file lives
} else if (f.isFile()) {
    // checks if it's a file...
    System.out.println("Type is: File");
```

### Return File Name

```java
System.out.println("File name is: " + f.getName());
```

### Return Absolute Path

```java
System.out.println("Absolute path is: " 
        + f.getAbsolutePath());
// returns something like C:\data\textFileName.txt
```

### Check the Size of a File (byte size)

```java
System.out.print("size: " + f.length());
// will just a print a number, but it's byte
```

### Return a Collection of Children from a Directory

```java
System.out.println("size: " + f.list());
// if you input: C:\Windows, it will return
// a hash code because it's outputting Strings
// in Eclipse, you can right-click: watch and
// go to the expressions to expand the list of
// all of the children of the directory
```

### Create a New Directory

Let's create a directory, but let's check some conditions first to make sure it doesn't already exist.

```java
File newDirectory = new File(path);
// remember: path is the name of the Scanner input
// we're asking a user to input a file name

if (newDirectory.exists()) {
    System.out.println("Sorry, " + 
        newDirectory.getAbsolutePath() + " already exists!");
    System.exit(100);
    // System.exit(someNumber); terminates the running JVM
    // any number passed that *isn't* usually means that
    // something bad has happened
} else {
    if (newDirectory.mkdir());
    // this is similar to the git bash command!
        System.out.println("New directory created as: "
                + newDirectory.getAbsolutePath());
   `} else {
        System.out.println("Unable to create directory: " +
                newDirectory.getName());
        System.exit(100);
    )
}
```

### Create a New File

We've created a directory; let's add a file to it.

```java
System.out.println("Enter the name of the new file >: ");
String fileName = userInput.nextLine();
File newFile = new File(fileName);
```

Doing the above method *does* work... If you put in the entire file path. Instead, there's a method for that:

```java
System.out.println("Enter the name of the new file >: ");

String fileName = userInput.nextLine();
File newFile = new File(newDirectory, fileName);
// notice how we now have the newDirectory name first
// and we created the directory above. it doesn't *have*
// to be a new directory... it can be an existing one

newFile.createNewFile();
// checks for existence of file; if it doesn't exist
// it creates it. note that simply creating a File
// object doesn't do the trick!!!
```

### Check if You Have Access to Read or Write to a File

You know that some files are read-only. Here's how to check for that in code without having to open the file:

```java
fileName.canWrite();
// this will return a boolean - useful for if statements
```

Similarly, there's a method to see if you can read the file:

```java
fileName.canRead();
// also returns a boolean - useful for if statements
```

## Writing to Files

### Have a User Write To the File

```java
String.out.println("Please enter a message to write to the file >: ");

String message = userInput.nextLine();

try (PrintWriter writer = new PrintWriter(newFile)) {
// this is the buffer; the try method ensures that
// the file will be closed once you're done using it

    writer.println(message);
}
```

### Writing to the File Yourself Within the Code

This is pretty similar to the example above, but instead of having the user input text, we just use the `println` method:

```java
try (PrintWriter dataOutput = new PrintWriter(dataFile)) {
    dataOutput.println("Writing the first line of the file");
    dataOutput.println("Writing the second line of the file");
} catch (FileNotFoundException ex) {
    System.err.println("Can not open the file for writing.");
}
```

### Making Sure You Don't Override a File (IGNORE)

So, writing to a file is pretty simple, but you want to be careful to not override it. This requires setting the file to be **appended to.** To ensure of that, we need to use `FileOutputStream`:

```java
try (PrintWriter dataOutput = new PrintWriter(
// standard PrinterWriter, which we need to write to any files
    new FileOutputStream(
        dataFile, true // This true sets the file to be appended
    )
)) {
```

Not really sure about this one...

## Data Streams

*Stream:*  a data structure that reads data as a series of ordered bytes. With text data streams, each byte represents a character in a large string.

Think of it like an assembly line; you don't process everything at once. Rather, you slowly go down the line.

The computer doesn't care where the data stream comes from. It can come from a file, user input, your hard drive, etc.

### Simplified Flow of Stream:

- data
  - `Scanner` and `PrintWriter` send data to input processing
- input processing
- buffer (bucket slang)
  - "fills" with data
  - "pours" the data into the buffer
  - "fills" up with more data
  - that way we don't get everything at once
- consuming code
  - rendering...
  - netflix...

