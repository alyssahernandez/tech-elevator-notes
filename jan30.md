# Arrays, Loops

*Stack*: code is executed from the top down
- organized allocated storage
- data lives here

*Heap:* contains objects that are kind of just all in a cluster
- references live here; they point to the memory addresses in the stack
  - arrays are an example of a reference type

## Declaring an array

Instead of writing a list such as this...

```java
int scout01;
int scout02;
int scout03;
int scout04;
```

You can condense it like this:

```java
int [] Scout = new int[] {
    23, 17, 1, 35
}
```

**Note**: once you declare the *lentgh* of an array and it's *type,* you cannot change it. It is immutable.

In the above example, `int` would go under *stack.* However, `scout` would exist under *heap.*
- *stack* needs to know how much storage to reserve for the object. if you say `new int[4]`, *stack* will know how much space to reserve. In this case, the array would have a *length* of *four.*
- the stack would start with `[0]` at the bottom & `[3]` at the top
- *elements:* individual types stored within the array; in the above example, the elements would be the array of integers

However, it's still a list of ints that you would have to individually reference: `Scout[0], Scout[1]` etc. That's where loops come in:

## Loops

`int scouts = Scount.length;` // output of 4

There are 4 numbers, but the positions start at 0. The array has positions of 0, 1, 2, 3.

```java
for (int x = 0; x <= Scout.length - 1; x++) {
    // above could be written as: < Scout.length

    System.out.println(Scout[x]);
    // above will print out each element in the array:
    // 23, 17, 1, 35
    // much easier than listing 4 separate println statements
}
```

In regards to *stack* and *heap,* a loop is part of a heap: it's a reference to the data in the stack.

Remember that above we declared the length of the array; 4. What if we want to reuse the code with different lengths? Use a class:

```java
public void PopulateScoutBadges (int numberOfSeats) {
    int[] Scout = new int[numberOfScouts] {
    // the scope of Scout is only within this method
        int badgeCount = System.out.println("Prompt the user for the badge count for Scout[x].");
        Scout[x] = badgeCount;
    }
}
```

You can output *or* input values of an array using a loop.

## For Loops

```java
for (<initializer; condition; iterator>) {
    <things that happen when code executes>
}
```

With a for loop, the *initializer* might be something like `i=0`. That's just declaring that whatever is in the *for* loop will execute based on the state of *i*.

The *condition* is what defines what state *i* must be in in order for the body of the for loop to execute. For example, it could be *i < someArray.length*. Maybe `someArray.length - 4`. That means that as long as *i* is less than *4*, the body of the for loop will execute.

Something has to change *i* in order for the code to decide whether or not to loop. That is called the *iterator*. The *iterator* executes after the body of the code executes (if it even does). For example, it might be a simple `i++`.

The above loop would execute four times:

```java
(psuedocode):
i = 0
i = 1
i = 2
i = 3
i = 4 // this would not execute because i is = 4,
// which is not less than the length.
```

In simple for loops like this, as long as *i* starts with *0,* the loop would execute the same number of times as the length of the loop. I would still increase to four because the iterator executes *after* the body code runs. The *condition* would then check the state of *i* and execute the body if it's true. Otherwise, it would exit the loop. Another way to make sure that the loop executes the same number of times as the array length is to do `i = 1; i <= array.Length; i++`

You don't have to use `<`. You could use any operator you want, including `=`. Here's an example of code that would print out "Hello World" five times:

```java
for (i = 1; i <= 5>; i++) {
    System.out.println("Hello World");
}
```

Here's how:

```java
i = 1; "Hello World"
i = 2; "Hello World"
i = 3; "Hello World"
i = 4; "Hello World"
i = 5; "Hello World" 
```

After the last line, *i* would increase to 6, so the condition would no longer be true and the body would not execute.

## Incrementing/Decrementing Variables

There are many different ways to increment a variable such as *i.*

In the for loop example above, you don't have to use `i++` to change the variable. You could use `i += 1`, `i += 2`, `i -= 5`, `i--`, `i = i * 2`. As you can see, there are *many* different ways to change the variable. However, make sure that is does change, or the loop will continue on forever!

## Scope of Variables

One thing to note is that variables within for loops are only visible within for loops. Inner blocks of code have access to variables declared outer blocks of code, known as the parent code, but outer blocks do not have access to inner variables. Example:

```java
int x = 0;

for (i = 0; i <= 5; i++) {
    x += 1;
    int a = x * 2;
}

System.out.println(a);
```

The above code would throw an error because *a* is declared within the for loop. The for loop is able to access *x* because it is declared outside of the for loop, so the body code within the loop is fine, but it wouldn't affect anything outside of the for loop. This is what we should do instead:

```java
int x = 0;

for (i = 0; i <= 4; i++) {
    x += 1;
    int a = x * 2;
    System.out.println(a);
}

/*
Here is what the execution would look like:
x += 0 / x = 0 / a = 0
x += 1 / x = 1 / a = 2
x += 2 / x = 3 / a = 6
x += 3 / x = 6 / a = 12
x += 4 / x = 10 / a = 20
*/
```

The output would print: *0, 2, 6, 12, 20.* After that, `i = 5` and the condition would not execute, so we would exit the for loop. Variable *a* would no longer be accessible.

**NOTE:** It's important to be able to write out for loops by hand. Most whiteboard problems involve for loops, so it's important to be able to write them out in coding interviews!!!

## Calculating Averages Using a For Loop

Let's say you have an integer array filled with 7 days' temperatures. We want to calculate the average temperate for the week. We could write it out several statements listing each variable, or we could use a simple for loop:

```java
int[] averageWeather = new int[7] { // array with 7 values
    42, 45, 30, 18, 55, 32, 25;
}

int sum = 0;

for (i = 0; i < averageWeather.length; i++) {
    sum += averageWeather[i];
}

int result = sum / averageWeather.length;
```

## Breaking Out of a Loop

Let's say you don't want to execute through the entire loop cycle. You want to *break* out of the loop once a certain condition is true, independent of the conditions set when you called the for loop.

For example, maybe you have an array of the weather for the past 7 days and you want to determine if any of the days were at or below freezing. With the for loop condition and iterator, the loop would execute through *all* of the temperatures, which may be unnecessary. It's like looking for your keys in every room of the house when you already found them.

```java
boolean isBelowFreezing = false;

int[] averageWeather = new int[7] { // array with 7 values
    42, 45, 30, 18, 55, 32, 25;
}

(for (i = 0; i < averageWeather.length; i++) {
    if (averageWeather[1] <= 32) {
        isBelowFreezing = true;
        break; // this exits loop
    }

System.out.println("Were any days at or below freezing? + )
```

The output of the above code would be: `Were any days below freezing? true`