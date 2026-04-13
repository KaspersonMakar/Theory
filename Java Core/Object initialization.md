# **Object Initialization Theory**
#### [Back to repository](https://github.com/KaspersonMakar/Theory)

## **Base**

<details>
<summary><b>What is object initialization in Java?</b></summary>
<h1></h1>
Object initialization is the process of creating an instance of a class in memory (Heap) and bringing it into a working state. It is not just a constructor call, but a whole chain of events triggered by the <code>new</code> keyword.

When you write <code>Integer a = new Integer();</code>, the JVM performs the following steps:
<br><b>Class Loading -> Static Initialization -> Memory Allocation & Zeroing -> Instance Initialization </b>

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
<summary><b>What constructors exist in Java?</b></summary>
<h1></h1>
From a language perspective, they are divided into three main types:
<ul>
  <li><b>Default Constructor</b>: If you do not write any constructor in your class, the compiler automatically adds an empty constructor with no arguments. As soon as you add any constructor of your own, the default one disappears.</li>
  <li><b>No-arg Constructor</b>: A constructor you write manually that takes no parameters (e.g., <code>public Board() { ... }</code>). It is used when an object has a sensible "default" state.</li>
  <li><b>Parameterized Constructor</b>: Takes data to configure the object (e.g., <code>public Piece(Color color, ...)</code>). This represents an "obligation"—the object cannot be created without these specific parameters.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What is a copy constructor?</b></summary>
<h1></h1>
Java does not have a built-in copy constructor (like C++), but it is a standard pattern. This is a constructor that takes an <b>object of the same class</b> as a parameter and creates an exact copy of it.
<br><br>
<b>Example:</b>
  
```java
public ChessPiece(ChessPiece other) {
    this.color = other.color;
    this.pieceType = other.pieceType;
    // Note: creating a new object for the position to ensure independence
    this.position = new Position(other.position.getRow(), other.position.getCol()); 
}
  
```
<h1></h1>
</details>

<details>
<summary><b>What does an object consist of?</b></summary>
<h1></h1>
Every object in Java is defined by three key characteristics:
<ul>
  <li><b>State</b>: Refers to the data variables (fields) that describe the object's current condition. For a "Car", this would be color, speed, and fuel level.</li>
  <li><b>Behavior</b>: Represented by methods. It defines the functional actions an object can perform, such as "accelerate" or "brake".</li>
  <li><b>Identity</b>: What makes an object unique and independent. In Java, this is typically associated with its memory address, allowing the JVM to distinguish between two objects even if their states are identical.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What is deep copying?</b></summary>
<h1></h1>
<b>Deep copying</b> is the process of creating a complete, independent copy of an object, where all nested objects and structures are also copied recursively.
<br><br>
Unlike shallow copying, a deep copy does not share references to internal data with the original. This makes any changes to the copy absolutely safe for the source object, as they do not affect each other.
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

## **Advanced**

<details>
<summary><b>How are final fields initialized?</b></summary>
<h1></h1>
Fields with the <code>final</code> modifier are not just constants. It is a promise to the compiler and the JVM that the value will be set <b>exactly once</b> and will never change. To keep this promise, Java imposes strict rules on their initialization.

<br><b>Three legitimate places for initialization:</b>
<ul>
  <li><b>At declaration</b>: <code>final int x = 10;</code>.</li>
  <li><b>In an instance initializer block</b>: <code>{ x = 10; }</code>.</li>
  <li><b>In every constructor</b>: If you haven't initialized the field by the first two methods, you are required to do so in every constructor of the class.</li>
</ul>

A field not initialized at declaration is called a <b>blank final</b>. This is a powerful tool: it allows a field to be immutable while still depending on input data.

<br><b>The "Definite Assignment" Rule</b>
<br>Unlike regular fields, which default to <code>0</code> or <code>null</code> if forgotten, <code>final</code> fields must be explicitly assigned. The Java compiler uses a <b>Definite Assignment</b> algorithm to prove that the variable will receive a value in every possible execution path.

<b>Example:</b>

```java
final int x;
if (condition) {
    x = 10;
} 
// ERROR: The compiler will say x might remain uninitialized if condition is false. 
// You must add an 'else { x = 20; }'.
```

<br><b>static final</b>
<br>For static final fields, the rules are even stricter. Since they have no constructors, there are only two places:
<ol>
  <li>At declaration.</li>
  <li>In a static initialization block: <code>static { ... }</code>.</li>
</ol>
If it is a primitive or a string known at compile time, it becomes a <b>compile-time constant</b>. The JVM won't even access the class for this value—it "embeds" the value directly into the call sites in other classes.
<h1></h1>
</details>

<details>
<summary><b>What is lazy initialization?</b></summary>
<h1></h1>
<b>Lazy Initialization</b> is a strategy where the creation of a "heavy" object or the calculation of a complex value is deferred until the moment it is actually needed in the code.
<br><br>
<b>Benefits:</b>
<ul>
  <li>Speeds up application startup (e.g., loading only 50 services initially instead of 100).</li>
  <li>Saves resources (e.g., if a service might not be used at all during execution).</li>
</ul>

<br><b>Multithreaded implementation (Double-Checked Locking):</b>

```java
public class HeavyService {
    private volatile HeavyObject instance; // The key is 'volatile'

    public HeavyObject getInstance() {
        if (instance == null) { // First check (no locking)
            synchronized (this) {
                if (instance == null) { // Second check (under lock)
                    instance = new HeavyObject();
                }
            }
        }
        return instance;
    }
}
```

<b>The "volatile" nuance:</b> Without <code>volatile</code>, a thread might see a reference to the object before the constructor has finished its work. <code>volatile</code> guarantees that the write to <code>instance</code> happens strictly after the constructor completes.
<h1></h1>
</details>

<details>
<summary><b>What are circular dependencies during initialization?</b></summary>
<h1></h1>
A <b>circular dependency</b> during initialization occurs when Class A requires Class B for its setup, while Class B, at that same moment, requires Class A.
<br><br>
In Java, this doesn't lead to an immediate crash (like <code>StackOverflowError</code>), but it creates some of the most elusive bugs where <code>null</code> or <code>0</code> appears where they shouldn't be, because one of the classes is accessed before it is fully initialized.
<h1></h1>
</details>

<details>
<summary><b>How does JVM guarantee initialization safety?</b></summary>
<h1></h1>
At the core is the <b>Initialization Lock (LC)</b>—a special lock assigned to every class. The JVM uses a complex 12-step algorithm, but simplified, it works as a <b>state machine</b>.

<br><b>Four states of a class:</b>
<ul>
  <li><b>Not initialized</b>: Class is loaded, but statics haven't run.</li>
  <li><b>Being initialized</b>: Thread T is currently executing <code>&lt;clinit&gt;</code>.</li>
  <li><b>Fully initialized</b>: Everything is ready for use.</li>
  <li><b>Error state</b>: Initialization failed (throws <code>ExceptionInInitializerError</code>).</li>
</ul>

<b>Protection mechanism:</b>
<ul>
  <li>When a thread requests a class, it must acquire the <b>LC-lock</b>.</li>
  <li>If the state is <b>"Being initialized"</b> by another thread, the current thread goes to sleep and waits.</li>
  <li>If the state is <b>"Fully initialized"</b>, the thread proceeds immediately.</li>
  <li><b>Happens-Before</b>: All memory changes made in a static block are guaranteed to be visible to all other threads once initialization is complete.</li>
</ul>
<h1></h1>
</details>
