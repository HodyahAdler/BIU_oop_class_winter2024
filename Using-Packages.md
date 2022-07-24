
## A Few words on Java Packages

Java code is organized into **packages**. We will learn more about packages later in this class.

For now, however, note that java classes may have long names, for example, there are classes named `java.awt.Color` and `java.util.Random`.

You can use these long names (a.k.a the class' fully-qualified name):
```java

public class Example {
   public static void main(String[] args) {
      java.util.Random rand = new java.util.Random();
   }
}
```

but it might be inconvenient because that's a lot to type.

We call the part before the last period the **package name**, and the part after the last period the **last name**.

The `import` keyword tells java that, in this file, you can use only the last name of some of the classes.

```java
import java.util.Random;
```

tells java that in this file, you can use `Random` instead of `java.util.Random`.

```java
import java.util.Random;

public class Example {
   public static void main(String[] args) {
      Random rand = new Random();
   }
}
```

```java
import java.util.*;
```

Tells java that in this files, you can use the last name of every class with the package name `java.util.`, including `Random`.

It is better to not use the `*` version, because it makes it hard to understand where the names come from.

