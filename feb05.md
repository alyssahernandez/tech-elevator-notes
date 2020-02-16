## Non-Linear/Associative Collections

A `List`, `Stack` and `Queue` are called *linear data structures* because when output, they are output in a certain sequential order depending on the type.

There are such things are *non-linear data structures*, meaning when output, they are **not** in the order you put them in. They do not guarantee ordering.

Regardless of whether its linear or non-linear, you'll probably be using them to do the following:

- adding or inserting items in a particular spot
- removing or deleting an item from the collection
- searching for a particular value
- updating the value

Some of the data types perform operations more efficiently than others. For example, a  `Queue` will always insert items at the end and remove them from the front. It's more efficient at doing so than the others; it doesn't matter the size of the data--1 or 100,000 items--it will always take the same amount of time.

## Sets

A *set* is a collection that is used to store unique values. Unlike the `List`, `Stack` and `Queue` collections, you can't have two values that are identical in a set.

```java
Set<String>
```

## Add an Object to a Set / .add()

Similar to lists, we use the `.add()` method:

```java
Set<String> uniqueNames = new HashSet<>();
uniqueNames.add("David");
uniqueNames.add("Scott");
uniqueNames.add("Adam");
uniqueNames.add("Jane");
uniqueNames.add("Scott");
uniqueNames.add("David");
uniqueNames.add("Usman");

System.out.println(uniqueNames);
```

Remember that a `Set` cannot have duplicate values, so the above code would output: `Adam, Jane, Scott, David, Usman`. It outputs in order, but if there are duplicates, it only outputs the most recent instance of the item added.

## Removing an Item from a Set / .remove()

This is pretty basic. Going off the previous example of code:

```java
uniquenames.remove("Usman");
System.out.println(uniqueNames);
```

The above code would output: `Adam, Jane, Scott, David`.

## Clearing a Set Entirely / .clear()

Using the `uniqueNames` example, let's say we want to completely clear the list to start over. We can use the `.clear()` method:

```java
uniqueNames.clear();
```

The above code output would be blank.

## Checking if a Set Contains a Certain List Item / .contains()

This is pretty basic as well. Within the parentheses, we pass what we'd like to check for:

```java
uniqueNames.contains("Alyssa");
```

The above output would return a `boolean` of `true` if the set contains "Alyssa".

## Checking if a Set is Empty / .isEmpty()

Again, similar to the `.contains()` method:

```java
uniqueNames.isEmpty();
```

The above code would return a `boolean` of `true` if the `Set` is empty.

## .iterator() / NEED CLARIFICATION ***

## Maps

Maps offer a distinct advantage over using arrays and lists, both of which take longer to search through.

With a `Map`, there are *keys* and *values*, both of which are unique. They're kind of similar to how arrays use indexes. With arrays, however, the indexes are just plain numbers that access the single value. With a `Map`, you can assign a `key` to a `value`. Here's an example below:

```java
Map<String, Boolean> people = new HashMap<String, Boolean>();
people.put("Luke", true);
people.put("Han", false);
people.put("Chewbacca", false);
people.put("Yoda", true);
people.put("Leia", false);
```

In the code above, we're assigning the `key` as a person, and the `value` as to whether or not they're a jedi. Maps are really useful for pairing data into a collection.

Each are considered a `Set`, so they follow the same rules as a set. All of the keys in a map are considered a `Set`, and all of the values within a `Map` are considered a `Set`.

It's important to note that map keys must be unique, but the values do not have to be unique (as demonstrated in the example above).

## Importing a Map

To use a `Map` in a program, you must import the methods from the java library. However, that is not enough. As we know, when we create a new instance of a class--an object--we have to use the keyword `new`. That's the case with `Map` as well.

`java.util.Map` is an *interface*. This is what we import at the top of the java file.

`java.util.HashMap` is *class*; it's not an object--it's not real--until we instantiate it. That's why we use `new HashMap` when creating the object.

## Creating a Map

```java
Map<Type Key, Type Value> nameToZip = new HashMap<Type Key, Type Value>();
```

Every time you create a `Map`, you must initiate it with `HashMap`.

- `Map<Type Key, Type Value>` is the interface type and its parameters
- `nameToZip` is the name of the interface object
- `new` is instantiating a new `Map` object
- `HashMap` is, again, required
- `<Type, Type>();` are the parameters you would pass when creating the `Map` object

Note in the example above that it *is* possible for the `key` and `value` to be of different data types. Our jedi example from above would look like this:

```java
Map<String, Boolean> people = new HashMap<String, Boolean>();
```

## HashMap

You'll see that in the declaration there is something called the `HaspMap`. Hash codes/HashSets are created internally. When you create a map and declare the two types, each key+value is assigned a unique hash code. A hash code looks something like "AD75AC". It is something generated by the computer, so in a way, it's kind of random.

## Data Ordering in a Map

With a `Set`, we saw that it would output in the order the items were added, but if there were any duplicates, it would only output the last instance of the duplicate.

With a `Map`, the `Set` rules apply in terms of not having duplicates, but outputting/printing the keys+values is not the same. Since maps are assigned hash codes that are randomized, when you print the set of keys+values, it prints in the order of the hash codes. That means that the output is *not* in the order that you added them.

## Adding Values to a Map / .put()

```java
Map<Type, Type> nameToZip = new HashMap<Type, Type>();

nameToZip.put("Ben", "19096");
nameToZip.put("Alyssa", "17268");
nameToZip.put("Elizabeth", "15213");
```

## Getting/Printing Map Values / Looping Through Them / .get()

With arrays, we can access the values using indexes. With maps, we access the values with the unique keys for each value.

Of course, we know there is the `System.out.println()` method. Using it in a map would look something like this:

```java
System.out.println(nameToZip.get("Ben"));
System.out.println(nameToZip.get("Alyssa"));
System.out.println(nameToZip.get("Elizabeth"));
```

However, typing out all of those `println` statements can be redundant. Instead, we can use a `for each` loop using a `Set`.

Again, to use a `Set`, we must declare, instantiate and initialize it:

```java
Set<String> keys = nameToZip.keySet();

for (String name : keys) {
    System.out.println("name" + " lives in " + nameToZip.get(name));
}
```

For every `name` String that we've created in the `for each` loop, we can now do some work on it.

## Removing Items from a Map / .remove()

The `key` and `value` of a `Map` go together. If you remove the `Key`, the `value` is removed as well:

```java
Map<Type, Type> nameToZip = new HashMap<Type, Type>();

nameToZip.put("Ben", "19096");
nameToZip.put("Alyssa", "17268");
nameToZip.put("Elizabeth", "15213");

nametoZip.remove("Alyssa");

System.out.println(nameToZip);
```

The above code would output the values of `Ben` and `Elizabeth`, but not necessarily in that order.

## Making Sure a Key Exists / .containsKey()

We know there are a few methods to check the contents of collections, but this one is specifically for maps:

```java
Map<String, Boolean> people = new HashMap<String, Boolean>(); 

// ... map is populated

if (!people.containsKey("Luke")) { 
    people.put("Luke", true);
}
```

## Looping Through a Map Set / .Entry / .entrySet()

To iterate through a `for each` loop with a `Map` collection, there's a special way we must write it:

```java
Map<String, Boolean> people = new HashMap<String, Boolean>(); 

// ... Map is populated with people

for(Map.Entry<String, Boolean> person : people.entrySet()) {
    if (person.getValue()) {
        System.out.println(person.getKey() + " is a Jedi.");
    } else {
        System.out.println(person.getKey() + " is not a Jedi.");
    }
}
```

In the above code, you'll see the `Map` declaration on top. We have the collection type, data types, object name, etc. Below that, we have a `for each` loop, which we've seen before.

Because `Map` types contain both a `key` and a `value`, and because we're not iterating it via `i`, we simply need to state the two data types, `String` and `Boolean`.

`person` is the name of the *item* you're looking for, which can be whatever name you want.

Most importantly, however, is the use of the `.Entry` and `.entrySet()` methods in the declaration of the `for each` loop.

It's also important to note the use of the `.getValue()` method. That method is what it sounds like: it's getting/retrieving the value of the `value` in a key+value pair in a `Map` collection. Because it's a `for each` loop, simply stating `person.getValue()` is enough to mean that for each item/pair in the list, we are going to retrieve and return the value of the `key` represented by the `person` variable.

## Measuring How Our Programs Behave

- how much memory it uses
- how much storage it uses
- how long it takes to run

All engineering is tradeoffs. If I care about clock time, I might use more memory. In the real world, reading hundreds of emails can take hours. Rather than use up our own clock time, we can pay someone to check our emails. The tradeoff would be money for time.

In coding, the tradeoffs are usually *speed* and *memory*. Thankfully, today, computers have a lot of memory and the processors are very fast.

## Big O Notation

It's really important to recognize how efficient your program will run; at least, your algorithm. An interviewer will want you to know how efficient your program is.

***REMEMBER: Premature optimization is the root of all evil.***

It's much better to do things *right* and then go back and worry about efficiency, if needed. Create a working solution! Going off of that, the Big O Notation is a measure of how long an algorithm takes to run. We can use it to compare the efficiencies of different solutions to a problem. We can talk about it in terms of speed and memory.

The Big O express the runtime in *how quickly it grows relative to the input, as the input gets arbitrarily large.*

## Measuring the Runtime of an Algorithm

This is kind of tricky. It's difficult (maybe impossible) to have an accurate measurement of the runtime. This is because different computers have different processors, and processors determine how fast the computer is.

However, we can calculate the *relative* speed in terms of *how quickly the runtime grows.*

## Runtime Relative to Input

If we were able to express the runtime directly, we could use seconds. However, since we can't do that, it has to be relative to the input; how quickly the runtime grows instead of how the direct runtime.

With the Big O, we use the *size of input*, which obviously varies, so we simply use `n`.

## Notation

The following list contains the ways we represent the efficiency. It is in order from fastest to slowest. It's also important to note that the Big O always refers to the worst case scenario, meaning the absolute longest it could take.

- O(1) : constant time / always takes the same amount of time, regardless of the data size
  - addition, multiplication, boolean, operations, hashSet, Map
  - ex: `return array[0] % 2 == 0;`
- O(n) : linear time / searches every element for a value
  - searching sorted data for a specific value
  - ex: `for(int i = 0; i < array.length; i++) {`
  - worst case scenario: not in the array/last value
  - best case scenario: first item
  - single loops over collections, String, indexOf
  - time it takes is linearly proportional to the amount of data it has to sort through
- O(n^2) : quadratic time / nested loops
  - multiple loops / loops within loops
  - a `for` loop within a `for` loop looking for duplicates
  - you take the first index in the first loop and then check it against every other index in the second group
  - even a 10-length array would iterate 100 times in the worst-case scenario
  - with more nested loops, you can get up to n^3, n^4 and so on
- O(n log n) : 
  - sorting arbitrary things

Honestly, just memorize the above. The **most** important one to memorize is `O(n log n)`. This is usually the one that comes up in interviews.

For the bulk of our programming, though, most of what we're doing can be expressed as `O(n)`.

Note: There are many other notations beyond the list above, but they are crazy exponential: `O(n^3)`, `O(2^n)`, etc. However, they aren't really practical because they aren't commercially practical to solve a problem if you're getting up to this speed. We simply don't typically have a processor fast enough. The biggest thing we have in practical terms is `O(n^2)`.

## Measuring How Long it Takes to Check if a Char is in a String

It can take a while to find if an individual `char` is within a `String`, especially if the `char` is at the very end of the `String`. That would be considered a worst possible case. If a `List` is five items long, the worst case would be if the `char` is the last item in the `List`. That means it would take five operations to complete it.

Index of a string is `O(n)`.

## Measuring the Time it Takes to Add Integers

This is always `O(1)` because it's just simple addition; something a computer can quickly do.

## Checking to See if Two Chars Exist Next to Each Other // CLARIFY****

To do this, we have to use a loop:

```java
chars[] chars = ... // array of chars

for (int i = 0; i < chars.length - 1; i++) {
    if (chars[i] == 'x' && chars[i + 1] == 'x') {
        return true;
    }
}
```

The worst case scenario for this loop would be if `x` is not in the array at all. The second worst case would be if the pair is the last two `chars` in the array.

The time on this loop is `O(n)`.

Alternatively, looking something up in an array with a known index is `O(1)`.

A comparison operator is also `O(1)`.

Let's take a look again:

```java
chars[] chars = ... // array of chars

for (int i = 0; i < chars.length - 1; i++) {
// i++ is O(1)
    if (chars[i] == 'x' && chars[i + 1] == 'x') {
    // chars[i] == 'x' is O(1)
    // chars[i + 1] == 'x' is O(1)
        return true;
        // return statements are O(1)
    }
}

// altogether, there are 4 O(1)
// n * (1 + 1 + 1 + 1) + 1
// 4n + 1 = O(n)
// ignore the 4n and 1, so it ends up just being n
```

Even though all of the operations in the `for` loop are `O(1)`, altogether the `for` loop is `O(n)`.

## Speed of Putting a List of Things in Order CLARIFY*****

The fastest you could do this would be `O(n log n)`.

## More Example Problems

```java
public int getMax (int[], nums) {
    Arrays.sort(nums); // O(n log n)
    int maxVal = Integer.MIN_VALUE; // O(1)

    for (int i = 0; i < nums.length; i++) { // O(n)
        maxValue = nums[i] > maxVal ? nums[i] : maxValue;
        // 5 -> O(1)
    }

    return maxVal; // O(1)
}
```

In the above code, we're sorting arbitrary data

```java
nlogn + 1 + n5 + 1
// we ignore the small stuff (1, n5, 1)
// the biggest thing is nlogn
```

The Big O of the above method is `O(n log n)`.

If, within the `for` loop, we put another `Arrays.sort(nums)`, then there would be another `O(n log n)` that we would be executing the `sort` method for each iteration of the loop. It would then be `O(n^2)`.

The above method could be written in a simpler way. The `.sort` method we see already sorts the numbers in increasing order, so there's no need to go through the for loop to get the `maxVal` because we know it's the last index after sorting it:

```java
public int getMax (int[], nums) {
    Arrays.sort(nums); // O(n log n)
    int maxVal = Integer.MIN_VALUE; // O(1)

    return num.length > 0 ? nums.[nums.length - 1] : Integer.MIN_VALUE;
}
```

## Big O Interview Questions!!!!

Trivia: "How fast can you sort a list? `O(n log n)`

What's an example of an `O(n log n) operation: looping over an array.

Likely. they will give you a problem and you answer how long it would take (in Big O notation).

"If I give you an array, how quickly can you find something in it?" To be smart, you can say: "Is it sorted or not sorted?" With sorted arrays, you can find it much faster.

Interviewers will drop some code on you and ask you to measure the complexity of it.

It's important to note that 90% of the time, you will not use this in your job. It will be another person's job to check for efficiency. 