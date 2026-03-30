Markdown

# **Operators in Java**
#### [Back to repository](https://github.com/KaspersonMakar/Theory)

## **Base**

<details>
<summary><b>What types of operators exist in Java?</b></summary>
<h1></h1>
In Java, operators are classified according to their functional purpose:
<ul>
  <li><b>Arithmetic operators</b>: Used for basic mathematical calculations like addition (<code>+</code>), subtraction (<code>-</code>), multiplication (<code>*</code>), division (<code>/</code>), and modulo (<code>%</code>).</li>
  <li><b>Comparison operators (relational)</b>: Allow you to compare two values, including <code>==</code>, <code>!=</code>, <code>&gt;</code>, <code>&lt;</code>, <code>&gt;=</code>, and <code>&lt;=</code>.</li>
  <li><b>Logical operators</b>: Work with Boolean values (<code>&&</code>, <code>||</code>, <code>!</code>) and support short-circuit evaluation.</li>
  <li><b>Bitwise operators</b>: Manipulate data at the level of individual bits (<code>&</code>, <code>|</code>, <code>^</code>, <code>~</code>, <code>&lt;&lt;</code>, <code>&gt;&gt;</code>, <code>&gt;&gt;&gt;</code>).</li>
  <li><b>Assignment operators</b>: Used to write values to variables, including compound forms (<code>=</code>, <code>+=</code>, <code>-=</code>, <code>*=</code>, <code>/=</code>, <code>%=</code>).</li>
  <li><b>Unary operators</b>: Require only one operand, such as increment (<code>++i</code>, <code>i++</code>) and decrement (<code>--i</code>, <code>i--</code>).</li>
  <li><b>Ternary operator</b>: A compact form of if-else: <code>condition ? value1 : value2</code>.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What is short-circuit evaluation?</b></summary>
<h1></h1>
This is an optimization mechanism where the JVM stops calculating a Boolean expression as soon as the result becomes obvious. This property is inherent in <code>&&</code> (logical AND) and <code>||</code> (logical OR).
<br><br>
<li><strong>Boolean AND (&&)</strong>: If the left side is <code>false</code>, the entire expression is <code>false</code>, and the right side is ignored.</li>
<li><strong>Boolean OR (||)</strong>: If the left side is <code>true</code>, the entire expression is <code>true</code>, and the right side is skipped.</li>
<h1></h1>
</details>

<details>
<summary><b>What does ++i vs i++ mean?</b></summary>
<h1></h1>
Both increment the variable by 1, but they differ in when the new value becomes available.
<br><br>
<li><b>++i (Prefix)</b>: The variable is incremented first, then the new value is used in the expression.</li>

```java
int a = 5;
int b = ++a; // a=6, b=6

````

<li><b>i++ (Postfix)</b>: The old value is used first, and only after that the variable is incremented.</li>

```Java

int x = 5;
int y = x++; // y=5, x=6

````

<h1></h1>
</details>

<details>
<summary><b>What are bitwise operators?</b></summary>
<h1></h1>
Bit operations are data manipulations at the level of bits (0 and 1). In Java, they are executed directly by the processor, making them extremely fast.


<li><code>&</code> (Bitwise AND): Result is 1 only if both bits are 1.</li>
<li><code>|</code> (Bitwise OR): Result is 1 if at least one bit is 1.</li>
<li><code>^</code> (XOR): Result is 1 if bits are different.</li>
<li><code>~</code> (NOT): Inverts all bits.</li>
<li><code>&lt;&lt;, &gt;&gt;, &gt;&gt;&gt;</code> (Shifts): Move bits left or right, effectively performing fast multiplication or division by powers of two.</li>
<h1></h1>
</details>

<details>
<summary><b>Why use bit operations instead of alternatives?</b></summary>
<h1></h1>
The choice of bit operations is justified in three cases:
<ul>
<li><b>Extreme performance</b>: If the operation is performed millions of times per second (e.g., graphics rendering).</li>
<li><b>Resource limitation</b>: In microcontrollers or network data where every byte counts.</li>
<li><b>Subject area specifics</b>: Working with file formats, network packages, or hardware directly.</li>
</ul>
Compared to alternatives like <code>EnumSet</code> or <code>Boolean</code>, bit operations offer minimum memory usage and maximum speed, though readability is lower.
<h1></h1>
</details>

<details>
<summary><b>Can operators be overloaded in Java?</b></summary>
<h1></h1>
Unlike languages like C++ or Python, Java <strong>does not</strong> allow you to change the behavior of standard symbols (such as <code>+</code> or <code>*</code>) for your own classes.
<h1></h1>
</details>
