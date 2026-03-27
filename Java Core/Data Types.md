# **Data Types in Java**
#### [Back to repository](https://github.com/KaspersonMakar/Theory)
## **Base**
<details>
  <summary><b>What are primitive data types in Java?</b></summary>
  <h1></h1>
Java has exactly eight primitive data types, which are the basic building blocks for data manipulation and directly store values in memory. They are categorized into four groups: <strong>integers</strong>, <strong>floating-point numbers</strong>, <strong>characters</strong>, and a <strong>boolean type</strong>.

| Data Type | Category | Size (bits) | Description | Wrapper Class |
|-----------|----------|-------------|-------------|---------------|
| byte | Integer | 8 | Stores whole numbers from -128 to 127. | Byte |
| short | Integer | 16 | Stores whole numbers from -32,768 to 32,767. | Short |
| int | Integer | 32 | The most common integer type, with a large range. | Integer |
| long | Integer | 64 | Used for very large whole numbers; requires 'L' suffix. | Long |
| float | Floating-point | 32 | Stores fractional numbers with single precision (approx. 7 decimal places); requires 'f' suffix. | Float |
| double | Floating-point | 64 | Stores fractional numbers with double precision (approx. 15 decimal places); this is the default for decimals. | Double |
| char | Character | 16 | Stores a single Unicode character (e.g., 'A', '$', etc.) in single quotes. | Character |
| boolean | Logical | Varies | Stores only true or false values. | Boolean |
<h1></h1>
</details>

<details>
<summary><b>Difference between Primitive and Reference Data Types</b></summary>
<h1></h1>
 In Java, data types are categorized into two fundamental groups: Primitive and Reference types. The primary distinction lies in how they are stored in memory and how the Java Virtual Machine (JVM) handles them during execution.
<br><b>Primitive Types</b>: Store the actual value directly in <b>Stack</b> memory.
<br><b>Reference Types</b>: Store only the <b>memory address (reference)</b> in the Stack, while the actual object resides in the <b>Heap</b>.
<h1></h1>
</details>

<details>
<summary><b>What is type casting? Difference between implicit and explicit casting?</b></summary>
<h1></h1>
<strong>Type casting</strong> is the process of converting a value from one data type (e.g., integer) to another (e.g., float). The Java compiler handles this in two ways depending on the size and precision of the types involved.
  
<li><b>Implicit casting</b>: Performed automatically by the compiler to prevent data loss when converting smaller types to larger ones (e.g., <code>int</code> to <code>double</code>).</li>
<li><b>Explicit casting</b>: Manually requested by the programmer using parentheses, often used when data loss (like truncating decimals) is acceptable or when converting larger types to smaller ones (e.g., <code>long</code> to <code>short</code>).</li>
<h1></h1>
</details>

<details>
<summary><b>What is autoboxing and unboxing?</b></summary>
<h1></h1>
<strong>Autoboxing</strong> is the automatic conversion of primitive types to their corresponding wrapper classes by the Java compiler, while <strong>unboxing</strong> is the reverse process.
<li><b>Autoboxing example</b>: Assigning an <code>int</code> to an <code>Integer</code> variable.</li>
<li><b>Unboxing example</b>: Assigning an <code>Integer</code> object to an <code>int</code> variable.</li>
<h1></h1>
</details>

<details>
<summary><b>What are Wrapper Classes and why are they needed?</b></summary>
<h1></h1>
<strong>Wrapper classes</strong> are object-oriented representations of primitive data types. They "wrap" the primitive value inside an object, allowing primitives to be treated as objects.

<b>Usage:</b>
<ul>
<li><b>Collections Framework:</b> Java data structures like <code>ArrayList</code>, <code>HashMap</code>, or <code>HashSet</code> can only store objects, not primitive types.</li>
<li><b>Nullability:</b> Primitive types cannot be <code>null</code>. Wrapper classes are objects, so they can hold a <code>null</code> value, which is useful in database operations and APIs.</li>
<li><b>Utility Methods:</b> They provide helpful methods for conversion (like <code>Integer.parseInt()</code>).</li>
</ul>
<h1></h1>
</details>

## **Advanced**
<details>
<summary><b>What is Integer caching?</b></summary>
<h1></h1>
There is a private static <code>IntegerCache</code> class inside the <code>Integer</code> class, which is initialized the first time it is accessed. By default, it stores objects for all numbers in the range from <strong>-128 to 127</strong>, which corresponds to the range of the <code>byte</code> type.
  
```java
Integer a1 = 100;
Integer b1 = 100;
System.out.println(a1 == b1); // true
  
Integer a2 = 1000;
Integer b2 = 1000;
System.out.println(a2 == b2); // false
```
The <code>==</code> operator compares addresses in memory (references) in the <strong>Stack</strong>. In the first case, references point to the same object in <code>IntegerCache</code>. In the second case, two new objects are created in the <strong>Heap</strong>.
<h1></h1>
</details>

<details>
<summary><b>What is the behavior of == vs .equals() for wrapper types?</b></summary>
<h1></h1>
In the context of <strong>wrapper classes</strong>, the <code>==</code> operator compares references to objects in memory, and <code>.equals()</code> compares their actual values.
  
```java
Integer a2 = 1000;
Integer b2 = 1000;
System.out.println(a2 == b2); // false
System.out.println(a2.equals(b2)); // true
```
Since <code>==</code> compares addresses, it may return <code>true</code> for cached values (up to 127) but <code>false</code> for others. Therefore, <code>.equals()</code> is the reliable way to compare the values of wrapper objects.
<h1></h1>
</details>
