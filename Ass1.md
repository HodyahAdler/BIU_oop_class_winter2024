As for all assignments, we provide you the [build.xml](https://github.com/HodyahAdler/-BIUoop2022summer/blob/main/ass1/build.xml) for ant.

Java for C programmers
In this assignment you will write a few simple java programs in a procedural (not Object Oriented) style. The purpose of this assignment is to refresh your memory on the Intro to CS course material, and get you up to speed with the basic java syntax. For each task, you can assume that the argument is correct.

Task 1: reverse number
Given a 32-bit signed integer, reverse digits of an integer.
Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

For example, the invocation of your program should look like this:

`> java ReverseNumber 5678
reverse number: 8765`

or with Ant

`> ant run1 -Dargs="5678"
reverse number: 8765`

(lines starting with > are what you write to the shell, other lines are expected output).

Your main(String[] args) method will read the input number from the args array and convert it from a string to an integer. It will then call the two methods:

`public static int reverseNum(int n);`

and print the results.

Note: you can convert a string to an integer using the following code:

`int n = Integer.parseInt("123");`

Task 2: Array place
Write a program called PlaceInArray that get array of integers nums sorted in non-decreasing order, and find the starting and ending position of a given target value. If target is not found in the array, return [-1, -1].


`> java PlaceInArray 1 1 4 5 8 9 9 9 5
5 start in 3 and end in 3`

or with ant:

`> ant run3 -Dargs="1 1 4 5 8 9 9 9 5" 
5 start in 3 and end in 3`


Task 3: Arrays
Write a program called tripletOfZero that gets a list of numbers in the commandline, and prints the triplet [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

If no such triplet exists, return -1. your output array need to be order by the user input:

`> java TripletOfZero asc 12 2 -3 -9 8
the triplet is: [12, -3, -9]
> java TripletOfZero desc 12 2 -3 -9 8
the triplet is: [-9, -3, 12]`

or with Ant

> ant run2 -Dargs="asc 12 2 -3 -9 8"
the triplet is: [12, -3, -9]
> ant run2 -Dargs="desc 12 2 -3 -9 8"
the triplet is: [-9, -3, 12]`


here, asc means ascending order and desc means descending order.

Note: string comparison is performed using the the .equals() method of String:

`String s = "hello";
if (s.equals("hello")) {
   // do something
} 
if (s.equals("goodbye")) {
   // do something else
}`

Your program must define and use (at least) the following functions:

`public static int[] stringsToArray(String[] numbers);
public static int[] tripletOfZero(int[] numbers);
public static void ascTripletPrint(int[] numbers);
public static void descTripletPrint(int[] numbers);
public static boolean isAsc(String[] order);`



Submission Instructions
Important: The first row of each file should include your ID and your name as follows: // 012345678 David Cohen (not in the Javadoc)

It's not allowed to import any JAVA class.

Submit through the [Submission System](http://submit.cs.biu.ac.il/).

Please follow the general [Submission Instructions](https://github.com/HodyahAdler/-BIUoop2022summer/wiki/Submission-Instructions) for the course.

Make sure your code follows the [CodingStyle](https://github.com/HodyahAdler/-BIUoop2022summer/wiki/CodingStyle).

Make sure you have JAVADOC as expected. 