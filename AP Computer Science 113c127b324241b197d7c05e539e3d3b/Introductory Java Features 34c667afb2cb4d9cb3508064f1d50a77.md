# Introductory Java Features

Java is the language used for the AP Computer Science Exam. It is a strongly typed, static, compiled language with a heavy focus on **Object Oriented Programming** and code structuring, making it ideal for enterprise applications.

Java compiles to bytecode, which is interpreted by the **Java Virtual Machine** (JVM). This allows Java to be run independently of platform, if they have the JVM installed.

# Packages and Classes

Java organizes its code into packages, which contains classes. Per convention, there should be one class per file. A file in a package can imported with the following code:

```java
import packagename.Classname;
```

To import all files in a package, use the following code

```java
import packagename.*;
```

Packages can contain sub-packages, which can be imported in the following manner

```java
import packagename.subpackage.subpackage.*;
```

A Java program contains one Main class, which has a main method. The main method is the entry point for your application. Methods are placed inside classes.

# Types and Identifiers

## Identifiers

An *identifiers* is a name for a variable, parameter, method, class, enum, interface, or annotation. In Java, an identifier is composed of any sequence of letters, digits, and the underscore character. Identifiers cannot start with a number. Identifiers are case sensitive, meaning `Person` and `person` are different identifiers

## Identifier Conventions

Identifiers follow certain naming conventions to create consistent and readable code. Variables and methods should be in `lowerCamelCase`. Class, enum, interface, and annotation should be in `UpperCamelCase`.

## Built-in Types

Java has 8 built-in primitive data types: `int`, `long`, `short`, `double`, `float`, `byte`, `char`, `bool`. The `int`, `long`, `short`, and `byte` types are used for storing integers in various ranges:

| Data Type | Size (bytes) | Min Value | Max Value |
| --- | --- | --- | --- |
| byte | 1 | $-2^{7}$ | $2^{7} - 1$ |
| short | 2 | $-2^{15}$ | $2^{15}-1$ |
| int | 4 | $-2^{31}$ | $2^{31}-1$ |
| long | 8 | $-2^{63}$ | $2^{63}-1$ |

The `float` and `double` types are used to store floating point numbers, in accordance of standard IEEE 754, in the following ranges. The max and min values are computed differently to integer values and are beyond the range of these notes:

| Data Type | Size (bytes) |
| --- | --- |
| float | 4 |
| double | 8 |

The `char` data type stores a single 16-bit Unicode character as an integer value.

<aside>
💡 The `boolean` data type stores a true or false value, in 8 bits, as CPUs cannot address memory smaller than a byte.

</aside>

## Declaration of Variables

Variable identifiers are introduced to a Java program with a declaration that specifies its type (or the `var` keyword can be used to let the compiler infer the type). Multiple variables of the same type can be declared on the same line

```java
int x; // single variable declaration 
int y, z; // multiple variable declaration 
```

Variables can also be initialized with a value in the declaration.

```java
double x = 1.5d; // single variable declaration 
double y = 1.75d, z = 2.25d; // multiple variable declaration 
```

When using literal numerical values, they can be suffixed with a letter to specify the type of the literal: `f` for float, `d` for double, and `L` for long.

```java
double x = 0.5d;
float y = 0.825f;
long z = 1125000L;
```

## Casting Variables

Casting is an operation on a variable which attempts to convert the variable’s value to a different type. Casts will be checked at run-time, and improper casts will result in a `ClassCastException`.

Keep in mind that integral variables cannot be assigned a floating point number — An exp;licit cast must be made.

```java
int x = (int) 45.5d; // will truncate 45.5 to 45
```

## Storage of Numbers

Integers are stored as a string of bits, following two’s complement notation. One bit, usually the first, will be the sign bit, indicating a positive or negative numbers. This is why the maximum and minimum values of integral types generally follow the equation $2^{size-1}$ , as the first bit is reserved for the sign. The range of these integral types are $-2^{size-1}$ to $2^{size-1} - 1$. The minimum value is one smaller because it does not have to store $-0$.

| Sign Bit | Bit | Bit | Bit | Bit | Bit | Bit | Bit |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | 1 | 1 | 1 | 0 | 0 | 1 |

The storage of floating points numbers are far more complex. Doubles follow the IEEE 754 64 bit floating point specification, which stores floating point numbers with the representation below. Floats are not included in the AP Java subset.

$$
sign * mantissa * 2^{exponent}
$$

Typically, for a 64 bit floating point number, 11 bits are allocated to the exponent, 52 to the mantissa, and one for the sign. 

Illegal operations can result in a `NaN` — Not a Number — and operations that create huge numbers will result in an `Infinity`.

<aside>
💡 Floats have 1 sign bit, 8 exponent bits, 23 mantissa bits
Doubles have 1 sign bit, 11 exponent bits, and 52 mantissa bits

</aside>

## Hexadecimal and Octal Numbers

A **hexadecimal number** is a number in base 16, with digits from 0-F. It is often to store binary in a more compact format. In Java they are specified with a **0x** or **0X** prefix. In the AP exam they will often be subscripted with hex (e.g. $F82_{hex}$). They are converted to binary in a similar fashion to binary numbers.

$$
\begin{align}C75F_{hex} = (C)(16^3) + (7)(16^2) + (5)(16^1) + (F)(16^0)\\= (49152) + (1792) + (80) + (15)\\=51039\end{align}
$$

An **octal number** is a number in base 8, with digits from 0-7. Similar to hexadecimal numbers, in the AP exam, it will be subscripted with oct ($132_{oct}$).

$$
\begin{align}132_{oct} = (1)(8^2) + (3)(8^1) + (2)(8^0)\\= (64) + (24) + (2)\\=90\end{align}
$$

## Final Variables

A **final variable**, identified by the keyword `final`, is used to declare a variable as a constant, whose value will not change. By convention, **final variables** are in all uppercase, with underscores as separators. 

```java
final double TAX_RATE = 12.23;
final double PI = 12.23;
```

Java’s final keyword prevents the variable from being rebound, but the internal state of the object, if it is a reference type, **can change without error**.

```java
final List<Integer> list = new ArrayList<>();

list.append(100); // This is fine

list = new ArrayList<>(); // This is NOT fine
```

Final variables do not have to be bound on declaration, it’s just that they can only be bound once

```java
final double TAX_RATE;

if (<some condition>) {
	TAX_RATE = 0.08;
}
else {
	TAX_RATE = 0.06;
}
```

# Operators

## Arithmetic Operators

| Operator | Meaning | Example |
| --- | --- | --- |
| + | Addition | 2 + x |
| - | Subtraction | x - y |
| * | Multiplication | 6 * z |
| / | Division | 10 / 2.5 |
| % | Modulus | 11 % 3 |

Java provides several arithmetic operations. They are pretty self-explanatory but there are some caveats.

- These operators can be applied to integral and decimal types together. For operations concerning both, the `int` will be coerced (automatic widening) into a `double`.
- For division where both operands are integral, the result type will be an integral type, even if the result will require decimals for accurate representation.
- The addition operator can also be used to concatenate strings (joins them together).

```java
3.0 / 4 -> 0.75
3 / 4.0 -> 0.75
(int) 3.0 / 4 -> 0
(double) 3 / 4 -> 0.75
3 / 4d -> 0.75
3 / 4 -> 0 
```

These operators follow mathematical order of operations (BEDMAS or PEMDAS). Casting will have precedence over all these operators.

## Relational Operators

| Operator | Meaning | Example |
| --- | --- | --- |
| == | Equality | if (x == 5) |
| != | Inequality | if (x != y) |
| > | Greater Than | if (x > 10) |
| < | Less Than | if (x < z + y) |
| >= | Greater Than or Equal To | if (z + 3 >= 10) |
| <= | Less Than or Equal To | if (x <= 10) |

Java provides several relational operator. These operator are often used in conditional checks, as they return booleans. They are evaluated after arithmetic operators.

```java
10 == 2 -> false
5 != 5 -> true
5 > 5 -> false
7 <= 8 -> true
```

However, relational operators also have a few caveats.

- When comparing an integral and decimal type, the `int` is coerced into a `double`.
- Relational operators should generally only be used for primitive types, as equality operators on user-defined types will check for identify (check if they are the same instance in memory) instead the values. Instead, objects should be compared with an overridden `equals` method.
- When comparing floating point values, they often cannot be directly compared using relation operator because they sometimes cannot be represented exactly in memory.

## Logical Operators

| Operator | Meaning | Example |
| --- | --- | --- |
| ! | NOT | if (!(x > 5)) |
| && | AND | if (x == 5 && y > 5) |
| || | OR | if (x != y || x != z ) |

Logical operators are applied to boolean expressions to form compound boolean expressions that evaluate to `true` or `false`.

| AND | T | F | OR | T | F | NOT |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | T | F | T | T | T | T | F |
| F | F | F | F | T | F | F | T |

Java uses short-circuit evaluation, where compound boolean expressions are broken into their constituent expressions, and evaluation stops as soon as the value of the entire expressions is known. The following expressions will never result in an `ArithmeticException` (division-by-zero error) for the second expression because the expression will stop being evaluated if `y` is 0:

```java
if (y != 0 && x / y > 90)
```

## Assignment Operators

| Operator | Example | Meaning |
| --- | --- | --- |
| = | x = 5 | Simple Assignment |
| += | x += 4 | x = x + 4 |
| -= | x -= 4 | x = x - 4 |
| *= | x *= 4 | x = x * 4 |
| /= | x /= 4 | x = x / 4 |
| %= | x %= 4 | x = x % 4 |

All the above operators, with the exception of the assignment operator, are called **compound assignment operators**. They expand to an assignment with another operator as well.

Chaining of the assignment operator is also allowed, with evaluation from left to right. This should only really be used for primitive types, as doing so with a reference type will share the same reference among the variable

```java
int x, y, z;
x = y = z = 10;
```

## Assignment Operators

| Operator | Example | Meaning |
| --- | --- | --- |
| = | x = 5 | Simple Assignment |
| += | x += 4 | x = x + 4 |
| -= | x -= 4 | x = x - 4 |
| *= | x *= 4 | x = x * 4 |
| /= | x /= 4 | x = x / 4 |
| %= | x %= 4 | x = x % 4 |

All the above operators, with the exception of the assignment operator, are called **compound assignment operators**. They expand to an assignment with another operator as well.

Chaining of the assignment operator is also allowed, with evaluation from left to right. This should only really be used for primitive types, as doing so with a reference type will share the same reference among the variable

```java
int x, y, z;
x = y = z = 10;
```

## Increment and Decrement Operators

| Operator | Example | Meaning |
| --- | --- | --- |
| ++ | x++ or ++x | Increment x by 1 |
| -- | x-- or --x | Decrement x by 1 |

The above operators are used on numerical variables to increment or decrement their value by 1. They can be used before or after the variable — prefix or postfix. However, note that they have different meanings. Prefix will increment/decrement the variable before the rest of the statement, will postfix will increment/decrement after the statement

```java
int i = 5;
System.out.println(i++); // 5
// i is now 6
```

```java
int i = 5;
System.out.println(++i); // 6
// i is now 6
```

## Operator Precedence

| Precedence (highest to lowest) | Operators |
| --- | --- |
| 1 | !, ++, -- |
| 2 | *, /, % |
| 3 | +, - |
| 4 | <, >, <=, >= |
| 5 | ==, != |
| 6 | && |
| 7 | || |
| 8 | =, +=, -=, *=, /=, %= |

Operator precedence is the order in which expressions are evaluated. Operators with the same level of precedence are evaluated from left to right, except for rows 1 **(Unary Operators)** and 8 **(Assignment Operators)** where the order is right to left.

```java
System.out.println(5 + 3 < 6 * 2 - 1);
System.out.println(8 < 11);
System.out.println(true);
```

# Input and Output

## Input

Input is **NOT PART** of the AP Java Subset, as there are too many ways to provide input to a program. In the AP exam, questions that require input will do so in the following manner:

```java
double x = ***call to a method that reads a floating-point number
// OR***
double x = IO.readDouble();
```

## Output

Testing of output on the AP exam will be **restricted to `System.out.println` and `System.out.print`.**

`System.out` is an object in the System class that allows output to be displayed in the console. The `println` method outputs an item onto the console, then goes to a new line. `print`, on the other hand, outputs an item onto the console, and **does not** go the the next line. The item printed can be a string, number, or a boolean. When printing user defined objects, their `[toString](Some%20Standard%20Classes%20213a7f76d2674a2aa35a19ead780de38.md)` method will be implicitly called. 

```java
// Prints:
// **Hotdog**
System.out.print("Hot");
System.out.print("dog");

// Prints
// **Hot
// dog**
System.out.println("Hot");
System.out.println("dog");

// Prints
**// 11**
System.out.println(7 + 4);

// Prints
**// true**
System.out.println(7 + 4 == 11);

int x = 28;
// Prints
**// The value of x is 28**
System.out.println("The value of x is " + x);
```

## Escape Sequence

An **escape sequence** is a backslash followed by a single character. It is used to print special characters that cannot normally be printed in a string. The most commonly used ones are highlighted in the below, with the top 3 being used in the AP exam.

| Escape Sequence | Meaning |
| --- | --- |
| \n | Newline |
| \" | Double Quote |
| \\ | Backslash |
| \t | Tab |

Below are some examples of escape sequences:

```java
// Prints
**// Welcome to
// a new line**
System.out.println("Welcome to**\n**a new line")

// Prints
**// "I'm gonna make him an offer he can't refuse"
// - The Godfather**
System.out.println("**\"**I'm gonna make him an offer he can't refuse**\"\n**- The Godfather")
```

# Control Structures

Control structures are the mechanism by which you make the statements of a program run in a non-sequential order. There are 2 general types: **Branching** and **Iteration**.

## Branching

Branching allows code to be run if certain conditions are true to run code in a non-sequential matter. 

### If Statement

The **`if statement`** will only execute statements if the boolean expression evaluates to true. If it is false, control passes immediately to the next statement following the `**if statement**`.

```java
if (**<boolean-expression>**) {
	**statements**
}
```

An if statement can be used without braces if there is only one statement to execute, However, this can lead to [dangling else statements](Introductory%20Java%20Features%2034c667afb2cb4d9cb3508064f1d50a77.md).

### If … Else Statement

The **`if...else statement`** will execute statements in the if block if the boolean expression evaluates to true. If it is false, it will execute the statements in the else block.

```java
if (**<boolean-expression>**) {
	**statements**
}
else {
	**statements**
}
```

### Nested If Statement

Several `if statements` can be nested to created more complex branching

```java
if (**<boolean-expression-1>**) {
	if (**<boolean-expression-2>) {
		statements;
	}
}
// Equal to**
if (**<boolean-expression-1> && <boolean-expression-2>**) {
	**statements;
}**
```

However, beware of a dangling else. When an if is used without braces, an else is paired to the closest `if statement`. In the below code, entering a 7 will result in an output of `7 is not positive`

```java
int n = IO.readInt(); //read user input
if (n > 0)
	if (n % 2 == 0)
		System.out.println(n);

else
	System.out.println(n + " is not positive");
```

### Else If Statements

```java
if (<boolean-condition>) {
	**statements**
} 
else if (<boolean-condition>) {
	**statements**
}
**...**
else {
	**statements**
}
```

An else if statement is used to run statements if the condition is true and the preceding if condition(s) is false. It can be paired with an else statement as well. 

```java
double grade = **// read a double from user input**
if (grade == 100) 
	System.out.println("A+");
else if (grade >= 90) 
	System.out.println("A");
else if (grade >= 80) 
	System.out.println("B");
else if (grade >= 70) 
	System.out.println("C");
else if (grade >= 60) 
	System.out.println("D");
else 
	System.out.println("F")
```

## Iteration

Java has three different control structures that allow the computer to perform iterative
tasks: the `for loop`, `while loop`, and `do...while` loop. The `do...while` loop is not in the AP Java subset.

### The For Loop

The `for loop` follows the general syntax below:

```java
for (***initialization***; ***termination condition***; ***iteration action***) {
	**statements**
}
```

The for loop is used for iterating for a known amount of time. The ***initialization*** will be run at the beginning of the loop and is used to initialize variables, called **target variables**, used in the for loop. This variable can be referenced in both the ***termination condition*** and the ***iteration action***. The termination condition is used to determine when the for loop will be exiting. If it is false at the beginning of an iteration, the loop will stop execution immediately. The iteration is used to run a statement of code at the end of each iteration. It is commonly used to increment the target variable(s).

The below code will print all numbers from 1 - 10:  

```java
for (int i = 1; i <= 10; i++) {
	System.out.println(i)
}
```

The target variable should not be changed in the body of the loop.

### The For Each Loop

The `for each loop`, also known as the `enhanced for loop` is a modified for loop that allows for iteration over arrays and collections which implement the interface **`Iterable<T>`**. It expands upon compilation.

```java
for (T element : collection) {
	**statements**
}
```

If the collection is an array, it is expanded to:

```java
for (int i = 0; i < collection.length; i++) {
    T element = collection[i];
    **statements**
}
```

If the collection is an object which implements `Iterable<T>`, it is expanded to:

```java
for (Iterator<T> iterator = collection.iterator(); iterator.hasNext(); ) {
    T element = iterator.next();
    **statements**
}
```

The for each loop cannot be used to replace or remove elements from the collection while iteration over it. It also hides the index of the container.

### The While Loop

The while loop repeatedly executes a block of code until a boolean condition becomes false. It is often used to loop for an unknown amount of times. The boolean condition is checked at the beginning of the loop, and at the end of every subsequent iteration. If it is false, the loop will stop execution and control will pass to the next statement

```java
while (<boolean-condition>) {
	**statements**
}
```

# Errors and Exceptions

Java uses exceptions as its main error handling mechanism. An **exception** is an error condition that can happen during the execution of a program. They are reserved for “exceptional” cases when the program must be stopped. Some examples include when the program is out of available memory, when a number is divided by zero, or using an out of index array operation. These exceptions can be handled and code can be executed in the event of an exception. However, if an exception is not handled, it will propagate up the call stack until it reaches the main method, where, if left unhandled, will cause the program to exit.

## Errors vs Exceptions

All errors and exceptions are subclasses of the `Throwable` class. Errors and Exceptions both are both children of the `Throwable` class. Errors are used when the problem mostly arises due to a shortage of system resources, while Exceptions are used for exceptional situations that occur during the runtime and compile time. 

## Throwing Exceptions

Exceptions should be thrown in exceptional situations, where the situation cannot be handled appropriately by the surrounding code. For example, a function that divides 2 numbers. When the denominator is 0, a function cannot return a number representing $\frac{a}{b}$ if b is 0. In this situation, an exception should be thrown. This exception can then be caught in the code that calls this method.

Exceptions can be thrown with the `throw` keyword. the throw keyword can be used to throw any instance of the `Throwable` class or any of its subclasses. Java has several built-in exceptions, such as `ArithmeticException`, all of which can constructed with an error message

```java
public class Calculator {
	public static double divide(double a, double b) {
		if (b == 0) throw new ArithmeticException("division by zero");
		return a / b;
	}
}
```

## Handling Exceptions

Exceptions can be handled with a `try…catch…finally` statement. The code that may produce an exception is placed inside the `try` block. The code in the catch block will run in the event of a specified exception type. the code in the optional finally block will run regardless of whether an exception is thrown or not.

The catch block can catch a specific type of exception, or its subclasses

```java
int x;
try {
	x = 10 / 0;
} catch (ArithmeticException e) {
	System.out.println("Caught exception: " + e)
} finally {
	System.out.println("I will run regardless of exceptions")
}
```

## Common Exceptions

There are 6 common exceptions in the AP Java subset, and 2 more optional exceptions that involve iterators.

### Arithmetic Exception

This exception is thrown when an exceptional arithmetic situation occurs, such division by zero.

```java
int x;
try {
	x = 10 / 0
}
catch (ArithmeticException e) {
	System.out.println("Caught exception: " + e)
}
```

### Null Pointer Exception

This exception is thrown when the developer tries to access a property or call a method on a null reference. 

```java
BankAccount frank; // defaults to null

try {
	frank.deposit(100); // frank is null
} catch (NullPointerException e) {
	System.out.println("Caught exception: " + e);
}
```

### Class Cast Exception

This exception is thrown when an [improper cast](Introductory%20Java%20Features%2034c667afb2cb4d9cb3508064f1d50a77.md) is made.

```java
BankAccount frank = new BankAccount("Frank", 100);
String frankString;
try {
	frankString = (BankAccount) frank;
} catch (ClassCastException e) {
	System.out.println("Caught exception: " + e);
}
```

### Array Index Out Of Bounds Exception

This exception is thrown when a negative index or a number larger than or equal to the length of the array is used to index an array

```java
int[] numbers = { 1, 2, 3, 4 };
try {
	System.out.println(numbers[-2]);
	System.out.println(numbers[10]);
} catch (ArrayOutOfBoundsException e) {
	System.out.println("Caught exception: " + e);
}
```

### Index Out Of Bounds Exception

This exception is thrown when a negative index or a number larger than or equal to the length of the array is used to index an indexable data structure

```java
BankAccount frank = new BankAccount("Frank", 100);
String frankString;
try {
	frankString = (BankAccount) frank;
} catch (IndexOutOfBoundsException e) {
	System.out.println("Caught exception: " + e);
}
```

### Illegal Argument Exception

This exception should thrown when arguments to a function are illegal.

```java
public class Calculator {
	public static double divide(double a, double b) {
		if (b == 0) throw new ArithmeticException("division by zero");
		return a / b;
	}
}
```

### No Such Element Exception

This exception is thrown when there are no more elements for an iterator to iterate over and the `next` function is called.

```java
List<Integer> list = new Arraylist();
Iterator<Integer> iter = list.iterator();
try {
	iter.next(); // No elements to interator over
} catch (NoSuchElementException e) {
	System.out.println("Caught exception: " + e);
}
```

### Invalid State Exception

This exception is thrown to indicate a method has been invoked at the wrong time. An example of this is when an iterator’s `remove` method is called before any call to `next`.

```java
List<Integer> list = new Arraylist();
Iterator<Integer> iter = list.iterator();
try {
	iter.remove(); // `next` method not invoked yet
} catch (InvalidStateException e) {
	System.out.println("Caught exception: " + e);
}
```

# Multiple Choice Questions

1. B
2. E
3. D
4. E
5. E
6. C
7. B
8. D
9. D
10. A
11. C
12. D
13. A
14. C
15. A
16. D
17. A
18. C
19. D 
20. D
21. B
22. C
23. B
24. E
25. D
26. D