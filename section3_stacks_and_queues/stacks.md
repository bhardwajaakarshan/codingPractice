# The Stack Data Structure
Good resource to read: https://www.geeksforgeeks.org/stack-data-structure/

## When is it best to use a stack?
Stack is a linear data structure which follows a particular order in which the operations are performed.There are many real-life examples of a stack. Consider an example of plates stacked over one another in the canteen. The plate which is at the top is the first one to be removed, i.e. the plate which has been placed at the bottommost position remains in the stack for the longest period of time. So, it can be simply seen to follow LIFO(Last In First Out) order.

## Implementation of a Stack
```java
/* Java program to implement basic stack operations */
class Stack { 
	static final int MAX = 1000; 
	int top; 
	int a[] = new int[MAX]; // Maximum size of Stack 

	boolean isEmpty() { 
		return (top < 0);
	} 

	Stack() { 
		top = -1; 
	} 

	boolean push(int x) { 
		if (top >= (MAX-1)) { 
			System.out.println("Stack Overflow"); 
			return false; 
		} else { 
			a[++top] = x; 
			System.out.println(x + " pushed into stack"); 
			return true; 
		} 
	} 

	int pop() { 
		if (top < 0) { 
			System.out.println("Stack Underflow"); 
			return 0; 
		} else { 
			int x = a[top--]; 
			return x; 
		} 
	} 
} 

// Driver code 
class Main { 
	public static void main(String args[]) { 
		Stack s = new Stack(); 
		s.push(10); 
		s.push(20); 
		s.push(30); 
		System.out.println(s.pop() + " Popped from stack"); 
	} 
} 
```

## How Do I Use a Stack?
```java
Stack<T> stack = new Stack<T>();
```
Is how you can instantiate a stack that expects data-type T. For primitive, this is the wrapper class (Integer, Character, Double, etc.)
