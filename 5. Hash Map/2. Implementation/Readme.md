

---

# 🔑 How HashMap Works Internally in Java

HashMap is one of the **most frequently asked Java interview topics** because its internal working is **not straightforward**.
HashMap stores data in **key–value pairs** and internally uses the concept of **Hashing**.

---

## 1️⃣ What is Hashing?

**Hashing** is a technique to generate a **unique integer value (hashcode)** for an object using its properties.

### Properties of HashCode

* ✅ If two objects are **equal**, they **must have the same hashcode**
* ❌ If two objects have the **same hashcode**, they **may not be equal**
* Hashing improves **search, insert, and delete performance**

---

## 2️⃣ Internal Structure of HashMap

### Node Class (Internal Data Structure)

HashMap internally uses a **nested static class `Node`** to store entries.

```java
static class Node<K,V> implements Map.Entry<K,V> 
{
    final int hash;
    final K key;
    V value;
    Node<K,V> next;

    Node(int hash, K key, V value, Node<K,V> next) 
    {
        this.hash = hash;
        this.key = key;
        this.value = value;
        this.next = next;
    }

    public final K getKey()        { return key; }
    public final V getValue()      { return value; }
    public final String toString() { return key + "=" + value; }

    public final int hashCode() 
    {
        return Objects.hashCode(key) ^ Objects.hashCode(value);
    }
}
```

### Explanation

* `hash` → hashcode of key
* `key` → key object
* `value` → value object
* `next` → reference to next node (used in collisions → LinkedList)

---

## 3️⃣ HashMap Table Structure

HashMap internally maintains an **array of Node objects** called `table`.

```java
transient Node<K,V>[] table;
```

* This array is **not initialized immediately**
* Each index of the array is called a **bucket**

---

## 4️⃣ HashMap Creation (No-Arg Constructor)

When we create a HashMap like this:

```java
HashMap<K,V> map = new HashMap<>();
```

Only the **load factor** is set.

```java
public HashMap() {
    this.loadFactor = DEFAULT_LOAD_FACTOR; // all other fields defaulted
}
```

### Default Values

* **Initial capacity** → *Not initialized yet*
* **Load factor** → `0.75`

👉 The `table` array is initialized **only when the first element is inserted**.

---

## 5️⃣ Inserting Elements into HashMap (`put()`)

### Step-by-Step Insertion Process

#### 🔹 Step 1: Table Initialization

* On **first insertion**, the table is initialized with **size = 16**
* Buckets → index `0` to `15`

#### 🔹 Step 2: Handling `null` Key

* Hashcode of `null` is `0`
* `null` key is always stored at **index 0**

#### 🔹 Step 3: Non-Null Key

* Hashcode of key is calculated
* Index is calculated using hash
* Element goes to corresponding bucket

#### 🔹 Step 4: No Collision

* If bucket is empty → new `Node` is created and inserted

---

## 6️⃣ Collision Handling in HashMap

**Collision** occurs when:

* Two different keys have the **same bucket index**

### How HashMap Handles Collision

1. Check if the **existing key equals the new key**

   * If `equals()` returns `true` → value is **updated**
2. If keys are different:

   * New Node is added at the **end of the LinkedList**

```
Bucket → Node → Node → Node
```

---

## 7️⃣ Java 8 Improvement – Treeification 🌳

In Java 8, HashMap improved collision handling.

### TREEIFY_THRESHOLD

* Constant value = **8**
* Declared as `final`
* Cannot be changed

### Behavior

* If **LinkedList size > 8** in a bucket
* LinkedList is converted into a **Red-Black Tree**
* Improves performance from **O(n) → O(log n)**

---

## 8️⃣ Fetching a Value from HashMap (`get()`)

### Steps to Fetch a Value

1. Calculate **hashcode of the key**
2. Calculate bucket index
3. Go to that bucket
4. Compare keys using `equals()`
5. If key is found → return value
6. If key not found → return `null`

---

## 9️⃣ Resizing a HashMap

### When Does Resizing Happen?

Resizing depends on:

```
threshold = capacity × loadFactor
```

Example:

* Capacity = 16
* Load factor = 0.75
* Threshold = `16 × 0.75 = 12`

👉 When elements exceed **12**, resizing happens.

---

### How Resizing Works

* Capacity is **always doubled**
* 16 → 32 → 64 → 128 …
* All existing elements are **rehashed and redistributed**
* This is a **costly operation**

---

## 🔟 Time Complexity Summary

| Operation | Average | Worst Case      |
| --------- | ------- | --------------- |
| put()     | O(1)    | O(n) / O(log n) |
| get()     | O(1)    | O(n) / O(log n) |
| remove()  | O(1)    | O(n) / O(log n) |

---

## 🧠 Interview Tip (Very Important)

👉 **HashMap performance depends heavily on:**

* Good `hashCode()` implementation
* Proper `equals()` method
* Avoiding too many collisions

---

