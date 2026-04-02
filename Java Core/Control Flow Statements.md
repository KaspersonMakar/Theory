# **Control Flow in Java**
#### [Back to repository](https://github.com/KaspersonMakar/Theory)

## **Base**

<details>
<summary><b>What are control flow statements in Java?</b></summary>
<h1></h1>
Control flow statements are instructions that break the linear ("top-down") order of code execution, allowing the program to branch, repeat actions, or jump over blocks. In Java, they are divided into three main categories:
<ul>
  <li><b>Selection</b>: <code>if-else</code>, <code>switch</code>. These allow you to choose one of several execution paths.</li>
  <li><b>Iteration</b>: <code>for</code>, <code>while</code>, <code>do-while</code>. Used to repeat a section of code multiple times.</li>
  <li><b>Jumps</b>: <code>break</code>, <code>continue</code>, <code>return</code>, <code>yield</code>. These transfer control to another part of the program.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What's the difference between if and switch?</b></summary>
<h1></h1>
While both operators are used to select a path, their mechanisms differ significantly:
<br><br>

| Characteristic | If-else | switch |
|:---|:---|:---|
| **Condition type** | Any logical expression (<code>boolean</code>). | Specific values (integers, strings, enums). |
| **Ranges** | Ideal for range testing (<code>x &gt; 10 && x &lt; 20</code>). | Exact matches only (<code>x == 10</code>). |
| **Complexity** | Multiple conditions can be combined. | Limited to testing a single variable. |
| **Performance** | Linear (<code>O(n)</code>). | Potentially constant (<code>O(1)</code>) via transition tables. |
<h1></h1>
</details>

<details>
<summary><b>What loops exist in Java?</b></summary>
<h1></h1>
There are four main types of loops in Java: <code>for</code>, <code>while</code>, <code>do-while</code>, and <code>enhanced for-loop</code>.
<br><br>
<ul>
  <li><b>while</b>: Used when the number of iterations is unknown. Checks the condition before each step.</li>
  <li><b>for</b>: Used when the number of iterations is known or there is a clear counter.</li>
  <li><b>do-while</b>: The loop body is executed at least once, as the condition is checked at the end.</li>
  <li><b>enhanced for-loop</b>: Optimized for iterating over arrays and collections.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What is the difference between break and continue?</b></summary>
<h1></h1>
<ul>
  <li><b>break</b>: Immediately terminates the current loop or <code>switch</code> block. Commonly used to exit a loop when a goal is achieved.</li>
  <li><b>continue</b>: Skips the rest of the current iteration and proceeds to the next one. Ideal for filtering data within a loop.</li>
</ul>

<b>Example:</b>
```java
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) continue; // Skip even numbers
    if (i > 7) break;        // Stop loop if i > 7
    System.out.println(i);
}
```
<h1></h1>
</details>
<details>
<summary><b>What is "fall-through" in a switch statement?</b></summary>
<h1></h1>Fall-through occurs when execution continues into subsequent <code>case</code> blocks after a match is found, until a <code>break</code> or the end of the <code>switch</code> is reached.
<br>How it works:</b> Once Java finds a match, it "enters" and executes all following code in order.
<br>Usage:</b> Useful for grouping multiple values that share the same result.
<br>Danger:</b> Forgetting a <code>break</code> can lead to unintended actions, which is a classic logic bug.
<h1></h1
</details>
