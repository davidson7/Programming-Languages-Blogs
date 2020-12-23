What is Functional Programming?

Functional programming is built on mathematical functions and uses trees of expressions that each return a value (recursion)
	Extra: Even Types (aka data types) can be recursive. See https://www.haskell.org/tutorial/goodies.html Section 2.2.1 Recursive Types

The simplest example of recusive programming is the Fibonacci sequence.

		fib(0) = 0;
		fib(1) = 1;
		fib(n+2) = fib (n) + fib(n+1);

There are two base cases, fib(0) and fib(1). Base case(s) are needed so recusion isn't infinite. If there was no base case, fib() would continue to call itself into negative numbers, and the process would never end.
The third line is the inductive case, or the function which defines what fib() should do for all natural numbers that are not 0 or 1.


How is this different from other programming languages?
	
Languages like Java, Python and C++ are Imperative programming languages. The simplest way to illustrate imperative programming is as a series of steps or instructions. These instructions manipulate the memory or 'state' of the program, whic determines where the program should go next,  which modifies the state, etc.
Conversely, the value returned by a function is soley dependent on its input.
	

