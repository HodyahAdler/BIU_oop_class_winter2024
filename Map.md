A `Mapping` or a `Dictionary` is a very common and useful abstraction when designing and writing programs.

The Mapping allows you to create a mapping from keys to values, and efficient retrieval of values based on their keys.  Maps are usually implemented using data-structures like binary search trees or hash-maps (which you will learn about in the data-structures course) but can also be implemented using linked lists -- they will just be less efficient.

The interface for a Map allows you to:
* associate a key with a value
* check if a key exists in the map
* get the value associated with a specific key.

In the Java collections library, the `[Map](http://docs.oracle.com/javase/7/docs/api/java/util/Map.html)` interface represents a mapping, and it has several implementations, among them "HashMap" and "TreeMap" (the first is implemented using a hash-based data structure, and the second is implemented using a tree-based data structure).

You create and use a mapping as follows:
```java
// You need the following imports
import java.util.Map;
import java.util.TreeMap;
// ...

// Now pretend we are inside a code block:
// The following lines will create a mapping where the keys are of type
// String and the values are of type Point.
Map<String, Point> m = new TreeMap<String, Point>();
// This is how we associate values with keys.
m.put("p1", new Point(1, 1));
m.put("p2", new Point(2, 3));
// This is how we check if a key exists, and get
// the value associated with a key.
if (m.containsKey("p1")) {
   Point p = m.get("p1");
}
Point p2 = m.get("baaa"); // p2 is null.
m.isEmpty(); // returns false
m.clear();
m.isEmpty(); // returns true
```

(see the [documentation](http://docs.oracle.com/javase/7/docs/api/java/util/Map.html) for other available methods).

**Valid Keys**
The `TreeMap` and `HashMap` implementations both rely on the `.equals()` method of the keys being correct. In addition, `TreeMap` relies on the keys being comparable (according to the `Comparable` interface or a supplied `Comparator`), and `HashMap` relies on a correctly implemented `.hashCode()`. Builtin Java objects such as `String`, `Integer`, `Double` are all comparable and have proper `hashCode`, but if you want to use your own objects as keys you must make sure to implement these methods yourself.

**Valid Values**
Any java Object can be a value. This means that primitive types are **not** valid values,
so the mapping must be created with one of the corresponding object types, for example:
```java
Map<String, double> m = new HashMap<String, double>(); // Impossible!
Map<String, Double> m = new HashMap<String, Double>(); // Good.
```

However, once created you can pass the primitive type to `.put()` and return it from `.get()`,
it will be automagically converted to and from the object type.
```java
m.put("a",1.0);  // this works
double d = m.get("a"); // this works
double e = m.get("b"); // NullPointerException!
```
