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
  <li>Parant's constructor call <code>(super())</code>.</li>
  <li>Field initializers.</li>
  <li>Initialization blocks.</li>
  <li>Execution of the constructor body.</li>
</ul>
</details>
<h1></h1>
</details>

<details>
<summary><b>What are instance initializer blocks?</b></summary>
<h1></h1>
An instance initializer block is simply a set of braces <code>{ }</code> inside a class containing executable code. It cannot be used inside methods or other initialization blocks.
<br><br>
<b>Code example:</b>
  
```java
public class ChessPiece {
    String type;

    // This is an INSTANCE INITIALIZER BLOCK
    {
        System.out.println("Block executed");
        type = "Pawn"; 
    }

    public ChessPiece() {
        System.out.println("Constructor executed");
    }
}
```
<br>
<b>How it works "under the hood":</b>
During compilation, <code>javac</code> scans the source code. It takes all anonymous blocks (not marked as <code>static</code>) and places them into the internal <code>&lt;init&gt;</code> method in the following order:
<ol>
  <li>Call to <code>super()</code>.</li>
  <li>Field initializers AND Initialization blocks (in the order they appear in the code from top to bottom).</li>
  <li>The body of the constructor.</li>
</ol>
<h1></h1>
</details>

<details>
<summary><b>What is the difference between constructor and initializer block?</b></summary>
<h1></h1>

| Characteristic | Initializer Block | Constructor |
|:---|:---|:---|
| **Parameters** | Cannot take arguments. | Can take arguments to configure the object. |
| **Execution** | Always executed for every object created. | Only the specific called constructor is executed. |
| **Name** | None. | Must match the class name. |
| **Logic** | Usually for common setup or anonymous classes. | For specific configuration of a particular instance. |
<h1></h1>
</details>

<details>
<summary><b>What is a static initialization block?</b></summary>
<h1></h1>
A <code>static { ... }</code> block is used to initialize static fields or perform actions when the <b>class</b> is first loaded into memory.
<br><br>
<b>Code example:</b>
  
```java
public class Board {
    static String[][] board;
    static {
        int size = 8;
        board = new String[size][size];
        System.out.println("Static block: Field created");
    }
}
```
<br>
<b>Key rules:</b>
<ul>
  <li><b>Execution</b>: Runs exactly once when the class is loaded by the JVM.</li>
  <li><b>Triggers</b>: Class loading is triggered by creating the first instance, accessing a static field/method, or using <code>Class.forName()</code>.</li>
  <li><b>Limitations</b>: You cannot use <code>this</code> or <code>super</code>, or access non-static instance fields/methods because the object doesn't exist yet.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What happens if initialization fails?</b></summary>
<h1></h1>

<details>
<summary><b>Scenario A: Error in a static block (Class failure)</b></summary>
If an exception is thrown inside a <code>static { ... }</code> block:
<ul>
  <li>The JVM throws an <code>ExceptionInInitializerError</code>.</li>
  <li>This is an <b>Error</b>, not a regular Exception. The class is marked as "unusable".</li>
  <li>Any subsequent attempt to access this class will result in a <code>NoClassDefFoundError</code>.</li>
</ul>
</details>

<details>
<summary><b>Scenario B: Error in a constructor (Object failure)</b></summary>
If an exception is thrown in a regular block <code>{ ... }</code> or a constructor:
<ul>
  <li>A regular Exception is thrown.</li>
  <li>The object is not created, and no reference is returned from the <code>new</code> keyword.</li>
  <li><b>Note:</b> If the object already partially occupied memory, it will eventually be cleaned up by the Garbage Collector.</li>
</ul>
</details>
<h1></h1>
</details>
