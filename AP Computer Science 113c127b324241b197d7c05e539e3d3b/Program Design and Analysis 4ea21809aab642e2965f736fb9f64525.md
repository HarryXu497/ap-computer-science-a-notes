# Program Design and Analysis

# The Software Development Lifecycle

## The Waterfall Model

The waterfall model of software development came about in the 1960s in order to bring structure and efficiency into the process of creating large programs.

Each step in the process flows into the next and does so in a structured way, although a criticism  of this model is that it is less flexible than other models.

![Untitled](Program%20Design%20and%20Analysis%204ea21809aab642e2965f736fb9f64525/Untitled.png)

## Program Specification

The specification is a written description of the project. Typically it is based on a customer’s requirements. The first step in writing a program is to analyze the specification, make sure you understand it, and clarify with the customer anything that is unclear. 

## Program Design

Even for a small-scale program a good design can save programming time and enhance the reliability of the final program. The design is a fairly detailed for solving the problem outlined in the specification. It should include all objects that will be used in the solution, the data structures that will implement them, plus a detailed list of the tasks to be performed by the program. 

A good design provides a fairly detailed overall plan at a glance, without including the minutiae of Java code.

## Program Implementation

Program implementation is the coding phase that you should be familiar with by now.

## Testing and Debugging

### Test Data

Not every possible input value can be tested, so a programmer should be diligent in selecting a representative set of test data. Typical values in each part of a domain should be selected, as well as endpoint values and out of range values. 

### Type of Errors

- A **compile-time error** occurs during the compilation of the program. The compiler is unable to translate the program into bytecode and prints an appropriate error message. A **syntax error** is a compile-time error caused by violating the rules of the programming language (e.g. missing semicolon).
- A **run-time error** occurs during execution of the program. the Java runtime environment throws an exception, which means that execution is stopped and an error message is printed unless the exception is handled. An error that causes a program to run forever can also be regarded as a runtime error.
- An **intent error** or **logic error** is one that fails to carry out the specification of the program. The program compiles and runs but does not do the job. This can make it hard to debug and fix the error.

### Robustness

Always assume that any user of your program is not as smart as you are, You must therefore aim to write a robust program, namely one that:

- Won’t give incorrect answers for some input data.
- Won’t crash is the input data is invalid.
- Won’t allow execution to proceed if invalid data is entered.

## Program Maintenance

Program maintenance involves upgrading the code as circumstances change. New features may be added. New programmers may come on board. To make their task easier, the original program must have clear and precise documentation.

# Object Oriented Design

Object oriented programming has been the dominant programming methodology since the mid 1990s. It uses an approach that blurs the lines of the waterfall model. Analysis of the problem, development of the design, and pieces of implementation all overall and influence one another.

Here are the steps in object oriented design:

- Identify classes to be written.
- Identify behaviors (i.e. methods) for each class.
- Determine the relationship between classes.
- Write the interface (public method headers) for each class.
- Implement the methods.

## Identifying Classes

Usually, the classes of a program can be identified by picking out the big nouns in the program specification. Some object types that are common in applications are a basic low-level object which usually holds data, a collection of said low-level components, a controlling object that holds everything together, and a display object that could be a GUI.

**Example**

Write a program that maintains an inventory of stock items for a small store.

```
Basic Object: StockItem
Collection: Inventory (a list of StockItems)
Display: StoreDisplay (could be a GUI/CLI)
Controller: Store (has an inventory, uses a StoreDisplay)
```

## Determining Relationships between Classes

### Inheritance Relationships

Look for classes with common behaviors. This will help identify inheritance relationships. If `object1` is-a `object2`, then `object2` is candidate for a superclass.

### Composition Relationships

Composition relationships are defined by the has-a relationship. For example, a `Student` has a `School`. Typically, if 2 classes have a composition relationship, one of them contains an instance variable whose type is the other class. 

Note that a wrapper class always implements a has-a relationship with any objects that it wraps.

## UML Diagrams

An excellent way to keep track of the relationships between classes and show the inheritance hierarchy in your programs is with a UML (Unified Modeling Language) diagram. This is a standard Graphical scheme used by object-oriented programmers. **This is not part of the AP subset, but on the exam you may be expected to interpret simple UML diagrams.**

Here are the general rules:

- Classes are represented with rectangles.
- Use angle brackets with the word abstract or interface to indicate either an abstract class or interface.
- Show the is-a relationship between classes with an arrow pointing up at the superclass.
- Show the is-a relationship between that involves an interface with a dotted arrow pointing up at the interface.
- Show the has-a relationship with an arrow pointing down or sideways.

![Untitled](Program%20Design%20and%20Analysis%204ea21809aab642e2965f736fb9f64525/Untitled%201.png)

## Implementing Classes

### Bottom-Up Development

For each method in a class, list all of the other classes needed to implement that particular method. These classes are called **collaborators** and a class with no collaborators is **independent**.

To implement the classes in an application, often an incremental, bottom-up approach is used. This means that independent classes are fully implemented and tested before being incorporation into the overall project. Typically, these are the basic objects of the program and they can be implemented by different programmers as they are independent of one another.

### Top-Down Development

In a top down design, the programmer starts with an overview of the program selecting the highest-level controlling object and the tasks needed. During development of the program, subsidiary classes may be added to simplify existing classes.

## Implementing Methods

### Procedural Abstraction

A good programmer should void chunks of duplicated code whenever possible. For example, if several methods in a class require the same task, like a search or swap, you should extract the repeated code into a helper method. This is called **procedural abstraction** and is an example of top-down development within a class. This process of breaking a long method into a sequence of smaller tasks is sometimes called **stepwise refinement**.

### Information Hiding

Instance variables and helper methods are generally declared as private, which prevents client classes from accessing them. This strategy is called **information hiding**.

### Stub Method

Sometimes it makes more sense in the development of a class to test a calling method before testing a method it invokes. A **stub** is a dummy method that stands in for a method until the actual method as been written and tested. A stub will usually have an output statement or return reasonable values if necessary.

### Algorithm

An **algorithm** is a precise step by step procedure that solves a problem or achieves a goal.

# Program Analysis

## Program Correctness

Testing that a program works does not prove that the program is correct. After all, you can hardly expect to test programs for every conceivable set of input data. Computer scientists have developed mathematical techniques to prove correctness in certain cases but these are beyond the scope of the APCS course. Nevertheless, you are expected to be able to make assertions about the state of a program at various points during its execution.

## Assertions

An assertions is a precise statement about a program at any given point. The idea is that is an assertion is proved to be true then the program is working correctly at that point.

### Precondition

The **precondition** for any piece of code whatever it is a method, loop, or block, is a statement of what is true immediately before execution of that code.

### Postcondition

The **postcondition** for a piece of code is what is true immediately after the execution of the code.

## Efficiency

An efficient algorithm is one that is economical is in the use of CPU time and memory