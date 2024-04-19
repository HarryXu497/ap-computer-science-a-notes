# Some Standard Classes

# The `Object` Class

The `Object` class is the universal superclass of all objects, either directly or indirectly. If a superclass is not specified by a class, it implicitly inherits from `Object`.

![Untitled](Some%20Standard%20Classes%20213a7f76d2674a2aa35a19ead780de38/Untitled.png)

## Methods in `Object`

There are many methods declared in Object, which are all inherited by every class. Since Object is a concrete class, all of its methods have implementations. The expectation is that these methods will be overridden in any class where the default implementation is not suitable. The methods off Object in the AP Java subset are `toString` and `equals`.

### The `toString` Method

This method returns a version of your object in String form. When you attempt to print an object, the inherited default `toString` method is invoked, and what you will see is the class name followed by an `@` followed by the memory address.

```java
SavingsAccount s = new SavingsAccount(500);
System.out.println(s); // ouputs something like SavingsAccount@fea485c4
```

To provide a more meaningful output, you need to override the `toString` method in your own classes.

```java
public class OrderedPair {
	private double x;
	private double y;	
	...
	/**
	* @return this OrderedPair in String form
	*/
	public String toString() {
		return "(" + x + ", " + y + ")";
	}
}
```

Now the statements

```java
OrderedPair p = new OrderedPair(7,10);
System.out.println(p);
```

Will output

```
(7, 10)
```

<aside>
💡 Note that Array objects do not have a `toString` method and to print the elements it must be traversed and each element must be explicitly printed.

</aside>

### The `equals` Method

The default version of this method will check 2 objects for identity (i.e. if they share the memory location). Using the equality (`==`) operator will do the same.

Often times you want two objects to be equal if their contents are the same, in which case we need to override the `equals` method and use that instead of the equality (`==`) operator.

**You will not be required to write code that overrides `equals` on the AP exam**

### The `hashCode` Method

<aside>
💡 **This is an optional topic**

</aside>

Every class inherits the `hashCode` method from Object. The value returned in an integer produced by a has function. A given object with the same contents should always produce the same `hashCode`. If 2 objects are equal (content-wise), they should produce the same hash code, but if they produce the same hash code it does not necessarily mean they are equal. If `obj1.equals(obj2)` is true, it implies that they should have the same hash code. **You will not be required to do this on the AP exam**.

# The String Class

An object of type String is a sequence of characters, All String literals, such as `"Java!"` are implemented as instances of this class. 

String objects are immutable, which means that there are no methods to change them after they’ve constructed. You can, however, make a new string from an existing String. For example, when concatenation is used for strings, it will create a new string object.

## Constructing `String` Objects

Because Strings are so commonly used in Java, they get special treatment from the language. They can be initialized like a primitive type:

```java
String s = "abc";
```

The above is equivalent to:

```java
String s = new String("abc");
```

in the sense that in both cases s is a reference to a `String` object with contents `“abc”`.

## The Concatenation Operator

We can use the addition operator with strings to create a new string with the 2 string parts joined together. If either the left or right hand operands are non string objects, Java will convert them by calling the `toString` method and then concatenate as normal. If both are non string objects, and error will occur.

## Comparison of `String` Objects

There are two ways to compare `String` objects (by value, not identity).

1. Use the `equals` method inherited from `Object` and overridden in `String`.
2. Use the `compareTo` method.
    - This will compare strings in lexicographical order.
        - If `string1.compareTo(string2) < 0`, `string1` precedes `string2` alphabetically.
        - If `string1.compareTo(string2) > 0`, `string1` follows `string2` alphabetically.
        - If `string1.compareTo(string2) == 0`, `string1` are identical to `string2` alphabetically.
    - Characters are compared to based on their position in the ASCII chart. All you need to know is that all digits precede all capital letters, which precede all lowercase letters.
    - If 2 strings are identical but one is shorter, the short one will precede the longer one
        
        ```java
        "hot".compareTo("hotel") < 0 // **true**, "hot" terminates first
        ```
        

## Other String Methods

### Length

<aside>
💡 `**int length()**`

</aside>

Returns the length of the string

### Substring

<aside>
💡 **`String substring(int startIndex)`**
**`String substring(int startIndex, int endIndex)`**

</aside>

These methods will return a new string that is a substring of the current string. It will start at `startIndex` (inclusive) and go up to `endIndex` (exclusive). if the `endIndex` is not included, it will go from `startIndex` to the end of the string.

These methods will throw `IndexOutOfBoundsException` if `startIndex` is negative, `endIndex` is larger than the length of the string (equal is fine), or if `startIndex` is larger than `endIndex`.

**`StringIndexOutOfBoundsException` will be thrown on Java 7+, but the AP Java subset will use `IndexOutOfBoundsException`.** 

### Index Of

<aside>
💡 **`int indexOf(String str)`**

</aside>

This method returns the index of the first occurrence of `str` within this string. If will return `-1` if str is not a substring of this string, and it will throw a `NullPointerException` is str is null.

# Wrapper Classes

A wrapper class takes either an existing object or a value of primitive types and “wraps” or “boxes” it in an object, and also provides a set of methods to for type. 

In each case, the wrapper class allows:

- The construction of an object from a single value (wrapping/boxing the primitive in a wrapper object).
- The retrieval of the primitive value (unwrapping/unboxing from the wrapper object)

Java provides a wrapper class for each of its primitive types. The two that you should know for the AP exam are the `Integer` and `Double` classes.

## Auto-boxing and Auto-unboxing

<aside>
💡 **These topics are not mentioned in the AP Computer Science A Textbook**

Auto-boxing and auto-unboxing is a feature in Java 5.0 and later versions and will not be
tested on the AP exam. It is OK, however, to use this convenient feature in code that
you write in the free-response questions.

</aside>

For ease of use, each of the primitive wrapper classes can be used in the following manner:

```java
Integer i = 3;
// Equivalent to
// Integer i = new Integer(3);

if (i == 5) { ... }
// Equivalent to
// if (i.intValue() == 5) { ... }
```

This is called auto-boxing and auto-unboxing and it helps make code more readable in Java. It will coerce primitive types to their wrapper counterpart and vice-versa when needed.

Be aware that is a program tries to auto-unbox null, the method will throw a `NullPointerException`.

Note that while auto-boxing and auto-unboxing reduce code clutter and improve readability, these boxing and unboxing operations must still be performed behind the scenes, leading to decreased run time efficiency. It is much more efficient to use an array with primitives types than an `ArrayList` of primitive wrapper classes.

## The `Integer` Class

The Integer class wraps a value of type `int` in an object. An object of type `Integer` contains just onw instance variable whose type is `int`.

It contains the following methods that you should know for the AP exam

- `**int compareTo(Integer other)**`
    - Works the exact same way they do in `String`.
- **`boolean equals(Object obj)`**
    - Returns true if and only if this `Integer` has the same int value as `obj`.
    - This method will throw a `ClassCastException` if obj is not an `Integer`.
- `**int intValue()**`
    - Returns the value of the int this `Integer` wraps. (unboxing)
- **`Integer(int value)`**
    - Construct an `Integer` object from an int. (boxing)
- **`String toString()`**
    - Returns a string representation of this `Integer`.

## The `Double` Class

This wrapper class wraps a double

It contains the following methods that you should know for the AP exam

- `**int compareTo(Doubleother)**`
    - Works the exact same way they do in `String`.
- **`boolean equals(Object obj)`**
    - Returns true if and only if this `Double` has the same int value as `obj`.
    - This method will throw a `ClassCastException` if obj is not an `Double`.
- `**double doubleValue()**`
    - Returns the value of the double this `Double` wraps. (unboxing)
- **`Double(double value)`**
    - Construct an `Double` object from an double. (boxing)
- **`String toString()`**
    - Returns a string representation of this `Double`.

# The `Math` Class

This class implements standard mathematical functions and constants.

Here are the functions you should know for the AP exam:

- **`static int abs(int x)`**
- **`static double abs(double x)`**
- **`static double pow(double base, double exp)`**
- **`static double sqrt(double x)`**
- **`static double random()`**
    - returns a random number $r$ where $0.0 \le r < 1.0$
    - You will need to be able to scale this range to generate random numbers in any real range. This can be done like the following, to generate a range $l \leq r < h$
    
    ```java
    double x = (h - l) * Math.random() + l;
    ```
    
    - To generate a random integer in that range $l \leq r \leq h$, the following can be done:
    
    ```java
    int x = (int) ((h - l + 1) * Math.random()) + l;
    ```
    

These methods are all implement as static methods and variables, meaning that there are no instances of Math objects.

# Multiple Choice Questions

1. B
2. B
3. C
4. C
5. A
6. D
7. E
8.