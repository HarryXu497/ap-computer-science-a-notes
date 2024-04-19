# Inheritance and Polymorphism

# Superclass and Subclass

**Inheritance** defines a relationship between 2 classes that share characteristics. Specifically, it is a mechanism where a new class, the **subclass**, is created from an existing class, the **superclass**, by inheriting and extending the functionality of the superclass. Inheritance provides an effective way to reduce code duplication and makes the code easier to test.

# Inheritance Hierarchy

A subclass can be a superclass for another subclass, creating a hierarchy of classes, called an **inheritance hierarchy**.

For example, consider the relationship between the classes `Person`, `Student`, `Employee`, `UnderGrad`, and `GradStudent`.

![Untitled](Inheritance%20and%20Polymorphism%20e68f5c56b4a24d01905ae45f14cb80e2/Untitled.png)

For each of these classes, there is an arrow pointing towards its superclass. This designates an inheritance relationship between the 2 classes. Informally, this relationship is an **is-a** relationship (i.e. a student **is a** person, but a person is not necessarily a student). This relationship is transitive.

# Implementing Subclasses

## The `extends` keyword

The inheritance relationship between 2 classes is defined in the  subclass via the `extends` keyword

```java
public class Student {
	// private instance variables
	// other data members
	// constructors
	// public methods
	// private methods
}

public class GradStudent extends Student {
	// private instance variables
	// other data members
	// constructors
	// public methods
	// private methods
}

public class UnderGradStudent extends Student {
	// private instance variables
	// other data members
	// constructors
	// public methods
	// private methods
}
```

## Inheriting Instance Methods and Variables

Subclasses inherit the public and protected data members of their parent. They do not inherit the private instance variables or methods of their superclasses but still contain memory to hold these values. 

In the student example, `UnderGradStudent` and `GradStudent` inherit of all of the public/protected members of the `Student` class. The private members are not inherited or directly accessible inside the class. However, it can still access them indirectly via accessors and mutators, as it still holds these private instance variables in its memory.

## Method Overriding and The `super` keyword

Any public method in a super class can be overridden in a subclass. To do this, the subclass defines a method with the exact same return type and signature (same parameter list and same name).

We can override a method and give it a completely new definition, but that is something more akin to abstract classes. In concrete classes, usually the overridden method will call the superclasses method using the `super` keyword. This is called **partial overriding**

The `super` keyword is used to refer to the superclass of a class. In this case, it is used to access data and methods in the superclass of a class. However, it can also be used to call the superclass’s constructor, which is something we’ll see shortly.

Given the above example, we can override a method like the following:

```java
public class Student {
	// private instance variables
	private double[] testMarks;
	// other data members
	// constructors
	public Student(double grade) { ... }
	// public methods
	public double getTestMarks() { ... }
	public void addTestMark(double mark) { ... }
	public double computeGrade() { ... }
	// private methods
}

public class GradStudent extends Student {
	// private instance variables
	// other data members
	// constructors
	// public methods
	public double computeGrade() {
		super.computeGrade();
		if (getTestAverage() >= 90) {
			...
		}	
	}

	public int getID() { ... }
	// private methods
}
```

<aside>
💡 Note: Usually, overridden methods in Java are marked with the `@Overide` annotation. This will ensure that all methods marked with this annotation are actually overriding a method in the superclass. **THIS IS NOT PART OF THE AP JAVA SUBSET**

</aside>

## Constructors and `super`

Constructors are never inherited. If any constructors are written for a class, only those can be used. If there are no constructors written, java will generate an empty no-arg constructor (This constructor will call the superclass constructor if it extends a class). To invoke the superclass constructor, super is used. The call to super should the first thing in subclass constructor, but if it isn’t, it will call the superclasses default constructor (if it does not exist an error will occur).

```java
// Prints A B
// constructor for B calls A **implicitly**
class A {
    public A() {
        System.out.println("A");
    }
}

class B extends A {
    public B() {
				// super(); this line would have no effect on the output
        System.out.println("B");
    }
}
```

```java
// Error: B **implictly** calls the default constructor of A, which does not exist
class A {
    public A(int x) {
        System.out.println("A: x = " + x);
    }
}

class B extends A {
    public B() {
        System.out.println("B");
    }
}
```

```java
// prints B
// B **implicitly** calls the default cosntructor of A, which is auto-generated
class A {}

class B extends A {
    public B() {
				// super(); this line would have no effect on the output
        System.out.println("B");
    }
}
```

```java
// Error: B **implicitly** calls the no arg constructor of A, which does not exist
class A {
    public A(int x) {
        System.out.println("A");
    }
}

class B extends A {
    public B(int x) {
        System.out.println("B");
    }
}
```

```java
// prints A B
// B **explicitly** calls the constructor of A
class A {
    public A(int x) {
        System.out.println("A");
    }
}

class B extends A {
    public B(int x) {
        super(x);
        System.out.println("B");
    }
}
```

## Declaring Subclass Objects

When a variable with a type of a super class object is declared, that reference can also refer to any of its subclasses. Therefore, the following code is legal:

```java
Student s = new Student();
Student g = new GradStudent();
Student u = new UnderGradStudent();
```

This is because of the inheritance **is-a** relationship. A `GradStudent` **is-a** `Student` and can therefore be stored in a `Student` variable.

Inheritance is one-way, so the following lines of code are illegal, as a `Student` **is not necessarily** a `GradStudent`.

```java
GradStudent g = new Student();
UnderGradStudent u = new Student();
```

# Polymorphism

Java has 2 examples of polymorphism: **Method Overriding** and **Method Overloading**.

The below notes talks entirely about **method overriding**.

A method that has been overridden in at least one subclass is said to be **polymorphic**. Polymorphism is the mechanism of selecting the appropriate method for a particular object in a class hierarchy. For **method overriding**, Java uses **dynamic dispatching** (also known as dynamic or late binding), where the type of the object stored in a variable, not the variable type. Dynamic dispatching locates the right method to call **at runtime**, unlike static dispatch, which does this at compile time.

The below code will call the `computeGrade` method in the `GradStudent` class, not the `Student` class’s version. This is because, although the variable `s` is of type `Student`, it holds a subclass object, a `GradStudent`, whose overridden version of the method gets called.

```java
Student s = new GradStudent();
s.computeGrade();
```

## Dynamic Binding

Making a runtime decision about which instance method to call is known as **dynamic binding** or **late binding**. For **method overloading**, Java determines which method to call based on its signature at **compile time**, which is known as **static binding** or **early binding**.

## Polymorphism in Action

We can combine polymorphism (method overriding) and Java’s feature of allowing subclass objects to be stored in superclass variables. This is where we can really see the power of polymorphism. We can have a list/array of superclass types which can each store the superclass itself or any subclass types. We can call a overridden method on each item in the array and Java will determine to correct one to call.

```java
Student[] students = new Student[3];

students[0] = new Student(...);
students[1] = new GradStudent(...);
students[2] = new UnderGradStudent(...);

for (int i = 0; i < students.length; i++) {
	Student student = students[i];

	// Java will determine the correct method to call at **runtime**
	student.computeGrade();
} 
```

## Using `super` in a Subclass

A subclass can call a method in its superclass by using super. Suppose that the superclass method then calls another method that has been overridden in the subclass. By polymorphism, the method that is executed is the version in the subclass.

```java
public class Dancer {
	public void act() {
		System.out.println("Spin");
		doTrick();
	}

	public void doTrick() {
		System.out.println("Float");
	}
}

public class Acrobat extends Dancer {
	public void act() {
		super.act();
		System.out.println("Flip");
	}

	public void doTrick() {
		System.out.println("Somersault");
	}
}
```

- What will the following code output to the console?
    
    ```bash
    Spin Somersault Flip
    ```
    

```java
Dancer a = new Acrobat();
a.act();
```

# Type Compatibility

## Downcasting

Consider the following code

```java
Student s = new GradStudent();
GradStudent g = new GradStudent();
int x = s.getID(); // compile time error
int y = g.getID(); // legal
```

Why does `s.getID()` cause an error but `g.getID()` does not?

This is because `s` is of type `Student` , and the `Student` class does not define a `getID` method. That is defined in the `GradStudent` class. At compile time, Java does not know that `s` holds a `GradStudent`. All it knows is that it may hold itself or a subtype, so it cannot ensure that the call to `getID` is legal, and this causes a compile time error. At compile time, only nonprivate methods of the `Student` class can be accessed with the dot operator.

<aside>
💡 Note that `getID` is not a polymorphic method. It is defined only in `GradStudent` and not in `Student`.

</aside>

If we are certain that `s` holds a `GradStudent` and we want to access members exclusively in `GradStudent`, we need to **downcast**. 

Downcasting is where we cast a superclass type to a subclass type. Note that we aren’t changing the type of the actual object, we are simply making the type more specific.

```java
int x = ((GradStudent) s).getID();
```

The outer parenthesis are necessary as the dot operator has a higher precedence than casting

<aside>
💡 Java determines at compile time whether or not a method call is legal (i.e. does it exist) and it determines at runtime what method to call (i.e. which method to dispatch)

</aside>

## The `ClassCastException`

A `ClassCastException` is thrown at runtime when an attempt is made to cast an object to a class of which it is not an instance.

# Abstract Classes

## Abstract Class

An **abstract class** is a superclass that represents an abstract concept and therefore should not be instantiated. An abstract class may also contain abstract methods, which has no implementation associated with it. Every non-abstract (concrete) class that extends this abstract class must implement all of these abstract methods or a compile time error is thrown.

## The `abstract` Keyword

An abstract class is defined with the keyword `abstract` in the header.

```java
public abstract class AbstractClass { ... }
```

The keyword `extends` is used as before to declare a subclass

```java
public class SubClass extends AbstractClass { ... }
```

If a subclass of an abstract class does not provide implementation code for all of the abstract methods declared in its superclass, it too must become an abstract class or a compile time error will occur.

```java
public abstract class SubClass extends AbstractClass { ... }
```

Below is an example:

```java
public abstract class Shape {
	public abstract double area();
	public abstract double perimeter();
	public double semiPerimeter() {
		return this.perimeter() / 2;
	}
}

public class Circle extends Shape {
	private double radius;

	public Circle(double radius) {
		super();
		this.radius = radius;
	}

	public double perimeter() {
		return 2 * Math.PI * radius;
	}

	public double area() {
		return Math.PI * radius * radius;
	}
}

public class Square extends Shape {
	private double sideLength;

	public Square(double sideLength) {
		super();
		this.sideLength = sideLength;
	}

	public double perimeter() {
		return 4 * side;
	}

	public double area() {
		return side * side;
	}
}
```

A couple things to note

1. The `perimeter` and `area` methods are abstract because there is no concrete way to calculate them for a concept as abstract as a `Shape`. Instead, we let any shapes that inherit from `Shape` to define their own way to calculate `area` or `perimeter`.
2. An abstract class can have both instance variables and concrete methods (i.e. `semiPerimeter`).
3. A concrete subclass of an abstract class must provide implementations for all abstract methods. Therefore both the Circle and Square classes implement both the `perimeter` and `area` methods.
4. It is possible for an abstract class to have no abstract methods. An abstract subclass can inherit abstract methods from a abstract superclass.
5. An abstract class may or may not have constructors.
6. No instances can be created for an abstract class.
7. Polymorphism works with abstract classes as it does with concrete classes. For example, the `semiPerimeter` method defined in `Shape` will call the `perimeter` method in whatever subclass is calling it.

# Interfaces

## Interface

An interface is a collection of related methods, either abstract (headers only) or default implemented. Default methods are new in Java 8 and **will not be on the AP exam**. The non default methods are both public and abstract — no need to explicitly include these keywords.

The classes that implement a given interface may represent objects that are vastly difference. They all, however, share a common capability expressed by the methods of the interface. For example, if we are making a game with several different objects, such as a `Player` and `Enemy`, both Player and Enemy may implement a `Moveable` interface as they can both move. However, a class representing a Powerup may not implement this interface as they do not move.

## Defining an Interface

An interface is declared in its own file with the interface keyword

```java
public interface Moveable {
	void move();
	boolean isMoving();
}
```

## The `implements` Keyword

Interfaces are implemented using the `implements` keyword:

```java
public class Enemy implements Moveable { ... }
```

This declaration means that the `Enemy` class must implement the `move` and `isMoving` methods as declared in the interface. Note that any subclass of `Enemy` will also implement the interface, as it will inherit the methods defined in `Enemy`.

A subclass that extends a superclass can also directly implement an interface:

```java
public class Bee extends Insect implements FlyingObject { ... }
```

The `extends` clause must precede the `implements` clause. A class have only inherit from one superclass but it can implement any number of interfaces

## The `Comparable` Interface

Starting in 2015, **this will not be tested on the AP exam**. Students will, however, be
required to use `compareTo` for comparison of strings