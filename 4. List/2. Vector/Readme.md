
---

## 📌 Vector in Java

### 🔹 What is Vector?

`Vector` is a **legacy class** in Java that implements the `List` interface and is a **thread-safe version of `ArrayList`**.

* All its public methods are **synchronized**
* Ensures **thread safety** in multi-threaded environments
* **Slower** than `ArrayList` due to synchronization overhead

📦 Package: `java.util`

---

### 🔹 Key Properties of Vector

| Property                  | Supported               |
| ------------------------- | ----------------------- |
| Thread-safe               | ✅ Yes                   |
| Maintains insertion order | ✅ Yes                   |
| Allows `null` values      | ✅ Yes                   |
| Allows duplicate elements | ✅ Yes                   |
| Dynamic resizing          | ✅ Yes                   |
| Performance               | ❌ Slower than ArrayList |

---

### 🔹 Vector vs ArrayList (Quick Comparison)

| Feature       | Vector              | ArrayList            |
| ------------- | ------------------- | -------------------- |
| Thread Safety | Yes (synchronized)  | No                   |
| Performance   | Slower              | Faster               |
| Legacy Class  | Yes                 | No                   |
| Use Case      | Multi-threaded apps | Single-threaded apps |

---

### 🔹 Important Points

* Default capacity = **10**
* Capacity doubles when exceeded
* Rarely used in modern applications (prefer `Collections.synchronizedList()` or `CopyOnWriteArrayList`)

---

## 🧑‍💻 Java Program: Vector Implementation

```java
import java.util.Vector;

public class Main 
{
    public static void main(String[] args) 
    {

        // Creating a Vector
        Vector<String> vector = new Vector<>();

        // Adding elements
        vector.add("Java");
        vector.add("Python");
        vector.add("C++");
        vector.add("Java"); // duplicate allowed
        vector.add(null);   // null allowed

        // Printing Vector
        System.out.println("Vector elements: " + vector);

        // Accessing element
        System.out.println("Element at index 1: " + vector.get(1));

        // Removing element
        vector.remove("C++");
        System.out.println("After removal: " + vector);

        // Size of Vector
        System.out.println("Size: " + vector.size());

        // Checking thread-safe behavior (conceptual)
        synchronized (vector) {
            System.out.println("Thread-safe block executed");
        }
    }
}
```

---

### 🔹 Output (Sample)

```
Vector elements: [Java, Python, C++, Java, null]
Element at index 1: Python
After removal: [Java, Python, Java, null]
Size: 4
Thread-safe block executed
```

---

### ✅ When to Use Vector?

* ✔ When **thread safety is mandatory**
* ❌ Avoid in high-performance applications

---