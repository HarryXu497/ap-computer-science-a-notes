# Arrays and Array Lists

# One-Dimensional Arrays

An array is a data structure consisting of a sequential list of elements, all of the same type. An array is declared with a fixed size that cannot be changed after declaration. In memory an array is stored in a contiguous block of memory. For example, an array of 8 integers are stored in 32 bytes of memory (4 bytes for each integer * 8 slots).

Items are accessed with square brackets, also known as the subscript operator. If `arr` is an array of `N` elements, the elements are `arr[0]`, `arr[1]`, `...`, `arr[N-1]`. If a negative subscript is used, or a subscript k where $k \ge N$, an `ArrayIndexOutOfBoundsExceptions` is thrown.

## Initialization

In Java, an array is an object and so there new keywords must be used to create it. The size of an array remains fixed once it has been created, but an array reference may be reassigned to a new array of a different size.

Each of the following code snippets are equivalent:

```java
double[] data = new double[25];
// OR
double data[] = new double[25];
// OR
double[] data;
data = new double[25];
```

A subsequent statement such as:

```java
double = new double[40];
```

reassigns data to a new array of length 40 and the memory allocated for the previous array is garbage collected.

When arrays are declared, the elements are automatically initialized to **zero** for the primitive numeric data types, **false** for booleans, or **null** for object references.

It is possible to declare several arrays in a single statement. For example:

```java
int[] intArray1, intArray2;

int[] intArray1 = new int[15], intArray2 = new int[20];
```

### Initializer List

Small arrays shows values are known can be declared with an initializer list.

```java
int[] coins = { 1, 5, 10, 25 };
// OR
int[] coins = new int[] { 1, 5, 10, 25 };
```

The first version can only be used in a variable declaration with initialization, and any other uses with throw an error.

```java
int[] coins;
coins = { 1, 5, 10, 25 }; // **NOT LEGAL**
coins = new int[] { 1, 5, 10, 25 }; // **DO THIS INSTEAD**
```

## Length of an Array

A Java array has a final public instance variable, `length`, which can be accessed when you need the number of elements in the array. Note that it is a field and not a method.

```java
String[] names = new String[25]

for (int i = 0; i < names.length; i++) {
	// Code
}
```

## Traversing an Array

Use a for-each loops whenever you need to access each element in an array without replacing or removing any elements. Use a for loop for all other cases, to get index, to replace, or remove elements, etc.

Note that if you have an array of objects/reference types, you can use the for each loop and call mutator methods on the object to modify it.

## Arrays as Parameters

Since arrays are treated as objects, passing an array as a parameter means passing its object reference. No copy is made of the array. **Thus the elements of the actual array can be accessed and modified.**

```java
/**
* fill
* fills an integer array with a specified value
* @param array the array to fill
* @param value the value to fill the array with
*/
public static void fill(int[] array, int value) {
	for (int i = 0; i < array.length; i++) {
		array[i] = value;
	}
}
```

```java
public static void main(String[] args) {
	int[] list = { 1, 2, 3, 4 };
	fill(list, 0);
	// list is now: [0, 0, 0, 0]
}
```

## Array Variables in a Class

We can have arrays as variables in a class

## Array of Class Objects

When an array of class objects is created, the default value of each element in the array is `null`.

# Array Lists

In Java, a list is a sequential data structure that can grow and shrink in size dynamically, rather than having a set size upon initialization.

An arraylist works by having an array with an initial size (e.g. 10) behind the scenes, and when the size needs to grow or shrink, a new array is made and the elements in the current array are copied over.

An arraylist provides an alternate way of storing a list of objects and has the following advantages over an array:

- An arraylist shrinks and grows as needed in a program, whereas an array has a fixed length that is set when the array is created.
- In an arraylist, the last slot is always `list.size() - 1`, whereas in a partially filled array the programmer must manually keep track of the last slot in use.
- For an arraylist, you can do insertion or deletion with a single statement. Shifting of elements i handled automatically. In an array insertion or deletion requires the programmer to write the code that shifts the elements.

## The Collections API

The `ArrayList` class is in the Collections API (**Application Programming Interface**), which is a library provided by Java. Most of the API is in `java.util`. This library gives the programmer access to prepackaged data structure and the methods to manipulate them. The implementation of these container classes are private and should not be of concern to the programmer.

All of the collection classes, including `ArrayList`, have the following features in common:

- They are designed to be both memory and run time efficient. They provide methods for insertion and removal of items (i.e. they can grow and shrink).
- They support iteration over the entire collection

## The Collections Hierarchy

Inheritance is a defining feature of the Collections API. The interfaces that are used to manipulate the collections specify the operations that must be defined for any container class that implements that interface.

Most types of collections (i.e. Lists, Maps, Sets) have their own interface which are implemented by specific implementations of the collection. For example, `ArrayList` implements the `List` interface.

## Collections and Generics

The collection classes are generic, with type parameters. Thus, `List<E>` and `ArrayList<E>` contain elements of type `E`.

When a generic class is declared, the type parameter is replaced by an actual object type. For example:

```java
private List<Student> students;
```

A few things to note:

1. The students list must only contain `Student` objects. An attempt to add a `Teacher` to the list, for example, will cause a compile-time error.
2. Since the type of objects in a generic class is restricted, the elements can be accessed without casting
3. All of the type information in a program with generic classes is examined at compile time. After compilation the type information is erased. This feature of generic classes is known as **erasure**. During execution of the program, any attempt at incorrect casting will lead to a `ClassCastException`. 

## [Auto-Boxing and Auto-Unboxing](Some%20Standard%20Classes%20213a7f76d2674a2aa35a19ead780de38.md)

# The `List<E>` Interface

A class that implements the `List<E>` interface — `ArrayList<E>`, for example — is a list of elements of type `E`. In a list, duplicate elements are allowed. The elements of the list are indexed, with 0 being the index of the first element. 

A list allows you to:

- Access an element at any position in the list using its integer index.
- Insert an element anywhere in the list
- Iterate over all elements using `ListIterator` or `Iterator` (**not in the AP subset**)

## The Methods of `List<E>`

Here are the methods you should know. These methods throw an `**IndexOutOfBoundsException`** if an index is negative or it is ≥ to the size of the list and a `**ClassCastException`** if a parameter the specified type does not match the argument type. **However, adding an element to an index `size() + 1`** **using the add methods is allowed and will not throw.**

### Adding An Element

To append an element to the end of the list, the add method can be used. It returns a boolean, indicating whether or not the add operation changed the collection. Because a list permits duplicates, this will always return true.

```java
boolean add(E obj)
...
List<Integer> list = new ArrayList<>(); // []
list.add(5); // [5]
```

To add an element at an specific index, an overload of the add method can be used. The elements at the index and above are shifted and the new element is inserted at the specified index. 

```java
void add(int index, E element)
...
List<Integer> list = new ArrayList<>(); // []
list.add(4); // [4]
list.add(0, 3); // [3, 4]
```

### Getting An Element

To get the element at a specified index, the get method can be used. 

```java
E get(int index)
...
List<Integer> list = new ArrayList<>(); // []
list.add(4); // [4]
list.add(7); // [4, 7]
list.get(1); // 7
```

### Setting An Element

To replace an element at an index with a new value, the set method can be used. It will replace the item at a specified index with a specific element. It will return the element that was previously at the specified index.

```java
E set(int index, E element)
...
List<Integer> list = new ArrayList<>(); // []
list.add(4); // [4]
list.add(7); // [4, 7]
list.set(1, 5); // [4, 5]
```

### Removing An Element

To remove an element from a list, the remove method can be used. It will also return the removed element.

```java
E set(int index, E element)
...
List<Integer> list = new ArrayList<>(); // []
list.add(4); // [4]
list.add(7); // [4, 7]
list.remove(0); // [7]
```

### Getting Iterators

<aside>
💡 **This is an OPTIONAL topic**

</aside>

The iterator method will return an iterator over the elements in a list, in proper sequence, starting at the first element.

```java
Iterator<E> iterator();
...
List<Integer> list = new ArrayList<>(); // []
list.add(4); // [4]
Iterator<Integer> it = list.iterator();
```

## The `ArrayList<E>` Class

In addition to the list methods, you must also know the following constructor which will construct an empty list.

```java
ArrayList()
```

# Collections and Iterators

<aside>
💡 **This is an OPTIONAL topic**

</aside>

An **iterator** is an object whose sole purpose is to traverse a collection one element at a time. During iteration, the iterator object maintains a current position in the collection, and is the controlling object in manipulating the elements of the collection.

## The `Iterator<E>` Interface

The package `java.util` provides a generic interface, `Iterator<E>` whose methods are `hasNext`, `next`, and `remove`.

Here are the methods you should know

### `boolean hasNext()`

Returns true is there’s at least one more element to be examined, false otherwise.

### `E next()`

Returns the next element in the iteration. If no elements remain, the method throws a `NoSuchElementException`.

### `void remove()`

Deletes from the collection the element that was returned by next (i.e. the current element). This method can be called only once per call to `next`. It throws an `IllegalStateException` if the `next` method has not yet been called, or if the `remove` method has already been called after the last call to `next`.

## Using a Generic Iterator

To iterate over a parameterized collection, you must use a parameterized iterator whose parameter is the same type.

**Example One**

```java
List<String> list = new ArrayList<String>();
// <code to initialize list with strings>
Interator<String> it = list.iterator();

while (it.hasNext()) {
	System.out.println(it.next());
}
```

NOTE:

1. Only classes that allow iteration and arrays can use the for each loop. This is because the loop operates using an iterator (or with indices for an array).
2. However, a for each loop cannot be used to remove elements from the collection. Removal of elements should be done with iterators.

# Two-Dimensional Arrays

A two dimensional array (matrix) is often the data structure of choice for objects like board games, table of values, and mazes.

Look at the following 3 x 4 matrix:

$$
\begin{bmatrix}2 & 6 & 8 & 7 \\1 & 5 & 4 & 0 \\9 & 3 & 2 & 8 \end{bmatrix}
$$

If `mat` is the matrix variable, the row subscripts go from 0 to 2 and the column subscripts go from 0 to 3. The element `mat[1][2]` is 4 and the element `mat[2][1]` is 3. As with one dimensional arrays, if the subscripts are out of range, an `ArrayIndexOutOfBoundsException` is thrown.

## Declaration

Each of the following declares a two-dimensional array:

```java
// table can reference a 2D array of integers
// table is currently a null reference
int[][] table;

// matrix references a 3 x 4 array (3 rows, 4 columns) of doubles
// Each element defaults to 0.0
double[][] matrix = new double[3][4];

// strs references a 2 x 5 array (2 rows, 5 columns) of String objects
// Each element defaults to null;
String[][] strs = new String[2][5]
```

We can also use an initializer list with multi-dimensional arrays

```java
int[][] matrix = {
	{ 3, 4, 5 },
	{ 6, 7, 8 }
};
```

## Matrix as Array of Row Arrays

A matrix is implemented as an array of rows, where each row is a one-dimensional array of elements. Supposed `mat` is the 3 x 4 matrix:

$$
\begin{bmatrix}2 & 6 & 8 & 7 \\1 & 5 & 4 & 0 \\9 & 3 & 2 & 8 \end{bmatrix}
$$

Then mat is an array of three arrays

$$
\texttt{mat[0]} \textnormal{ contains } \texttt{[2, 6, 8, 7]} \\ \texttt{mat[1]} \textnormal{ contains } \texttt{[1, 5, 4, 0]} \\ \texttt{mat[2]} \textnormal{ contains } \texttt{[9, 3, 2, 8]}
$$

The quantity `mat.length` represents the number of rows. In this case it equals 3 because there are three arrays in `mat`. For any given row k, where $0 \le k < \texttt{mat.length}$, the quantity `mat[k].length` represents the number of elements in that row, namely the number the number of columns. Java allows a variable number of element in each row. Since these staggered arrays are not part of the AP Java subset, you can assume that `mat[k].length` is the same if all rows `k` of the matrix (i.e. that the matrix is rectangular).