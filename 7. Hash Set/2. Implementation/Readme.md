
---

# 📘 HashSet in Java – Internal Working

## 1️⃣ What is a HashSet?

`HashSet` is a class in Java that implements the **Set interface**.

### Key Characteristics:

* ✅ **Stores only unique elements**
* ❌ **Does not maintain insertion order**
* ⚙️ **Backed internally by a HashMap**
* ❌ **Not thread-safe**
* ⚡ Provides **O(1)** average time complexity for add, remove, and contains

---

## 2️⃣ Why do we use HashSet?

The **main reason** to use a `HashSet` is:

> 👉 **It guarantees uniqueness of elements**

No duplicate values are allowed.

---

## 3️⃣ Important Properties of HashSet

### ✔ 1. Uniqueness

* Duplicate elements are **not allowed**
* If you try to add the same element again, it is **ignored**

### ✔ 2. Backed by HashMap

* Internally, `HashSet` uses a **HashMap**
* Every element of the set is stored as a **key** in the map

### ✔ 3. No Insertion Order

* Elements are stored based on **hashing**
* Order is **not predictable**

### ✔ 4. Not Thread-Safe

* If multiple threads modify the same `HashSet`, it may cause:

  * Race conditions
  * Inconsistent results

---

## 4️⃣ Example: Adding Employees to HashSet

```java
Set<Employee> employees = new HashSet<>();

employees.add(new Employee("Varsha"));
employees.add(new Employee("Harsha"));
employees.add(new Employee("Ramesh"));
employees.add(new Employee("Varsha")); // duplicate

System.out.println(employees);
```

### Output:

```
[Varsha, Harsha, Ramesh]
```

➡ Even though `Varsha` was added twice, it appears **only once**.

---

## 5️⃣ How HashSet is Created Internally

```java
public HashSet() {
    map = new HashMap<>();
}
```

🔹 When you write:

```java
new HashSet<>();
```

➡ Internally, Java creates a **new HashMap**

---

## 6️⃣ Internal Working of add() Method

### HashSet add() Implementation (Simplified)

```java
public boolean add(E e) {
    return map.put(e, PRESENT) == null;
}
```

### Important Constant:

```java
private static final Object PRESENT = new Object();
```

* `PRESENT` is a **dummy constant value**
* Every element is stored as:

  ```
  key   = element
  value = PRESENT
  ```

---

## 7️⃣ How HashSet Guarantees Uniqueness

### Case 1: Adding a New Element

```java
employees.add("Varsha");
```

Internally:

```java
map.put("Varsha", PRESENT); // returns null
```

* No existing key → returns `null`
* Condition `== null` → `true`
* ✔ Element added successfully

---

### Case 2: Adding a Duplicate Element

```java
employees.add("Varsha");
```

Internally:

```java
map.put("Varsha", PRESENT); // returns old value (PRESENT)
```

* Key already exists
* `map.put()` returns **previous value**
* Condition `== null` → `false`
* ❌ Element NOT added

➡ **No change to HashMap → No change to HashSet**

---

## 8️⃣ remove() Method – Internal Working

### HashSet remove() Implementation (Simplified)

```java
public boolean remove(Object o) {
    return map.remove(o) == PRESENT;
}
```

---

### Case 1: Removing an Existing Element

```java
employees.remove("Varsha");
```

* Key exists in map
* `map.remove()` returns `PRESENT`
* ✔ Returns `true`
* Element removed

---

### Case 2: Removing a Non-Existing Element

```java
employees.remove("Sheetal");
```

* Key does NOT exist
* `map.remove()` returns `null`
* ❌ Returns `false`
* Nothing removed

---

## 9️⃣ Example: Checking remove() Return Value

```java
System.out.println(employees.remove("Sheetal")); // false
System.out.println(employees.remove("Varsha"));  // true
```

---

## 🔁 Other HashSet Methods (Mapped to HashMap)

| HashSet Method | Internally Uses         |
| -------------- | ----------------------- |
| `add()`        | `HashMap.put()`         |
| `remove()`     | `HashMap.remove()`      |
| `contains()`   | `HashMap.containsKey()` |
| `clear()`      | `HashMap.clear()`       |
| `size()`       | `HashMap.size()`        |
| `isEmpty()`    | `HashMap.isEmpty()`     |

---

## 10️⃣ Iterator Behavior

* HashSet iterator is **fail-fast**
* Modifying the set while iterating causes:

  ```
  ConcurrentModificationException
  ```

### Example:

```java
for (Employee e : employees) {
    employees.remove(e); // ❌ throws exception
}
```

---

## 11️⃣ Interview One-Line Summary

> **HashSet maintains uniqueness because it internally uses a HashMap where elements are stored as keys, and HashMap does not allow duplicate keys.**

---

## 12️⃣ Key Takeaways for Interviews

✅ HashSet is backed by HashMap
✅ Elements are stored as keys
✅ Value is a dummy constant `PRESENT`
✅ `add()` depends on `map.put()` return value
✅ Duplicate → old value returned → not added
✅ Iterator is fail-fast
✅ Not thread-safe

---

