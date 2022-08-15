## Logical Expressions, Nand and Nor Logic and Logical Simplification

In this assignment we will put aside our game for a little while, and delve instead
into the magical world of logics. We will implement a system that can represent
nested logical expressions that include variables, evaluate their values
for specific variable assignments, convert them, and simplify the results.

In doing so we will work in a recursive framework, see some more examples of
polymorphism, and practice the use of inheritance and class hierarchies for
sharing common code.

We supply this [build.xml](https://github.com/HodyahAdler/-BIUoop2022summer/blob/main/ass4/build.xml) for the assignment.

## Part 1 -- Logical Expressions

### Introduction:

Our goal is to represent logical expressions such as:

`~((T & (x | y))^x)`

Where `T` is a value of "True", the `~`,`|`,`&`,`^`, symbols denotes the "not","or","and" and "xor" operators respectively,  and `x` and `y` are variables.

Note that this somewhat complicated expression is composed of atomic expressions which are either binary or unary, arranged in a tree structure. The expression itself is the root of the tree.

The unary expressions are:

* `Var("x")` indicating that `x` is a variable.
* `Not(x)` indicating the negation of the value of x.

The binary expressions are:

* `Or(x,y)` indicating the "or" of `x, y`.
* `And(x,y)` indicating the "and" of `x, y`.
* `Xor(x,y)` indicating the "xor" of `x, y`.

- This link might be helpful: [Wikipedia page for Boolean operations in Hebrew](https://he.wikipedia.org/wiki/%D7%A4%D7%A2%D7%95%D7%9C%D7%94_%D7%91%D7%95%D7%9C%D7%99%D7%90%D7%A0%D7%99%D7%AA)

We also have a `Val(F)` expression indicating the logical value "False".

Assuming we represent each of the atomic expressions as a Class of the same name that takes its arguments in the constructor, we can create the expression above
in java using:

```java
Expression e = new Not(
                  new Xor(
                     new And(
                        new Val(true),
                        new Or(
                           new Var("x"),
                           new Var("y")
                        )
                     ),
                     new Var("x")
                  )
               );
```

The tree is given below:

![expression tree](https://github.com/HodyahAdler/-BIUoop2022summer/blob/main/ass4/tree.svg)

Note that all the nodes in the tree are expressions (according to the `Expression` interface):

![expression tree](https://github.com/HodyahAdler/-BIUoop2022summer/blob/main/ass4/etree.svg)

Similarly, we could represent `(x & y) ^ T` as:

```java
Expression e2 = new Xor(new And(new Var("x"), new Var("y")), new Val(true));
```

Once we have an expression, we would like to be able to:

* **Get a nice and readable string representation:**
   ```java
   String s = e2.toString();
   System.out.println(s);
   ```
   Should print ```((x & y) ^ T)```

* **Ask about the variables in the expression:** (this example uses [generics](Generics))
   ```java
   List<String> vars = e2.getVariables();
   for (String v : vars) {
      System.out.println(v);
   }   
   ```
   Should print
   ```
   x
   y
   ```

* **Assign values to variables:**
   ```java
   Expression e3 = e2.assign("y", e2);
   System.out.println(e3);
   // ((x & ((x & y) ^ T)) ^ T)
   e3 = e3.assign("x", new Val(false));
   System.out.println(e3);
   // ((F & ((F & y) ^ T)) ^ T)
   ```

   In the first `assign` the variable `y` was assigned the Expression `(x & y) ^ T`, while in the
   second `assign` the variable `x` was assigned the Expression `False`.

* **Evaluate its value for a given variable assignment to values:** (this example uses a [mapping](Map))
   ```java
   Map<String, Boolean> assignment = new TreeMap<>();
   assignment.put("x", true);
   assignment.put("y", false);
   Boolean value = e2.evaluate(assignment);
   System.out.println("The result is: " + value);
   ```
   Should print `The result is: true`

   In this last example, we make use of the [Map](Map) interface for mapping keys to values. We created a map called `assignment` mapping the value `"x"` to `True` and the value
   `"y"` to `False`, and then evaluated the expression `e2` with these values, resulting in (True And False) Xor True, which is True.

### What you need to implement

In the first part,we begin with a simple interface called `Expression`:

(this interface uses [generics](Generics) and [map](Map))

```java
public interface Expression {
   // Evaluate the expression using the variable values provided
   // in the assignment, and return the result. If the expression
   // contains a variable which is not in the assignment, an exception
   // is thrown. 
   Boolean evaluate(Map<String, Boolean> assignment) throws Exception;

   // A convenience method. Like the `evaluate(assignment)` method above,
   // but uses an empty assignment.
   Boolean evaluate() throws Exception;

   // Returns a list of the variables in the expression.
   List<String> getVariables();

   // Returns a nice string representation of the expression.
   String toString();

   // Returns a new expression in which all occurrences of the variable
   // var are replaced with the provided expression (Does not modify the
   // current expression).
   Expression assign(String var, Expression expression)
}
```

You should write following classes, each of them corresponding to an atomic expression, and each of them should implement the Expression interface.
* `Val`, `Var` -- representing truth values and variables.
* Unary expressions: `Not`.
* Binary expressions: `And`, `Or`, `Xor`, `Nand`, `Nor`, `Xnor`.

The string representations are as follows:
* And(x,y) = (x & y)
* Or(x,y) = (x | y)
* Xor(x,y) = (x ^ y)
* Nand(x,y) = (x A y)
* Nor(x,y) = (x V y)
* Xnor(x,y) = (x # y)
* Not(x) = ~(x)


**You have to use the exact same symbols, since the assignment will be checked with an automatic test as well.**

`Val` should have a constructor accepting a `Boolean`.
`Var` should have a constructor accepting a `String`.
The unary expressions should have a constructor accepting an `Expression`.
The binary expressions should have a constructor accepting two `Expression`s. 

The implementation will make heavy use of recursion. For example, in order to evaluate an expression, you need to first evaluate its sub-expressions and then apply some function to the results, with the base cases being the evaluation of the `Var` and `Val` expressions.

**Class Hierarchy**

You should also implement the abstract base classes `BaseExpression`, `UnaryExpression` and `BinaryExpression`, and have the different expression classes inherit from them, according to the
following hierarchy:

![UML class diagram](https://github.com/HodyahAdler/-BIUoop2022summer/blob/main/ass4/uml.svg)

Try to put shared code in the base classes instead of the leaf classes. Example for candidate methods
that can be in the base classes are `Boolean evaluate()` and `List<String> getVariables()`.
You can add whatever non-public methods you want to the class hierarchy in order to help with code sharing.

### How to approach this

You need to implement many classes. One way to approach this would be to start with only a subset of the classes, for example only `Var`, `Val`, `And`, `Or` and `Not`. Once these are working, see if you can move some of the shared code to the base classes `UnaryExpression`, `BinaryExpression` and `BaseExpression`.
Then, go ahead and implement the rest of the expression classes.

### Test your code

Create a class with a `main` method that creates some nested expressions (for example `Expression e` as defined above) and then prints them, evaluates them, and asks for the variables in them).

## Part 2 -- Nandify and Norify

We can now create expressions, get their variables, and evaluate them with given variable assignments.

In this part we will also convert them to logically equal expressions according to this logic:

* [Wikipedia page for Nand Logic]( https://en.wikipedia.org/wiki/NAND_logic)
* [Wikipedia page for Nor Logic]( https://en.wikipedia.org/wiki/NOR_logic)

Add the following methods to the Expression interface:
```java
public interface Expression {
   // ... as before
   
   // Returns the expression tree resulting from converting all the operations to the logical Nand operation.
   Expression nandify();
   // Returns the expression tree resulting from converting all the operations to the logical Nor operation.
   Expression norify();
}
``` 

For example:
```java
   Expression e = new Xor(new Var("x"), new Var("y"));
   System.out.println(e.nandify());
   System.out.println(e.norify());
// should print:
// ((x A (x A y)) A (y A (x A y)))
// (((x V x) V (y V y)) V (x V y))
```

## Part 3 -- Simplification

Logical expression can be quite messy and contain many "redundant" parts.
For example:

```java
Expression e = new Xor(new And(new Var("x"), new Val(false)), new Or(new Var("y"), new Val(false)));
System.out.println(e);
// the result is:
// ((x & F) ^ (y | F))
```

This is correct, but can be really hard to read. We need to "simplify" the expression to make it
more friendly to humans.

We will add another method to the Expression interface. This method
will return a new expression which is a simplified version of the current one.

```java
public interface Expression {
   // ... as before

   // Returned a simplified version of the current expression.
   Expression simplify();
}
```

Example usage:
```java
Expression e = new Xor(new And(new Var("x"), new Val(false)), new Or(new Var("y"), new Val(false)));
System.out.println(e);
// the result is:
// ((x & F) ^ (y | F))
System.out.println(e.simplify());
// the result is:
// (y)


```

You need to support the following simplifications:


* x & 1 = x
* x & 0 = 0
* x & x = x
* x | 1 = 1
* x | 0 = x
* x | x = x
* x ^ 1 = ~(x)
* x ^ 0 = x
* x ^ x = 0
* x A 1 = ~(x)
* x A 0 = 1
* x A x = ~(x)
* x V 1 = 0
* x V 0 = ~(x)
* x V x = ~(x)
* x # x = 1

* an expression without variables evaluates to its result. `((T & T) | F) ^ T => F`.

Note that X here stands for **any** expression, not just a variable.

These should be recursive, so that, for example: `And((Xnor(x, x),y)) => y`.

## What to submit:

Your code should include at least the following classes, interfaces and abstract classes:
`Val`, `Var`, `And`, `Or`, `Xor`, `Nand`, `Nor`, `Xnor`, `Not`.
`Expression`, `BaseExpression`, `BinaryExpression`, `UnaryExpression`.

You should also include a class called `ExpressionsTest` including a `main` method that
will:

1. Create an expression with at least three variables.
2. Print the expression.
3. Print the value of the expression with an assignment to every variable. 
4. Print the Nandified version of the expression.
5. Print the Norified version of the expression.
6. Print the simplified version of the expression.

Each printing should be performed on its own line, do not add extra text, and do not add spaces between the lines.


**String representation rules**
* Truth values are a single capital letter: `T`, `F`
* Spaces and parenthesis in the binary expressions &, |, ^, A, V, #: `(x & y)`, `(x | y)`, `(x ^ y)`, `(x A y)`, `(x V y)`, `(x # y)`
* Parenthesis (but no spaces) in ~: `~(x)` (and have double parenthesis if they come from the inner expression)

## Notes

* You are not allowed to use downcasting.  
* You are not allowed to use the function `instanceof`.
* The assignment will be checked **automatically**, please submit it with correct printing format, 
  otherwise you'll get 0. 