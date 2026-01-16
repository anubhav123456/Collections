# ConcurrentLinkedDeque in Java

## Introduction

`ConcurrentLinkedDeque` is a **thread-safe**, **non-blocking**, and **lock-free** implementation of the **Deque** interface provided in the `java.util.concurrent` package. Internally, it is based on a **linked list** structure and is designed for **high concurrency scenarios**.

It is suitable when multiple threads need to **insert, remove, or access elements from both ends** of a deque concurrently.

---

## Key Characteristics

* Part of **Java Collection Framework**
* Package: `java.util.concurrent`
* Implements:

  * `Deque<E>`
  * `Queue<E>`
  * `Collection<E>`
* Extends:

  * `AbstractCollection<E>`
* Implements `Serializable`

### Important Properties

* ✅ **Thread-safe** for concurrent access
* ✅ **Lock-free & non-blocking** (uses CAS internally)
* ❌ **Does not allow null elements**
* ⚠️ `size()` is **NOT constant time** (O(n))
* 🔁 Iterators and spliterators are **weakly consistent**

  * They do **not throw ConcurrentModificationException**
  * They may reflect some, all, or none of the modifications made during iteration

---

## Why ConcurrentLinkedDeque?

* Better scalability than synchronized collections
* High throughput under heavy multi-threading
* Ideal for **producer-consumer**, **work-stealing**, and **task scheduling** use cases

---

## Class Hierarchy


![ConcurrentLinkedDequeinJava](pics/ConcurrentLinkedDequeinJava.png)

```
AbstractCollection
        ↑
      Deque
        ↑
      Queue
        ↑
ConcurrentLinkedDeque
```

---

## Declaration

```java
ConcurrentLinkedDeque<Type> deque = new ConcurrentLinkedDeque<>();
```

Where `Type` can be `Integer`, `String`, custom objects, etc.

---

## Constructors

| Constructor                              | Description                                                 |
| ---------------------------------------- | ----------------------------------------------------------- |
| `ConcurrentLinkedDeque()`                | Creates an empty deque                                      |
| `ConcurrentLinkedDeque(Collection<E> c)` | Creates a deque containing elements of the given collection |

---

## ConcurrentLinkedDeque Methods

### ➕ Add Methods

| Method                              |  Explanation                                                                            |
| ----------------------------------- | --------------------------------------------------------------------------------------- |
| `add(E e)`                          | Inserts the element at the **tail** of the deque; throws exception if it fails          |
| `addAll(Collection<? extends E> c)` | Adds **all elements of the given collection** to the tail of the deque                  |
| `addFirst(E e)`                     | Inserts the element at the **front (head)** of the deque                                |
| `addLast(E e)`                      | Inserts the element at the **end (tail)** of the deque                                  |
| `offer(E e)`                        | Inserts the element at the **tail**, returns `true/false` instead of throwing exception |
| `offerFirst(E e)`                   | Inserts the element at the **front**, returns status instead of exception               |
| `offerLast(E e)`                    | Inserts the element at the **end**, returns status instead of exception                 |

---

### ➖ Remove Methods

| Method             |          Explanation                                                          |
| ------------------ | ----------------------------------------------------------------------------- |
| `remove()`         | Removes and returns the **first element**; throws exception if deque is empty |
| `remove(Object o)` | Removes the **first occurrence** of the specified element                     |
| `removeFirst()`    | Removes and returns the **head element**; throws exception if empty           |
| `removeLast()`     | Removes and returns the **tail element**; throws exception if empty           |
| `poll()`           | Removes and returns the **first element**; returns `null` if empty            |
| `pollFirst()`      | Removes and returns the **head element**; returns `null` if empty             |
| `pollLast()`       | Removes and returns the **tail element**; returns `null` if empty             |

---

### 📥 Access Methods (Exception-Throwing)

| Method       |          Explanation                                                          |
| ------------ | ----------------------------------------------------------------------------- |
| `element()`  | Retrieves (without removing) the **head element**; throws exception if empty  |
| `getFirst()` | Retrieves (without removing) the **first element**; throws exception if empty |
| `getLast()`  | Retrieves (without removing) the **last element**; throws exception if empty  |

---

### 👀 Peek Methods (Safe / Null-Returning)

| Method        |          Explanation                                                        |
| ------------- | --------------------------------------------------------------------------- |
| `peek()`      | Retrieves (without removing) the **head element**; returns `null` if empty  |
| `peekFirst()` | Retrieves (without removing) the **first element**; returns `null` if empty |
| `peekLast()`  | Retrieves (without removing) the **last element**; returns `null` if empty  |

---

### 🔁 Iterator Methods

| Method                 |          Explanation                                           |
| ---------------------- | -------------------------------------------------------------- |
| `iterator()`           | Returns a **weakly consistent iterator** from **head to tail** |
| `descendingIterator()` | Returns a **weakly consistent iterator** from **tail to head** |

---

### ✅ Boolean Method

| Method               |          Explanation                                        |
| -------------------- | ----------------------------------------------------------- |
| `contains(Object o)` | Checks whether the deque **contains the specified element** |

---




## Basic Working Example

```java
// Java Program to demonstrate the working of ConcurrentLinkedDeque
import java.util.*;
import java.util.concurrent.ConcurrentLinkedDeque;

public class Main
{
    public static void main(String[] args)
    {
        Deque<Integer> d = new ConcurrentLinkedDeque<>();
        d.addFirst(1);
        d.addLast(2);
        int f = d.pollFirst();
        int l = d.pollLast();
        
        //First: 1, Last: 2
        System.out.println("First: " + f + ", Last: " + l);
    }
}
```

---

## Example: Using addFirst() and Copy Constructor

```java
// Java Program to demonstrates the working of addFirst()
import java.util.concurrent.*;

class Main 
{
    public static void main(String[] args) 
    {
        // Create a ConcurrentLinkedDeque
        ConcurrentLinkedDeque<Integer> d
                = new ConcurrentLinkedDeque<>();

        // Add elements to the front
        d.addFirst(10);
        d.addFirst(20);
        d.addFirst(30);
        d.addFirst(40);

        // Display the deque
        //Deque: [40, 30, 20, 10]
        System.out.println("Deque: " + d);

        // Create another ConcurrentLinkedDeque by copying
        ConcurrentLinkedDeque<Integer> d1
                = new ConcurrentLinkedDeque<>(d);
        
        // Deque Copy: [40, 30, 20, 10]
        System.out.println("Deque Copy: " + d1);
    }
}
```

---

## Example: Add, Peek & Remove Operations

```java
// Java Program to demonstrates addFirst(), peekLast(), peekFirst(),
// removeLast(), removeFirst()
import java.util.concurrent.*;
class Main 
{
    
    public static void main(String[] args)
    {
        ConcurrentLinkedDeque<Integer> d
                = new ConcurrentLinkedDeque<>();

        d.addFirst(10);
        d.addFirst(20);
        d.addFirst(30);
        d.addFirst(40);
        
        // Deque: [40, 30, 20, 10]
        System.out.println("Deque: " + d);
        
        //Last Element: 10
        System.out.println("Last Element: " + d.peekLast());
        
        //First Element: 40
        System.out.println("First Element: " + d.peekFirst());

        d.removeLast();
        //After removing last: [40, 30, 20]
        System.out.println("After removing last: " + d);

        d.removeFirst();
        //After removing first: [30, 20]
        System.out.println("After removing first: " + d);
    }
}
```

---

## Performing Various Operations

## 1. Adding Elements

Methods used:

* `add()`
* `addAll()`
* `addFirst()`
* `addLast()`

```java
// Add Elements in ConcurrentLinkedDeque
import java.util.concurrent.*;
class Main 
{

    public static void main(String[] args) 
    {
        
        ConcurrentLinkedDeque<Integer> d
        = new ConcurrentLinkedDeque<>();

        d.add(10);
        d.add(20);
        d.addFirst(30);

        System.out.println("Elements in d: " + d);

        ConcurrentLinkedDeque<Integer> d1
        = new ConcurrentLinkedDeque<>();

        d1.addAll(d);
        System.out.println("Elements in d1: " + d1);
    }
}
```

---

## 2. Removing Elements

Methods used:

* `remove()`
* `remove(Object)`
* `removeFirst()`
* `removeLast()`

```java
// Java Program to demonstrates removal operations
import java.util.concurrent.*;
class Main 
{
    
    public static void main(String[] args) 
    {

        ConcurrentLinkedDeque<Integer> d
        = new ConcurrentLinkedDeque<>();

        d.add(40);
        d.add(50);
        d.add(60);
        d.add(70);
        d.add(80);

        System.out.println("Deque: " + d);

        System.out.println("Removing first element: " + d.remove());
        System.out.println("60 removed?: " + d.remove(60));

        System.out.println("Deque after removal: " + d);

        d.removeFirst();
        d.removeLast();

        System.out.println("Deque after removing first and last: " + d);
    }
}
```

---

## 3. Iterating Elements

* `iterator()`
* `descendingIterator()`

```java
// Java Program to demonstrates iterator()
import java.util.concurrent.*;
import java.util.*;

public class Main 
{

    public static void main(String args[]) 
    {

        ConcurrentLinkedDeque<String> d
        = new ConcurrentLinkedDeque<>();

        d.add("Java");
        d.add("C++");
        d.add("Python");
        d.add("Js");

        System.out.println("Deque: " + d);

        Iterator<String> i = d.iterator();

        System.out.println("Iterating over elements:");
        while (i.hasNext()) {
            System.out.println(i.next());
        }
    }
}
```


```java
// Java Program to demonstrates descendingIterator()
import java.util.concurrent.*;
import java.util.*;

public class Main 
{

    public static void main(String args[]) 
    {

        ConcurrentLinkedDeque<String> d
        = new ConcurrentLinkedDeque<>();

        d.add("Java");
        d.add("C++");
        d.add("Python");
        d.add("Js");

        System.out.println("Deque: " + d);

        Iterator<String> i = d.descendingIterator();

        System.out.println("Iterating over elements:");
        while (i.hasNext()) {
            System.out.println(i.next());
        }
    }
}
```

---

## 4. Accessing Elements

Methods used:

* `getFirst()`
* `getLast()`
* `element()`

```java
// Java Program to demonstrates getFirst(), getLast() and element()
import java.util.*;
import java.util.concurrent.*;
class Main 
{
    public static void main(String[] args)
    {
        ConcurrentLinkedDeque<String> d
            = new ConcurrentLinkedDeque<>();

        d.add("Java");
        d.add("C++");
        d.add("Python");
        d.add("Js");

        System.out.println("Deque: " + d);

        System.out.println("First element: " + d.getFirst());
        System.out.println("Last element: " + d.getLast());
        System.out.println("Head of deque: " + d.element());
    }
}
```

---

## Time Complexity (Average)

| Operation                | Complexity |
| ------------------------ | ---------- |
| addFirst / addLast       | O(1)       |
| removeFirst / removeLast | O(1)       |
| peekFirst / peekLast     | O(1)       |
| size()                   | O(n)       |

---

## When to Use ConcurrentLinkedDeque

* Multiple threads adding/removing tasks
* Sliding window problems with concurrency
* Work-stealing algorithms
* High-performance, non-blocking systems

---

## Summary

`ConcurrentLinkedDeque` is a **powerful concurrent data structure** that provides **safe, fast, and scalable** double-ended queue operations without locking. It is a superior choice over synchronized deques in highly concurrent applications.

---