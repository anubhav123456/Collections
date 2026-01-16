
---

## 📌 ArrayDeque (Java)

### What is ArrayDeque?

* `ArrayDeque` is a **resizable array implementation of the Deque interface**
* Part of **`java.util` package**
* Implements **Deque**, so it can work as:

  * Queue (FIFO)
  * Stack (LIFO)
  * Double Ended Queue

---

### Key Characteristics

* ✅ **Resizable array** (no fixed capacity)
* ✅ **No capacity restriction** (grows automatically)
* ❌ **Not thread-safe**
* ❌ **Does NOT allow null elements**
* 🚀 **Faster than Stack and LinkedList** in most cases

  * Better cache locality
  * No node/object overhead like LinkedList

---

### Declaration

```java
Deque<Integer> dq = new ArrayDeque<>();
```

---

## 📌 ArrayDeque as Queue (FIFO)

### Queue Behavior

* **Insert at rear**
* **Remove from front**
* Follows **FIFO (First In First Out)**

---

### Common Queue Methods

| Operation | Method    |
| --------- | --------- |
| Add       | `offer()` |
| Remove    | `poll()`  |
| Peek      | `peek()`  |

---

### Example

```java
Queue<Integer> q = new ArrayDeque<>();

q.offer(10);
q.offer(20);
q.offer(30);

System.out.println(q.poll()); // 10
System.out.println(q.peek()); // 20
```

---

### Internal Flow (FIFO)

```
10 → 20 → 30
↑
removed first
```

* `poll()` removes **10** (front element)
* `peek()` shows **20** (new front)

---

### ✅ When to Use ArrayDeque as Queue

* When you need a **simple FIFO queue**
* When performance matters
* Prefer it over:

  * `LinkedList` (slower due to node traversal)
  * `Stack` (legacy + synchronized overhead)

---

### 🔥 Interview One-Liner

> **ArrayDeque is the fastest general-purpose Queue implementation in Java when thread safety is not required.**

---