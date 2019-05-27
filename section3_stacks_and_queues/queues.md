# The Queue Data Structure
Good resource to read: https://www.geeksforgeeks.org/queue-data-structure/

## When is it best to use a queue?
A Queue is a linear structure which follows a particular order in which the operations are performed. The order is First In First Out (FIFO). A good example of a queue is any queue of consumers for a resource where the consumer that came first is served first. The difference between stacks and queues is in removing. In a stack we remove the item the most recently added; in a queue, we remove the item the least recently added.

## Implementation of a Queue via Array
```java
// Java program to implement a queue using an array 
class Queue { 
	private static int front, rear, capacity; 
	private static int queue[]; 

Queue(int c) { 
	front = rear = 0; 
	capacity = c; 
	queue = new int[capacity]; 
} 

// function to insert an element 
// at the rear of the queue 
static void queueEnqueue(int data) { 
	// check queue is full or not 
	if (capacity == rear) { 
		System.out.printf("\nQueue is full\n"); 
		return; 
	} else { // insert element at the rear
		queue[rear] = data; 
		rear++; 
	} 
	return; 
} 

// function to delete an element 
// from the front of the queue 
static void queueDequeue() { 
	// if queue is empty 
	if (front == rear) { 
		System.out.printf("\nQueue is empty\n"); 
		return; 
	} else { 
		// shift all the elements from index 2 till rear 
		// to the right by one 
		for (int i = 0; i < rear - 1; i++) { 
			queue[i] = queue[i + 1]; 
		} 

		// store 0 at rear indicating there's no element 
		if (rear < capacity) 
			queue[rear] = 0; 

		// decrement rear 
		rear--; 
	} 
	return; 
} 

// print queue elements 
static void queueDisplay() { 
	int i; 
	if (front == rear) { 
		System.out.printf("\nQueue is Empty\n"); 
		return; 
	} 

	// traverse front to rear and print elements 
	for (i = front; i < rear; i++) { 
		System.out.printf(" %d <-- ", queue[i]); 
	} 
	return; 
} 

	// print front of queue 
	static void queueFront() { 
	if (front == rear) { 
		System.out.printf("\nQueue is Empty\n"); 
		return; 
	} 
	System.out.printf("\nFront Element is: %d", queue[front]); 
	return; 
	} 
} 

public class StaticQueueinjava { 

// Driver code 
public static void main(String[] args) { 
	// Create a queue of capacity 4 
	Queue q = new Queue(4); 

	// print Queue elements 
	q.queueDisplay(); 

	// inserting elements in the queue 
	q.queueEnqueue(20); 
	q.queueEnqueue(30); 
	q.queueEnqueue(40); 
	q.queueEnqueue(50); 

	// print Queue elements 
	q.queueDisplay(); 

	// insert element in the queue 
	q.queueEnqueue(60); 

	// print Queue elements 
	q.queueDisplay(); 

	q.queueDequeue(); 
	q.queueDequeue(); 
	System.out.printf("\n\nafter two node deletion\n\n"); 

	// print Queue elements 
	q.queueDisplay(); 

	// print front of the queue 
	q.queueFront(); 
	} 
} 

```
The time complexity of the Array implementation are O(1) for insertion, but O(N) for deletion (moving all elements over). We can look to improve that with other implementations.

## LinkedList Implementation of a Queue

```java
// Java program for linked-list implementation of queue 

// A linked list (LL) node to store a queue entry 
class QNode { 
	int key; 
	QNode next; 
	
	// constructor to create a new linked list node 
	public QNode(int key) { 
		this.key = key; 
		this.next = null; 
	} 
} 

// A class to represent a queue 
//The queue, front stores the front node of LL and rear stores the 
//last node of LL 
class Queue { 
	QNode front, rear; 
	
	public Queue() { 
		this.front = this.rear = null; 
	} 
	
	// Method to add an key to the queue. 
	void enqueue(int key) { 
		
		// Create a new LL node 
		QNode temp = new QNode(key); 
	
		// If queue is empty, then new node is front and rear both 
		if (this.rear == null) { 
			this.front = this.rear = temp; 
			return; 
		} 
	
		// Add the new node at the end of queue and change rear 
		this.rear.next = temp; 
		this.rear = temp; 
	} 
	
	// Method to remove an key from queue. 
	QNode dequeue() { 
		// If queue is empty, return NULL. 
		if (this.front == null) 
			return null; 
	
		// Store previous front and move front one node ahead 
		QNode temp = this.front; 
		this.front = this.front.next; 
	
		// If front becomes NULL, then change rear also as NULL 
		if (this.front == null) 
			this.rear = null; 
		return temp; 
	} 
} 

	
// Driver class 
public class Test { 
	public static void main(String[] args) { 
		Queue q=new Queue(); 
		q.enqueue(10); 
		q.enqueue(20); 
		q.dequeue(); 
		q.dequeue(); 
		q.enqueue(30); 
		q.enqueue(40); 
		q.enqueue(50); 
		
		System.out.println("Dequeued item is "+ q.dequeue().key); 
	} 
} 
// This code is contributed by Gaurav Miglani 
```
Time Complexity: Time complexity of both operations enqueue() and dequeue() is O(1) as we only change few pointers in both operations. There is no loop in any of the operations.

## How Do I Use a Queue?
```java
Queue<T> q = new LinkedList<T>();
```
We can instantiate a Queue as such so that the `enqueue()` and `dequeue()` operations are both O(1). 
