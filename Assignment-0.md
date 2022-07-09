# Setup Assignment

The goal of this assignment is to get you through the technical requirements of the assignments of this course.
You will not be graded for this assignment. However, we strongly suggest you submit it, to verify that 
you have all prerequisite ready and you understand all submission instructions before you get into "real" assignments.  

Assignments should be submitted through the [Submission System](http://submit.cs.biu.ac.il).


## Working Environment Guide

We have prepared a detailed [technical guide](https://docs.google.com/document/d/1L5ryhn8VO73n19YRb6iNMXXYl0vDo0m84YIN3_Rd3Ao/edit?usp=sharing) 
(from previous years) with general things you should probably know, especially when working from Windows. Have a look.
In addition, Ayal Klein (TA of the course in 2020) prepared very useful [videos](https://www.youtube.com/watch?v=Sr8iEftSWfI&list=PLtQ-fYSVAsxrvXVIKUtriFwz53Pn1N1m-&index=1)
 in hebrew, explaining how to install JDK 13 (we will use JDK 17) and some other stuff. 


## Install Java

Install the Java Development Kit (JDK). 
This year, we will use the most recent Java version, which is Java 17.
Download the installation file from [here](https://www.oracle.com/java/technologies/downloads/) and run it.

## Make sure that your installation is working

Open up a terminal window, and issue the following commands:

```
java -version

javac -version
```

You should see output similar to:
```
java version "17.0.2" 2022-01-18 LTS
Java(TM) SE Runtime Environment (build 17.0.2+8-LTS-86)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.2+8-LTS-86, mixed mode, sharing)
```

and
```
javac 17.0.2
```

## Write, Compile and Run a simple program

1. Create a file named `HelloWorld.java`
2. Enter the following content:
```java
/**
 * @author Someone
 */
public class HelloWorld {
   /**
    * This is a traditional demo class to demonstrate how to
    *  write, build and run a Java program.
    *
    * @param args command line arguments.
    */
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hi");
        }
    }
}
```
3. Compile the program using: `javac HelloWorld.java`
4. Verify that a corresponding `HelloWorld.class` file is created.
5. Run the compiled program: `java HelloWorld`

You should see the output
```
Hi
Hi
Hi
Hi
Hi
```


## Install Ant 

Please follow [[Installing Ant]] for installing ant on your computer. 



## Make sure you understand the Submission Instructions

Please read the general [[Submission Instructions]] for the course. 
You must fully understand and follow these instructions for every assignment in this course.
Now is a good time to carefully read it and to follow the instructions provided there. 
