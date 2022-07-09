As for all assignments, we provide you the [build.xml](code/ass1/build.xml) for ant. 

## Java for C programmers

In this assignment you will write a few simple java programs in a procedural (**not** Object Oriented) style.
The purpose of this assignment is to refresh your memory on the *Intro to CS* course material, and get you up to speed with the basic java syntax.
For each task, you can assume that the argument is correct.

### Task 1: Factorial

Write a program for calculating the factorial function. Your code should reside in a file named `Factorial.java`. The program will read a number `n` from the commandline, and will then calculate `n!` twice, once using a recursive definition, and once using an iterative procedure, and print out the result.

For example, invocation of your program should look like this:
```bash
> java Factorial 5
recursive: 120
iterative: 120
```

or with Ant
```bash
> ant run1 -Dargs="5"
recursive: 120
iterative: 120
```

(lines starting with `>` are what you write to the shell, other lines are expected output).

Your `main(String[] args)` method will read the input number from the `args` array and convert it from a string to an integer.  It will then call the two methods:
```java
public static long factorialIter(long n);
public static long factorialRecursive(long n);
```
and print the results.

Note: you can convert a string to an integer using the following code:
```
int n = Integer.parseInt("123");
```

### Task 2: Arrays

Write a program called DescribeNumbers that gets a list of numbers in the commandline, and prints their minimum, maximum, and average values.

```bash
> java DescribeNumbers 12 2 3 -9 8
min: -9
max: 12
avg: 3.2
```

or with Ant
```bash
> ant run2 -Dargs="12 2 3 -9 8"
min: -9
max: 12
avg: 3.2
```



Your program must define and use (at least) the following functions:
```java
public static int[] stringsToInts(String[] numbers);
public static int min(int[] numbers);
public static int max(int[] numbers);
public static float avg(int[] numbers);
```

### Task 3: Sorting

Write a program called Sort that will take a sorting order followed by a list of numbers from the commandline and print out the sorted list of numbers:

```bash
> java Sort asc 12 2 3 -9 8 
-9 2 3 8 12
> java Sort desc 12 2 3 -9 8 
12 8 3 2 -9
```
or with ant: 
```bash
> ant run3 -Dargs="asc 12 2 3 -9 8" 
-9 2 3 8 12
> java run3 -Dargs= "desc 12 2 3 -9 8" 
12 8 3 2 -9
```


here, `asc` means ascending order and `desc` means descending order.

**Note:** string comparison is performed using the the `.equals()` method of String:
```java
String s = "hello";
if (s.equals("hello")) {
   // do something
} 
if (s.equals("goodbye")) {
   // do something else
}
```

For sorting, you can use the [Bubble Sort](http://en.wikipedia.org/wiki/Bubble_sort) algorithm.

## Submission Instructions

**Important:** The first row of each file should include your ID and your name as follows:
``// 012345678 David Cohen`` (not in the Javadoc)

It's not allowed to import any JAVA class. 

Submit through the [Submission System](http://submit.cs.biu.ac.il). 

Please follow the general [[Submission Instructions]] for the course.

Make sure your code follows the [[CodingStyle]].