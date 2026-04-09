# **Object Initialization Theory**
#### [Back to repository](https://github.com/KaspersonMakar/Theory)

## **Base**

<details>
<summary><b>What is object initialization in Java?</b></summary>
<h1></h1>
Object initialization is the process of creating an instance of a class in memory (Heap) and bringing it into a working state. It is not just a constructor call, but a whole chain of events triggered by the <code>new</code> keyword.

When you write <code>Integer a = new Integer();</code>, the JVM performs the following steps:
<br><b>Class Loading -> Memory Allocation -> Zeroing -> Initialization -> Constructor</b>

<br>
<details>
<summary><b>Step 1: Class Loading</b></summary>
Imagine you are building a house:
<ul>
  <li>The <b>.class file</b> is the blueprint.</li>
  <li><b>Metaspace</b> (JVM memory area) is the archive where blueprints are stored.</li>
  <li><b>Heap</b> is the construction site where the houses themselves stand.</li>
</ul>
The JVM cannot allocate memory for an object in the Heap until it knows its size. It reads the <code>.class</code> file to understand exactly how many bytes (e.g., 8 bytes for a <code>long</code> and 4 bytes for an <code>int</code>) need to be "cut out" in the Heap.
</details>

<details>
<summary><b>Step 2: Static Initialization (&lt;clinit&gt;)</b></summary>
Static fields belong to the <b>Class</b>, not the object. They are created in Metaspace (or a special area of the Heap in newer Java versions) only once. During this stage, the JVM executes the <code>&lt;clinit&gt;</code> (Class Initializer) method:
<ul>
  <li>Assigns values specified at declaration (e.g., <code>static int x = 10;</code>).</li>
  <li>Executes <code>static { ... }</code> blocks.</li>
</ul>
</details>

<details>
<summary><b>Step 3: Memory Allocation and "Zero State"</b></summary>
Once the blueprint is ready, memory is allocated in the Heap. Immediately after allocation, it is filled with zeros:
<ul>
  <li>All numeric fields become <code>0</code> or <code>0.0</code>.</li>
  <li><code>boolean</code> fields become <code>false</code>.</li>
  <li>All references (<code>Object</code>, <code>String</code>) become <code>null</code>.</li>
</ul>
This ensures that you never read "garbage" from memory left over from previous objects (as can happen in C++).
</details>

<details>
<summary><b>Step 4: Instance Initialization (&lt;init&gt;)</b></summary>
Now the process of turning a "zeroed blank" into a real object begins. This stage involves:
<ul>
  <li>Constructor call.</li>
  <li>Field initializers.</li>
  <li>Initialization blocks.</li>
  <li>Execution of the constructor body.</li>
</ul>
</details>
<h1></h1>
</details>
