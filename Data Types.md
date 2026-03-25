# **Data Types in Java**
#### [Back to repository](https://github.com/KaspersonMakar/Theory)
## **Base**
<details>
  <summary><b>What are primitive data types in Java?</b></summary>
&ensp;Java has exactly eight primitive data types, which are the basic building blocks for data manipulation and directly store values in memory. They are categorized into four groups: <strong>integers</strong>, <strong>floating-point numbers</strong>, <strong>characters</strong>, and a <strong>boolean type</strong>.

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

</details>

<details>
<summary><b>Difference between Primitive and Reference Data Types</b></summary>
&ensp;In Java, data types are categorized into two fundamental groups: Primitive and Reference types. The primary distinction lies in how they are stored in memory and how the Java Virtual Machine (JVM) handles them during execution.
<br><b>Primitive Types</b>: Store the actual value directly in <b>Stack</b> memory.
<br><b>Reference Types</b>: Store only the <b>memory address (reference)</b> in the Stack, while the actual object resides in the <b>Heap</b>.
</details>

<details>
<summary><b>What is type casting? Difference between implicit and explicit casting?</b></summary>
&ensp;<strong>Type casting</strong> is the process of converting a value from one data type (e.g., integer) to another (e.g., float). The Java compiler handles this in two ways depending on the size and precision of the types involved.
  
<li><b>Implicit casting</b>: Performed automatically by the compiler to prevent data loss when converting smaller types to larger ones (e.g., <code>int</code> to <code>double</code>).</li>
<li><b>Explicit casting</b>: Manually requested by the programmer using parentheses, often used when data loss (like truncating decimals) is acceptable or when converting larger types to smaller ones (e.g., <code>long</code> to <code>short</code>).</li>
</details>

<details>
<summary><b>What is autoboxing and unboxing?</b></summary>
&ensp;<strong>Autoboxing</strong> is the automatic conversion of primitive types to their corresponding wrapper classes by the Java compiler, while <strong>unboxing</strong> is the reverse process.
<li><b>Autoboxing example</b>: Assigning an <code>int</code> to an <code>Integer</code> variable.</li>
<li><b>Unboxing example</b>: Assigning an <code>Integer</code> object to an <code>int</code> variable.</li>
</details>

<details>
<summary><b>What are Wrapper Classes and why are they needed?</b></summary>
&ensp;<strong>Wrapper classes</strong> are object-oriented representations of primitive data types. They "wrap" the primitive value inside an object, allowing primitives to be treated as objects.

<b>Usage:</b>
<ul>
<li><b>Collections Framework:</b> Java data structures like <code>ArrayList</code>, <code>HashMap</code>, or <code>HashSet</code> can only store objects, not primitive types.</li>
<li><b>Nullability:</b> Primitive types cannot be <code>null</code>. Wrapper classes are objects, so they can hold a <code>null</code> value, which is useful in database operations and APIs.</li>
<li><b>Utility Methods:</b> They provide helpful methods for conversion (like <code>Integer.parseInt()</code>).</li>
</ul>
</details>
