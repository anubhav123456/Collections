
---

# 📌 ArrayDeque in Java

## 🔹 What is ArrayDeque?

* **Part of:** `java.util`
* **Implements:** `Deque` (Double Ended Queue)
* **Internal structure:** **Resizable circular array**
* **Capacity:** No fixed size (grows dynamically)
* **Thread safety:** ❌ Not thread-safe
* **Null elements:** ❌ Not allowed
* **Performance:** 🚀 Faster than `Stack` and `LinkedList` in most cases

```java
Deque<Integer> dq = new ArrayDeque<>();
```

---

## 🔹 Why ArrayDeque is Fast?

* No node creation (unlike `LinkedList`)
* No synchronization overhead (unlike `Stack`)
* Uses **contiguous memory** → better cache locality
* O(1) amortized time for add/remove at both ends

---

## 🔹 ArrayDeque as Double Ended Queue (Deque)

You can **insert and remove elements from both ends**.

### 🔸 Deque Operations

| Operation | Front           | Rear           |
| --------- | --------------- | -------------- |
| Add       | `addFirst()`    | `addLast()`    |
| Remove    | `removeFirst()` | `removeLast()` |
| Peek      | `peekFirst()`   | `peekLast()`   |

---

## 🔹 Example: Basic Deque Operations

```java
Deque<Integer> dq = new ArrayDeque<>();

dq.addFirst(20);
dq.addLast(30);
dq.addFirst(10);

System.out.println(dq); // [10, 20, 30]

dq.removeLast(); // removes 30
```

### 📌 Internal Structure

```
Front → 10 | 20 | 30 ← Rear
```
---

## 🔹 Comparison Summary

| Feature      | ArrayDeque | LinkedList         | Stack  |
| ------------ | ---------- | ------------------ | ------ |
| Backed by    | Array      | Doubly Linked List | Vector |
| Performance  | 🚀 Fastest | Slower             | Slow   |
| Thread-safe  | ❌          | ❌                  | ✔      |
| Null allowed | ❌          | ✔                  | ✔      |
| Recommended  | ✅ YES      | ❌                  | ❌      |

---

## 🧠 Interview One-Liner

> **ArrayDeque is a resizable array-based implementation of Deque that provides faster stack and queue operations than Stack and LinkedList.**

---
