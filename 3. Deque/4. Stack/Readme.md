
---

# 📌 ArrayDeque in Java

## 🔹 What is ArrayDeque?

* Part of **`java.util`**
* A **resizable array implementation** of the **Deque (Double Ended Queue)** interface
* Supports insertion & removal from **both ends**

```java
Deque<Integer> dq = new ArrayDeque<>();
```

---

## 🔹 Key Characteristics

* ✅ **Resizable** (no fixed capacity)
* ✅ **No capacity restriction**
* ❌ **Not thread-safe**
* ❌ **Does NOT allow null elements**
* 🚀 **Faster than Stack and LinkedList** in most cases

---

## 🔹 Why is ArrayDeque Fast?

* Uses **contiguous array** (better cache locality)
* No synchronization overhead
* No node allocation like LinkedList
* Amortized **O(1)** operations

---

# 📌 ArrayDeque as Stack (LIFO)

⚠️ **Java-recommended replacement for legacy `Stack` class**

---

## 🔹 Stack vs Deque Methods Mapping

| Stack Operation | Deque Method |
| --------------- | ------------ |
| `push()`        | `push()`     |
| `pop()`         | `pop()`      |
| `peek()`        | `peek()`     |

---

## 🔹 Example: Using ArrayDeque as Stack

```java
Deque<Integer> stack = new ArrayDeque<>();

stack.push(10);
stack.push(20);
stack.push(30);

System.out.println(stack.pop());   // 30
System.out.println(stack.peek());  // 20
```

---

## 🔹 Internal Flow (LIFO)

```
30  ← top
20
10
```

---

## 🔹 Use Cases (Stack via ArrayDeque)

✅ Use when:

* Function calls
* Undo / Redo operations
* DFS (Depth First Search)
* Expression evaluation
* Backtracking problems

---

# ❌ Why NOT use Stack class?

| Stack               | ArrayDeque              |
| ------------------- | ----------------------- |
| Legacy class        | Modern                  |
| Synchronized (slow) | Non-synchronized (fast) |
| Extends `Vector`    | Cleaner design          |
| Poor performance    | High performance        |

---

## 📌 Official Java Recommendation

> **Java documentation recommends using `ArrayDeque` instead of `Stack`.**

---

## 🔑 One-Line Interview Summary

> **ArrayDeque is a modern, high-performance replacement for Stack and LinkedList when stack behavior is required.**

---
