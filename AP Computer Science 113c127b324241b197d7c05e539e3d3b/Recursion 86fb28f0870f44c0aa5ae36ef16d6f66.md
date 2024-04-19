# Recursion

# Recursive Methods

A **recursive method** is a method that calls itself. For example, here is a program that calls a recursive method `stackWords`.

```java
public class WordPlay {
	public static void stackWords() {
		String word = IO.readString(); //read user input

		if (word.equals(".")) {
			System.out.println();
		} else {
			stackWords();
		}
		System.out.println(word);
	}

	public static void main(String args[]) {
		System.out.println("Enter list of words, one per line.");
		System.out.println("Final word should be a period (.)");
		stackWords();
	}
}
```

If you enter the input

```
hold
my
hand
.
```

The output will be

```
.
hand
my
hold
```

This happens because of the **call stack**. The computer keeps track of which methods to call via a **call stack**. This is a stack data structure which holds a **stack frame** for each function call. The first time `stackWords()` is called, the word `"hold"` is read. 

It then calls itself, which pushes another call of `stackWords()` on to the call stack, which repeats until a period is inputted. When a period is inputted, the period is printed and the current function call ends, which lets the previous statements on the stack be “popped off”

![Untitled](Recursion%2086fb28f0870f44c0aa5ae36ef16d6f66/Untitled.png)

Note that each time the function is called, a new local variable `word` is created.

# General Form of Simple Recursive Algorithms

Every recursive method has two distinct parts:

- A base case or termination condition that causes the to end without recursing.
- A non base case whose actions move the algorithm towards the base case (and therefore termination)

**Example One: Fibonacci**

```java
/**
* fibonacci
* calculates the nth fibonacci number
* @param n the term of the sequence
* @return the nth fibonacci number starting from 0
*/
public static int fibonacci(int n) {
	if (n <= 1) {
		return n;
	}

	return fibonacci(n - 1) + fibonacci(n - 2)
}
```

Note that for every recursive call we make, we reduce the size of the problem and get closer to the base case by subtracting.

# Writing Recursive Methods

To come up with a recursive algorithm, the programmer has to be able to frame a process recursively (i.e. in terms of a simpler case of itself). This is different from framing it iteratively, which repeats a process until a condition is met.

**Example One: Factorial**

$$
\begin{array}{ccc} \textnormal{n! defined iteratively}                                                                     & \textnormal{n! defined recursively} \\ \hline 0! = 1 & 0! = 1 \\ 1! = 1 & 1! = (1)(0!) \\ 2! = (2)(1) & 2! = (2)(1!) \\ 3! = (3)(2)(1) & 3!=(3)(2!) \\ ... & ...                                    
\end{array}
$$

# Analysis of Recursive Methods

Recall the Fibonacci sequence, 1, 1, 2, 3, 5, 8, 13, …. The nth Fibonacci number is the sum of the previous 2 is $n \ge 3$.