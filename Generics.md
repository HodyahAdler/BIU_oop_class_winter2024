Java collection classes can be parameterized by a type, through the use of generics.
We will learn more about generics later in the class.
But you do not need to know much about generics in order to use them, so here is an example.
```java
import java.util.List;
import java.util.LinkedList;
public class C {
  public static void main(String[] args) {
    // This creates a LinkedList containing only Strings.
    List<String> l = new LinkedList<String>();
    // Let's add some elements:
    l.add("ABC");
    l.add("DEF");
    // Since we declared the type upon construction, we can now
    // get elements of type string without casting.
    String s = l.get(1);
    // And we cannot add non-Strings
    l.add(new java.util.Random()); // This will fail at complile time.
    l.add(new C()); // This will fail at complile time.
  }
}
```