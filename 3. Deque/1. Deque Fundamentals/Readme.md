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



