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
</details>

## **Advanced**

<details>
<summary><b>What are labeled break and continue?</b></summary>
<h1></h1>
In Java, standard <code>break</code> and <code>continue</code> only work on the innermost loop. Labels allow you to control outer loops in complex nested constructs.
<br><br>
<li><b>Label</b>: An identifier followed by a colon (e.g., <code>outer:</code>) placed immediately before a loop.</li>
<li><b>Labeled break</b>: Immediately terminates the execution of the labeled loop and all nested constructs. This is a clean way to exit deep nesting without extra flags.</li>
<li><b>Labeled continue</b>: Skips the remainder of the inner loop iteration and continues with the next iteration of the labeled outer loop.</li>

<br><b>Code example:</b>
```java
outer: // Label for the outer loop
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        if (matrix[i][j] == target) {
            System.out.println("Found!");
            break outer; // Exit both loops at once
        }
    }
}
```
<h1></h1>
</details>

<details>
<summary><b>How do you iterate safely over collections?</b></summary>
<h1></h1>
Safe iteration means traversing a collection without throwing a <code>ConcurrentModificationException</code> (CME) when attempting to modify its contents.
<br><br>
<b>Basic safe iteration techniques:</b>
<ul>
  <li><b>Explicit Iterator</b>: The most reliable method. Only <code>iterator.remove()</code> safely removes elements during iteration by synchronizing the state of the iterator and the collection.</li>
  <li><b>removeIf() (Java 8+)</b>: The most concise modern approach. It encapsulates iterator logic internally and is optimized for different collection types.</li>
  <li><b>Iterating over a copy</b>: Creating a copy (e.g., <code>new ArrayList&lt;&gt;(list)</code>) to iterate while modifying the original. This is safe but memory-intensive.</li>
</ul>
<h1></h1>
</details>
