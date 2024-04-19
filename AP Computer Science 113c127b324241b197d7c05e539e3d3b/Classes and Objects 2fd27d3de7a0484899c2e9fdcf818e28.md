# Classes and Objects

Objects are encapsulations of variables (state) and methods (behavior) to manipulate the state. Java programs can use primitive objects such as integers and floats, and user-defined objects. Java can store user defined objects in variables, and does so with a reference, where the variable, and all variables that are assigned the initial variable reference one object in memory.

## Classes

Classes are user-defined blueprints to make objects. They can be thought of as object templates, where custom data can be inputted. The current state of the object is maintained in its *instance fields*/*attributes*/*properties*. The state can be modified via *methods*. These 2 concepts, fields and methods, can be *encapsulated* (combined) into a singular class. Objects can be created from classes — the object would be an *instance* of the class.

Below is a simple class for a Bank Account, without implementations

```java
public class BankAccount {
	private String password;
	private double balance;
	public static final double OVERDRAWN_PENALTY = 20.00;

	//constructors
	/** Default constructor.
	* Constructs bank account with default values. */
	public BankAccount()
	{ /* implementation code */ }

	/** Constructs bank account with specified password and balance. */
	public BankAccount(String acctPassword, double acctBalance)
	{ /* implementation code */ }

	//accessor
	/** @return balance of this account */
	public double getBalance()
	{ /* implementation code */ }

	//mutators
	/** Deposits amount in bank account with given password.
	* @param acctPassword the password of this bank account
	* @param amount the amount to be deposited
	*/
	public void deposit(String acctPassword, double amount)
	{ /* implementation code */ }

	/** Withdraws amount from bank account with given password.
	* Assesses penalty if balance is less than amount.
	* @param acctPassword the password of this bank account
	* @param amount the amount to be withdrawn
	*/
	public void withdraw(String acctPassword, double amount)
	{ /* implementation code */ }
}
```

## Access Modifiers and Static

Classes, as well as fields and methods in a class can be given an access (`public`/`protected`/`private`) modifier and be set as static with the `static` keyword.

```java
public class BankAccount {
	public void deposit() {...}
}
```

A `public` modifier indicates that the method or field can be accessed in the class, in subclasses, and outside the class. A `protected` modifier indicates that the method or field can be accessed in the class, in subclasses, but not outside the class. A `private` modifier indicates that the method or field can only be accessed in the class. If the modifier is omitted, it is package protected — it is only accessible in the class, and outside the class and in subclasses in the same package of the class.

The `static`keyword means that the thing the keyword is modifier is allocated once.`static` fields/variables belong to the class itself and are shared between all instances of that class. They are often used to keep accumulate a total or as a constant namespaced to a class. A `static` method belongs to the class as well and is shared between instances. They are invoked in the following manner. Static variables and methods can be accessed anywhere in the class (i.e. both in instance and static methods)

```java
ClassName.methodName();
ClassName.fieldName;
```

## Methods

### Headers

All methods are defined in the following way

```java
public static int add(int a, int b) {...}
```

They consist of several parts, highlighted below

| Access Modifier | Static (optional) | Return Type  | Method Name | Parameter list |
| --- | --- | --- | --- | --- |
| public | static | int | add | (int a, int b) |

```java
public class User {
	private String firstName;
	private String lastName;
	
	public String getFirstName() {
		return this.firstName;
	}

	public String getLastName() {
		return this.lastName;
	}

	public String getFullName() {
		return this.firstName + " " + this.lastName;
	}
}
```

### Constructors

A constructor is a special method, meant to create and initialize an object. Its name is always the same as its class. It usually has a `public` access modifier and has no return type (not `void`, just no specified return type)

A constructor can take arguments and use these to configure or set the initial values of the objects

```java
public BankAccount(String name, double balance) {
	this.name = name;
	this.balance = balance;
}
```

Constructors can also be overloaded (defined multiple times with different parameters) to provide default values and additional configuration

```java
public BankAccount(String name, double balance) {
	this.name = name;
	this.balance = balance;
}

public BankAccount(String name) {
	this.name = name;
	this.balance = 0.0;
}
```

However, the above implementations are not the preferred way to implement that functionality. Instead, we can chain constructors — call different constructor implementations from inside a constructor. We can do this by calling `this`.

```java
public BankAccount(String name, double balance) {
	this.name = name;
	this.balance = balance;
}

/* 
	This calls the above constructor with a name parameter
	and a 0.0 as a balance default 
*/
public BankAccount(String name) {
	this(name, 0.0);
}
```

The above constructors can be called in the following manner

```java
BankAccount acc = new BankAccount("Harry", 1000.0);
BankAccount acc = new BankAccount("Harry");
```

### Accessors

Accessors, also called **getters**, are methods that return information about the object without mutating the object. They are often titled get*PropertyName* and return the property name specified. They are used to encapsulate data — the fields are `private` and their accessors are `public`, which allows the developer to control what can be accessed or mutated. They can also be used to compound data together.

```java
public class User {
	private String firstName;
	private String lastName;
	
	public String getFirstName() {
		return this.firstName;
	}

	public String getLastName() {
		return this.lastName;
	}

	public String getFullName() {
		return this.firstName + " " + this.lastName;
	}
}
```

### Mutators

Mutators, also called **setters**, are methods that change, or mutate, its internal state (its instance fields). The term setters is usually reserved for methods that sets one instance variable to a certain value, and are usually presented with **set…**.

```java
public class User {
	private String firstName;
	private String lastName;
	
	public void setFirstName(String name) {
		this.firstName = name;
	}

	public void setLastName(String name) {
		this.lastName = name;
	}

	public void setFullName(String name) {
		String[] names = name.split(" ");

		this.setFirstName(names[0]);
		this.setLastName(names[1]);
	}
}
```

### Static Methods

Static methods, declared with the static keyword, are methods that belong to the class, and not any particular instance of the class. They cannot use access any instance fields, but can access static fields. It is used for methods that are related to class, but not to any particular instance of the class. (For example, a method that determines whether or not a given day is a weekend on a Calendar class)

```java
public class Employee {
	private static int employeeCount = 0;

	public Employee() {
		employeeCount++;
	}

	public static getEmployeeCount() {
		return employeeCount;
	}	
}
```

### Method Overloading

Overloaded methods are 2 or more methods in the same class with the same name, but a different parameter lists. Java allows the developer to do this and will determine which method to call passed on the passed parameters. This is often used to give default arguments to functions, as demonstrated below:

```java
public class Math {
	public static product(int a, int b) {
		return a * b;
	}

	// This calls the above method with `a` and `a` as arguments
	public static product(int a) {
		return product(a, a);
	}
}
```

This can also be done with constructors to give default values to fields (see [Constructors](Classes%20and%20Objects%202fd27d3de7a0484899c2e9fdcf818e28.md)).

You cannot have multiple methods that are only differentiated by their return types. The compiler doesn't know which one to call.

### Scope

The **scope** of a variable or method is the region in which it can be accessed.

Instance variables, static variables, and methods of a class belong to that class’s
scope, meaning it can be accessed within the class. Within the class all instance variables and methods are accessible and can be simply referred to by name.

**Local variables**, variables declared inside a method, are accessible from the the point they were declared in, to the end of the block it is declared it. Local variable stake precedence over instance variables with the same name, although this situation should be avoided and is bad programming practice

### The `this` Keyword

An instance method or variable are always called on a particular instance of an object. The object is an **implicit parameter** of any instance method call, and it can be referred to in the method using the keyword `this`.  **You are expected to know this vocabulary for the exam**.

In the example below, `obj` is an implicit parameter, whereas `amount` **is an explicit parameter.

```java
obj.deposit(amount);
```

If the object above has a `balance` instance variable, we can implement the method as:

```java
public void deposit(double amount) {
	this.balance += amount;
}
```

## References

### References vs Primitive Data Types

All of the data types that are keywords (`byte`, `int`, `short`, `long`, `float`, `double`, `char`, `boolean`), are **primitive data types**. All objects (e.g. `String`) are **reference data types**.

Consider the following code:

```java
int num1 = 10;
int num2 = num1;
```

Both variables, `num1` and `num2`, are primitive types and each occupy their own slot in memory (i.e. they have different memory addresses).

![Untitled](Classes%20and%20Objects%202fd27d3de7a0484899c2e9fdcf818e28/Untitled.png)

Because they have different memory addresses, changing one of them will not change the other.

Contrast this with the reference data type (i.e. an object) below:

```java
Date d = new Date(2, 17, 1948);
```

With the above code, Java creates the date object in memory, and stores the memory address in the variable. This means that `date1` is a reference variable: it stores the memory address to the object and dereferences it upon usage.

![Untitled](Classes%20and%20Objects%202fd27d3de7a0484899c2e9fdcf818e28/Untitled%201.png)

Suppose the following declaration is made after the above one:

```java
Date birthday = d;
```

This will create 2 reference variables pointing to the same object in memory, and changing the object through one of the variables will affect the other variable.

![Untitled](Classes%20and%20Objects%202fd27d3de7a0484899c2e9fdcf818e28/Untitled%202.png)

When 2 variables reference the same object in memory, it is known as **aliasing**. This can sometimes create unintended problems for developers when they change the object through one variable and forget this changes the other variable as well.

### The Null Reference

The declaration below creates a reference variable that is uninitialized (i.e. it doesn’t point to an object in memory). This variable `b` is called a **null reference** or **null pointer**. The null reference only occurs in reference variables, as all primitive types have sensible defaults (i.e. 0 for numerical, false for boolean)

```java
BankAccount b;
```

Instead, it points to `null`, a special value in Java that represents the absence of any value.

Attempting to invoke an instance method or access and instance property on a **null reference** will throw a `NullPointerException`.

## Method Parameters

### Formal vs Actual Parameters

When a method is defined, it defines a parameter list. The variable names defined in this parameter list are called **formal parameters** (or just **parameters**), and the actual values provided when the method is called are called **actual parameters** (or **arguments**)

```java
public class BankAccount {
	...
	// Amount is the formal parameter
  public void deposit(double amount) {...}
}

public class Main {
	public static void main(String[] args) {
		BankAccount b = new BankAccount(...);
    
		// 100 is the actual parameter
		b.deposit(100); 
	}
}
```

### Passing Primitive Types as Parameters

In Java, all parameters are passed by value, although primitives are the only ones truly passed by value; references variables are passed by reference by passing the reference to the object by value. This means that primitive parameters are each allocated their own spot in memory, and the value passed will be copied into this new memory slot, and changes to the formal parameters will not affect the actual parameter’s value. When the method is exited, these memory slots for the parameters will be erased

### Passing Reference Types as Parameters

Reference types will have their stored addresses to an object copies by value, so the formal and actual parameters will point to the same object in memory, but the parameters will essentially be 2 different variables. This means that changes to the object in the method will change the value of the actual parameter. However, assigning to a reference parameter will not change the underling object, as it will simply make the variable point to a different object.