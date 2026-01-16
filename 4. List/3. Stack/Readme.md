
---

## 📌 Stack in Java

### 🔹 What is Stack?

`Stack` is a **legacy class** in Java that represents a **Last In First Out (LIFO)** data structure.

* It **extends `Vector`**
* Inherits **thread-safety** from `Vector`
* Commonly used for **undo/redo**, **expression evaluation**, **function calls**, etc.

📦 Package: `java.util`

---

## 🔹 Stack Characteristics

| Feature           | Supported |
| ----------------- | --------- |
| Extends           | `Vector`  |
| Thread-safe       | ✅ Yes     |
| Ordering          | LIFO      |
| Allows duplicates | ✅ Yes     |
| Allows null       | ✅ Yes     |
| Legacy class      | ✅ Yes     |

---

## 🔹 Time Complexity (Stack)

| Operation | Complexity |
| --------- | ---------- |
| Push      | O(1)       |
| Pop       | O(1)       |
| Peek      | O(1)       |
| Search    | O(n)       |
| Space     | O(n)       |

---

## 🔹 Important Stack Methods

| Method             | Description                          |
| ------------------ | ------------------------------------ |
| `push(E e)`        | Inserts element at top               |
| `pop()`            | Removes and returns top element      |
| `peek()`           | Returns top element without removing |
| `isEmpty()`        | Checks if stack is empty             |
| `search(Object o)` | 1-based position from top            |

---

## 🧑‍💻 Java Program: Stack Implementation

```java
import java.util.Stack;

public class Main 
{
    public static void main(String[] args) 
    {

        // Creating a Stack
        Stack<Integer> stack = new Stack<>();

        // Push elements
        stack.push(10);
        stack.push(20);
        stack.push(30);
        stack.push(40);

        System.out.println("Stack: " + stack);

        // Peek top element
        System.out.println("Top element: " + stack.peek());

        // Pop element
        System.out.println("Popped element: " + stack.pop());

        // Stack after pop
        System.out.println("Stack after pop: " + stack);

        // Search element
        System.out.println("Position of 20: " + stack.search(20));

        // Check empty
        System.out.println("Is stack empty? " + stack.isEmpty());
    }
}
```

---

### 🔹 Sample Output

```
Stack: [10, 20, 30, 40]
Top element: 40
Popped element: 40
Stack after pop: [10, 20, 30]
Position of 20: 2
Is stack empty? false
```

---

## ⚠️ Modern Recommendation

Although `Stack` is thread-safe, **it is not recommended for new applications**.

✔ Prefer:

```java
Deque<Integer> stack = new ArrayDeque<>();
```

---
