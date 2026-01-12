# Java Collections – Queue, PriorityQueue, Comparator & Comparable

![JCF](pics/JCF1.jpg)

---

## 1. Queue Interface

### What is a Queue?

* Queue follows **FIFO (First In, First Out)** principle.
* Elements are:

  * **Inserted at the rear (tail)**
  * **Removed from the front (head)**
* Real-life analogy: Movie ticket queue.

### Queue Characteristics

* Queue is an **interface**
* Child of **Collection interface**
* Supports all Collection methods + extra queue-specific methods

---

## 2. Queue Methods (Very Important for Interviews)

Queue provides **6 additional methods**:

| Method    | Behavior                  | If Queue is Empty | If Insertion Fails |
| --------- | ------------------------- | ----------------- | ------------------ |
| add(e)    | Inserts element           | —                 | Throws exception   |
| offer(e)  | Inserts element           | —                 | Returns false      |
| poll()    | Removes & returns head    | Returns null      | —                  |
| remove()  | Removes & returns head    | Throws exception  | —                  |
| peek()    | Returns head (no removal) | Returns null      | —                  |
| element() | Returns head (no removal) | Throws exception  | —                  |

### Key Differences

* **add vs offer** → exception vs false
* **poll vs remove** → null vs exception
* **peek vs element** → null vs exception

---

## 3. PriorityQueue

### What is PriorityQueue?

* A special type of Queue
* **Does NOT follow FIFO strictly**
* Elements are ordered based on **priority**

### Internal Data Structure

* Uses **Heap** internally

  * Min Heap (default)
  * Max Heap (using Comparator)

### When to Use PriorityQueue?

* Whenever a **Heap** is required
* DSA problems like:

  * Kth largest/smallest element
  * Heap-based problems

---

## 4. Min Priority Queue (Default)

### Code Example

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();

pq.add(5);
pq.add(2);
pq.add(8);
pq.add(1);

while (!pq.isEmpty()) {
    System.out.print(pq.poll() + " ");
}
```

### Output

```
1 2 5 8
```

### Explanation

* Default ordering = **Natural Ordering**
* For Integer → Ascending order
* Hence, behaves like a **Min Heap**

---

## 5. Max Priority Queue (Using Comparator)

### Code Example

```java
PriorityQueue<Integer> maxPQ = new PriorityQueue<>((a, b) -> b - a);

maxPQ.add(5);
maxPQ.add(2);
maxPQ.add(8);
maxPQ.add(1);

while (!maxPQ.isEmpty()) {
    System.out.print(maxPQ.poll() + " ");
}
```

### Output

```
8 5 2 1
```

### Explanation

* Comparator reverses natural ordering
* Behaves like a **Max Heap**

---

## 6. Time Complexity of PriorityQueue

| Operation            | Time Complexity |
| -------------------- | --------------- |
| add / offer          | O(log N)        |
| poll / remove (head) | O(log N)        |
| peek                 | O(1)            |
| remove(object)       | O(N)            |

---

## 7. Need for Comparator & Comparable

### Problems Without Comparator/Comparable

1. Sorting in **descending order**
2. Sorting **custom objects**

Example issue:

```java
Arrays.sort(carArray); // Throws ClassCastException
```

Reason:

* JVM doesn’t know **how to compare objects**

---

## 8. Comparator

### What is Comparator?

* A **functional interface**
* Used to define **custom sorting logic externally**

### Method

```java
int compare(T o1, T o2);
```

### Rules

* Return > 0 → swap
* Return = 0 → equal
* Return < 0 → no swap

---

## 9. Comparator with Primitive Wrapper

### Ascending Order

```java
Arrays.sort(arr, (a, b) -> a - b);
```

### Descending Order

```java
Arrays.sort(arr, (a, b) -> b - a);
```

---

## 10. Comparator with Custom Object (Car)

### Car Class

```java
class Car {
    String name;
    String type;

    Car(String name, String type) {
        this.name = name;
        this.type = type;
    }
}
```

### Sort by Car Type (Descending)

```java
Arrays.sort(carArray, (c1, c2) -> c2.type.compareTo(c1.type));
```

### Sort by Car Name (Ascending)

```java
Arrays.sort(carArray, (c1, c2) -> c1.name.compareTo(c2.name));
```

---

## 11. Comparator Using Separate Class

```java
class CarNameDescComparator implements Comparator<Car> {
    public int compare(Car c1, Car c2) {
        return c2.name.compareTo(c1.name);
    }
}
```

### Usage

```java
Collections.sort(carList, new CarNameDescComparator());
```

---

## 12. Comparable

### What is Comparable?

* Interface implemented by the **object itself**
* Provides **natural ordering**

### Method

```java
int compareTo(T o);
```

---

## 13. Comparable Example (Car)

```java
class Car implements Comparable<Car> {
    String name;
    String type;

    Car(String name, String type) {
        this.name = name;
        this.type = type;
    }

    @Override
    public int compareTo(Car other) {
        return this.type.compareTo(other.type); // ascending
    }
}
```

### Sorting

```java
Collections.sort(carList);
```

---

## 14. Comparator vs Comparable (Interview Gold)

| Feature              | Comparator              | Comparable   |
| -------------------- | ----------------------- | ------------ |
| Package              | java.util               | java.lang    |
| Method               | compare(o1, o2)         | compareTo(o) |
| Location             | Separate class / lambda | Same class   |
| Multiple sorting     | Yes                     | No           |
| Modify class needed  | No                      | Yes          |
| Asc/Desc flexibility | Yes                     | No           |

---

## 15. Key Takeaways

* **Queue** → FIFO structure
* **PriorityQueue** → Heap-based (Min/Max)
* **Comparator** → External, flexible sorting
* **Comparable** → Internal, fixed sorting
* Prefer **Comparator** for real-world applications

---

✅ Very frequently asked interview topic
✅ Practice with custom objects

---
