# **Data Types in Java**
#### [Back to repository](https://github.com/KaspersonMakar/Theory)
## **Base**
<details>
  <summary><b>What are primitive data types in Java?</b></summary>
  <p style='text-indent:0.25cm'>
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

</details>

<details>
<summary><b>Difference between Primitive and Reference Data Types</b></summary>
<p style='text-indent:0.25cm'>
In Java, data types are categorized into two fundamental groups: Primitive and Reference types. The primary distinction lies in how they are stored in memory and how the Java Virtual Machine (JVM) handles them during execution.
<br><b>Primitive Types</b>: Store the actual value directly in <b>Stack</b> memory.
<br><b>Reference Types</b>: Store only the <b>memory address (reference)</b> in the Stack, while the actual object resides in the <b>Heap</b>.
</details>
