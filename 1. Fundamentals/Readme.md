# Java Collection Framework

---

## 1. What is Java Collection Framework (JCF)?

### What is a Collection?

* A **collection** is a **group of objects** (also called elements).
* Example: An array holding integers is also a collection.
* All collection-related classes and interfaces are present in **`java.util` package**.

### What is a Framework?

* A **framework** provides a **predefined architecture**.
* It consists of:

  * Interfaces
  * Classes
  * Methods
  * Ready-made functionality
* JCF provides built-in support for:

  * Add
  * Update
  * Delete
  * Search
  * Traverse elements

### Definition

> **Java Collection Framework** is a unified architecture that represents and manipulates a group of objects using predefined interfaces and classes.

### Java Version

* Introduced in **Java 1.2**

---

## 2. Why Do We Need Java Collection Framework?

### Before JCF (Pre-Java 1.2)

Available collections:

* Array
* Vector
* Hashtable

### Problem Before JCF

* No **common interface**
* Different syntax for:

  * Insertion
  * Retrieval
  * Removal
* Hard to remember APIs

### Example Without Common Interface

#### Array Example

```java
int[] arr = new int[4];
arr[0] = 1;
System.out.println(arr[0]);
```

#### Vector Example

```java
Vector<Integer> vector = new Vector<>();
vector.add(1);
System.out.println(vector.get(0));
```

➡ Different ways to **read/write** elements

### Solution by JCF

* Introduced **common interfaces**
* Same method names across collections
* Focus shifts from *how to use* → *which collection to use*

---

## 3. Java Collection Framework Hierarchy

### Two Major Categories

1. **Iterable → Collection** hierarchy
2. **Map** (separate hierarchy)

![JCF](pics/JCF1.jpg)
![JCF](pics/JCF2.jpg)

### Important Points

* **Map is NOT a child of Collection**
* Collection-based classes share common behavior

---

## 4. Iterable Interface

### Purpose

* Used to **traverse a collection**

### Java Version

* Added in **Java 1.5**

### Methods

* `iterator()` → Java 1.5
* `forEach()` → Java 1.8

---

## 5. Iteration Techniques



---

### 1️⃣ Using Iterator

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class Main
{
    public static void main(String[] args)
    {
        List<Integer> values = new ArrayList<>();
        values.add(1);
        values.add(2);
        values.add(3);
        values.add(4);

        Iterator<Integer> iterator = values.iterator();

        while (iterator.hasNext())
        {
            int value = iterator.next();
            System.out.println(value);

            if(value == 3)
            {
                iterator.remove();
            }
        }

        System.out.println(values); // [1, 2, 4]

    }
}
```

#### Iterator Methods

* `hasNext()` → checks if elements remain
* `next()` → returns next element
* `remove()` → removes last returned element
---

### 2️⃣ Enhanced For Loop

```java
import java.util.ArrayList;
import java.util.List;

public class Main
{
    public static void main(String[] args)
    {
        List<Integer> values = new ArrayList<>();
        values.add(1);
        values.add(2);
        values.add(3);
        values.add(4);

        for(Integer value : values)
        {
            System.out.println(value);
        }

    }
}
```

✔ Works because Collection implements **Iterable**

---

### 3️⃣ forEach() Method (Java 1.8)

```java
import java.util.ArrayList;
import java.util.List;

public class Main
{
    public static void main(String[] args)
    {
        List<Integer> values = new ArrayList<>();
        values.add(1);
        values.add(2);
        values.add(3);
        values.add(4);

       //values.forEach(System.out::println); or
       values.forEach(val -> System.out.println(val));

    }
}
```

* Uses **lambda expression**
* Internally uses `Consumer<T>` functional interface

---

## 6. Collection Interface

### Purpose

* Represents a group of objects
* Defines common operations

### Java Version

* Added in **Java 1.2**

---

## 7. Commonly Used Collection Methods

### Method Summary

| Method           | Description                                                                                       | Java Version Introduced |
| ---------------- | ------------------------------------------------------------------------------------------------- | ----------------------- |
| size()           | Number of elements                                                                                | Java 1.2                |
| isEmpty()        | Checks if empty                                                                                   | Java 1.2                |
| contains()       | Search element                                                                                    | Java 1.2                |
| add()            | Insert element                                                                                    | Java 1.2                |
| remove()         | Remove element                                                                                    | Java 1.2                |
| addAll()         | Add another collection                                                                            | Java 1.2                |
| removeAll()      | Remove common elements                                                                            | Java 1.2                |
| containsAll()    | Check full collection presence                                                                    | Java 1.2                |
| clear()          | Remove all elements                                                                               | Java 1.2                |
| iterator()       | Iterate elements                                                                                  | Java 1.2                |
| forEach()        | Performs the given action for each element of the collection using a lambda expression            | Java 1.8                |
| equals()         | Compare collections *(Object override)*                                                           | Java 1.2                |
| toArray()        | Converts collection into an array (`Object[]` or typed array)                                     | Java 1.2                |
| stream()         | Creates a sequential stream to process collection elements one by one using functional operations | Java 1.8                |
| parallelStream() | Creates a parallel stream to process collection elements concurrently using multiple threads      | Java 1.8                |



---

## 8. Collection Methods – Code Example

```java
import java.util.ArrayList;
import java.util.List;

public class Main
{
    public static void main(String[] args)
    {
        List<Integer> values = new ArrayList<>();
        values.add(1);
        values.add(2);
        values.add(3);
        values.add(4);

        System.out.println(values.size()); // 4
        System.out.println(values.isEmpty()); // false
        System.out.println(values.contains(100)); // false

        Integer[] arr1 = values.toArray(new Integer[0]);
        int[] arr2 = values.stream().mapToInt(Integer::intValue).toArray();
        for(int i : arr1)
        {
            System.out.print(i + " "); // 1 2 3 4
        }

        System.out.println();

        for(int i : arr2)
        {
            System.out.print(i + " "); // 1 2 3 4
        }

        System.out.println();

        values.add(100);
        System.out.println(values); // [1, 2, 3, 4, 100]

        //remove from ith index
        values.remove(4);
        System.out.println(values); //[1, 2, 3, 4]

        values.add(100);
        //remove value from list
        values.remove(Integer.valueOf(100));
        System.out.println(values); //[1, 2, 3, 4]

        List<Integer> list = new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);
        list.add(40);

        values.addAll(list);
        System.out.println(values); //[1, 2, 3, 4, 10, 20, 30, 40]

        values.removeAll(list);
        System.out.println(values); // [1, 2, 3, 4]

        values.add(20);
        values.add(10);
        values.add(40);
        values.add(30);

        System.out.println(values.containsAll(list)); // true

        values.removeAll(list);
        list.clear();
        System.out.println(values); // [1, 2, 3, 4]
        System.out.println(list); // []

        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);

        System.out.println(values.equals(list)); // true

        list.clear();

        list.add(2);
        list.add(4);
        list.add(1);
        list.add(3);

        System.out.println(values.equals(list)); // false

    }
}
```


---

## 9. Power of Collection Framework

* Same method names across all collections
* Easy to remember
* Focus on **use-case**, not syntax

Example:

```java
list.add();
stack.add();
queue.add();
```

---

## 10. Collection vs Collections

### Collection (No 's')

* Interface
* Part of JCF
* Represents a group of objects

### Collections (With 's')

* Utility class
* Contains only **static methods**
* Helps operate on collections

---

## 11. Collections Utility Methods

```java
import java.util.ArrayList;
import java.util.Collection;
import java.util.Collections;
import java.util.List;

public class Main
{
    public static void main(String[] args)
    {

        List<Integer> values = new ArrayList<>();
        values.add(4);
        values.add(1);
        values.add(3);
        values.add(2);

        // sort
        Collections.sort(values);
        System.out.println("Sorted: " + values); // Sorted: [1, 2, 3, 4]

        // binarySearch (list must be sorted)
        int index = Collections.binarySearch(values, 3);
        System.out.println("Index of 3: " + index); // Index of 3: 2

        // get (List method, NOT Collections)
        //Element at index 1: 2
        System.out.println("Element at index 1: " + values.get(1));

        // reverse
        Collections.reverse(values);
        //Reversed: [4, 3, 2, 1]
        System.out.println("Reversed: " + values);

        // shuffle
        Collections.shuffle(values);
        //Shuffled: [3, 4, 1, 2]
        System.out.println("Shuffled: " + values);

        // swap
        Collections.swap(values, 0, 2);
        //After swap(0,2): [1, 4, 3, 2]
        System.out.println("After swap(0,2): " + values);

        // copy
        List<Integer> dest = new ArrayList<>();
        dest.add(0);
        dest.add(0);
        dest.add(0);
        dest.add(0);

        Collections.copy(dest, values);
        //Copied list: [1, 4, 3, 2]
        System.out.println("Copied list: " + dest);

        // min
        //Min value: 1
        System.out.println("Min value: " + Collections.min(values));

        // max
        // Max value: 4
        System.out.println("Max value: " + Collections.max(values));

        List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        list.add(5);

        // rotate -> rotation towards right
        Collections.rotate(list, 2);
        //After rotate by 2: [4, 5, 1, 2, 3]
        System.out.println("After rotate by 2: " + list);

        // rotate <- rotation towards left
        Collections.rotate(list, -2);
        //After rotate by -2: [1, 2, 3, 4, 5]
        System.out.println("After rotate by -2: " + list);

        // unmodifiableCollection
        Collection<Integer> unmodifiable =
                Collections.unmodifiableCollection(values);

        // Unmodifiable collection: [3, 1, 4, 2]
        System.out.println("Unmodifiable collection: " + unmodifiable);

        // unmodifiable.add(10); ❌ throws UnsupportedOperationException
    }
}
```

---