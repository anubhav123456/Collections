# Java Collections – Deque & List Implementations

![JCF](pics/JCF1.jpg)
---

## 1. Deque (Double Ended Queue)

### What is Deque?

* Deque stands for **Double Ended Queue**.
* It extends the `Queue` interface.
* Allows **insertion and removal from both ends** (front & back).
* Can behave as:

  * Queue (FIFO)
  * Stack (LIFO)

---

### Queue vs Deque

| Queue             | Deque                     |
| ----------------- | ------------------------- |
| Insert at last    | Insert at first or last   |
| Remove from first | Remove from first or last |

---

### Methods Inherited from Queue

* `add()`
* `offer()`
* `poll()`
* `remove()`
* `peek()`
* `element()`

Default behavior:

* `add()` → internally calls `addLast()`
* `offer()` → internally calls `offerLast()`
* `poll()` → internally calls `pollFirst()`
* `remove()` → internally calls `removeFirst()`
* `peek()` → internally calls `peekFirst()`

So **if you use normal Queue methods, Deque behaves like a Queue**.

---

### New Methods Introduced in Deque

#### Insertion

| Method         | Behavior                                 |
| -------------- | ---------------------------------------- |
| `addFirst()`   | Adds at front, throws exception if fails |
| `offerFirst()` | Adds at front, returns true/false        |
| `addLast()`    | Adds at back, throws exception           |
| `offerLast()`  | Adds at back, returns true/false         |

#### Removal

| Method          | Behavior                             |
| --------------- | ------------------------------------ |
| `removeFirst()` | Removes front, throws exception      |
| `pollFirst()`   | Removes front, returns null if empty |
| `removeLast()`  | Removes back, throws exception       |
| `pollLast()`    | Removes back, returns null if empty  |

#### Examination (No Removal)

| Method        | Behavior                        |
| ------------- | ------------------------------- |
| `getFirst()`  | Returns front, throws exception |
| `peekFirst()` | Returns front, null if empty    |
| `getLast()`   | Returns last, throws exception  |
| `peekLast()`  | Returns last, null if empty     |

---

### Using Deque as Stack

* Stack = LIFO (Last In First Out)

Mapping:

* `push()` → internally calls `addFirst()`
* `pop()` → internally calls `removeFirst()`

Example:

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1);
stack.push(2);
stack.push(3);

System.out.println(stack.pop()); // 3
System.out.println(stack.pop()); // 2
```

---

## 2. ArrayDeque

### What is ArrayDeque?

* Concrete class implementing `Deque`
* Uses **resizable array** internally
* Faster than `Stack`
* Can be used as **Queue or Stack**

---

### Using ArrayDeque as Queue

```java
Deque<Integer> dq = new ArrayDeque<>();

dq.addLast(1);
dq.addLast(5);
dq.addLast(10);

System.out.println(dq.pollFirst()); // 1
System.out.println(dq.pollFirst()); // 5
System.out.println(dq.pollFirst()); // 10
```

---

### Using ArrayDeque as Stack

```java
Deque<Integer> dq = new ArrayDeque<>();

dq.addFirst(1);
dq.addFirst(5);
dq.addFirst(10);

System.out.println(dq.removeFirst()); // 10
System.out.println(dq.removeFirst()); // 5
System.out.println(dq.removeFirst()); // 1
```

---

### Time & Space Complexity (ArrayDeque)

| Operation           | Complexity     |
| ------------------- | -------------- |
| Insert (front/back) | O(1) amortized |
| Delete (front/back) | O(1)           |
| Peek                | O(1)           |
| Resize              | O(n)           |
| Space               | O(n)           |

* Initial capacity = 8
* Capacity doubles when full

---

### Properties

* Thread-safe ❌
* Maintains insertion order ✅
* Allows null ❌
* Allows duplicates ✅

---

### Thread-safe Version

```java
Deque<Integer> dq = new ConcurrentLinkedDeque<>();
```

* Safe for multi-threaded access

---

## 3. PriorityQueue vs ArrayDeque

| Feature             | PriorityQueue         | ArrayDeque            |
| ------------------- | --------------------- | --------------------- |
| Order               | Heap-based            | Insertion order       |
| Null allowed        | ❌                     | ❌                     |
| Thread-safe         | ❌                     | ❌                     |
| Thread-safe version | PriorityBlockingQueue | ConcurrentLinkedDeque |

---

## 4. List Interface

### What is List?

* Ordered collection
* Allows duplicate elements
* Index-based access
* Can insert/remove/access from **any position**

---

### List vs Queue

| Queue          | List          |
| -------------- | ------------- |
| FIFO           | Index-based   |
| Limited access | Random access |

---

### New Methods in List

#### Index-based Operations

```java
add(int index, E element)
addAll(int index, Collection<E> c)
get(int index)
set(int index, E element)
remove(int index)
```

#### Search

```java
indexOf(Object o)
lastIndexOf(Object o)
```

#### Iteration

```java
ListIterator<E> listIterator()
ListIterator<E> listIterator(int index)
```

#### SubList

```java
List<E> subList(int from, int to) // from inclusive, to exclusive
```

---

## 5. ArrayList

### Example

```java
List<Integer> list = new ArrayList<>();
list.add(0, 100);
list.add(1, 200);
list.add(2, 300);
```

---

### addAll at Index

```java
List<Integer> list1 = new ArrayList<>();
list1.add(100);
list1.add(200);

List<Integer> list2 = new ArrayList<>();
list2.add(400);
list2.add(500);

list1.addAll(1, list2);
```

---

### replaceAll (Functional Interface)

```java
list.replaceAll(val -> val * -1);
```

---

### Sorting

```java
list.sort((a, b) -> a - b); // Ascending
```

---

### Difference: add vs set

| add             | set              |
| --------------- | ---------------- |
| Shifts elements | Replaces element |

---

### ListIterator (Forward & Backward)

#### Forward Traversal

```java
ListIterator<Integer> it = list.listIterator();
while(it.hasNext()) {
    System.out.println(it.next());
}
```

#### Backward Traversal

```java
ListIterator<Integer> it = list.listIterator(list.size());
while(it.hasPrevious()) {
    System.out.println(it.previous());
}
```

---

### Time Complexity (ArrayList)

| Operation    | Complexity     |
| ------------ | -------------- |
| Add at end   | O(1) amortized |
| Add at index | O(n)           |
| Remove       | O(n)           |
| Get by index | O(1)           |
| Space        | O(n)           |

---

### Properties

* Thread-safe ❌
* Maintains order ✅
* Allows null ✅
* Allows duplicates ✅

---

### Thread-safe Version

```java
List<Integer> list = new CopyOnWriteArrayList<>();
```

---

## 6. LinkedList

### Features

* Implements `List` + `Deque`
* Doubly linked list internally
* Supports index-based and deque operations

---

### Example

```java
LinkedList<Integer> list = new LinkedList<>();
list.addLast(200);
list.addLast(300);
list.addFirst(100);

System.out.println(list.getFirst()); // 100
```

---

### Index-based Operations

```java
list.add(1, 200);
System.out.println(list.get(1)); // 200
```

---

### Time Complexity (LinkedList)

| Operation             | Complexity |
| --------------------- | ---------- |
| Add/remove first/last | O(1)       |
| Add/remove at index   | O(n)       |
| Search                | O(n)       |
| Space                 | O(n)       |

---

### Properties

* Thread-safe ❌
* Maintains order ✅
* Allows null ✅
* Allows duplicates ✅

---

## 7. Vector

### What is Vector?

* Thread-safe version of ArrayList
* All methods are synchronized
* Slower due to locking

```java
Vector<Integer> v = new Vector<>();
v.add(10);
v.add(20);
```

---

### Properties

* Thread-safe ✅
* Maintains order ✅
* Allows null ✅
* Allows duplicates ✅

---

## 8. Stack

### Stack Characteristics

* Extends Vector
* Thread-safe
* LIFO behavior

```java
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);

System.out.println(stack.pop()); // 3
```

---

### Time Complexity (Stack)

| Operation | Complexity |
| --------- | ---------- |
| Push      | O(1)       |
| Pop       | O(1)       |
| Search    | O(n)       |
| Space     | O(n)       |

---

## Final Summary

* **Deque** → Queue + Stack behavior
* **ArrayDeque** → Fast, non-thread-safe
* **ConcurrentLinkedDeque** → Thread-safe Deque
* **ArrayList** → Fast random access
* **LinkedList** → Fast insert/delete
* **Vector & Stack** → Thread-safe but slower

---

