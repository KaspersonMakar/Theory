# **Access Modifiers & Encapsulation**
#### [Back to repository](https://github.com/KaspersonMakar/Theory)

## **Base**

<details>
<summary><b>What are access modifiers in Java?</b></summary>
<h1></h1>
Access modifiers are keywords in Java that define the visibility and access level of classes, constructors, methods, and fields.

From a technical perspective, they instruct the compiler and JVM which code has the right to "see" and invoke a specific component. From a design perspective, they are the primary tool for <b>encapsulation</b>, allowing you to hide internal logic and expose only a safe interface.

In Java, there are 4 levels of access:
<ul>
  <li><b>private</b> (most restrictive).</li>
  <li><b>package-private</b> (default, if no modifier is specified).</li>
  <li><b>protected</b>.</li>
  <li><b>public</b> (most open).</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What is the difference between public, private, protected, and default?</b></summary>
<h1></h1>

| Modifier | Inside Class | Inside Package | In Subclasses | Everywhere |
|:---|:---:|:---:|:---:|:---:|
| **public** | Yes | Yes | Yes | Yes |
| **protected** | Yes | Yes | Yes | No |
| **default** (not specified) | Yes | Yes | No | No |
| **private** | Yes | No | No | No |

<h1></h1>
</details>

<details>
<summary><b>Can a class be private?</b></summary>
<h1></h1>
The answer depends on the type of class:
<ul>
  <li><b>Top-level class</b> (in a separate file): <b>No</b>. It can only be <code>public</code> or <code>package-private</code> (default). If an outer class were <code>private</code>, no one could see it or create an instance, making the class useless.</li>
  <li><b>Nested class</b> (Inner/Nested class): <b>Yes</b>. A nested class can be <code>private</code>. This is the highest degree of encapsulation; a private nested class is used only within its "parent".</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>Can constructors have access modifiers?</b></summary>
<h1></h1>
The modifier on a constructor determines who can write <code>new MyClass()</code>.
<ul>
  <li><b>public</b>: Anyone can create the object.</li>
  <li><b>protected</b>: Only "peers" in the same package or subclasses can create the object (often used in abstract classes).</li>
  <li><b>default</b>: Only classes within the same package (useful for internal library components).</li>
  <li><b>private</b>: No one outside can call <code>new</code>.</li>
</ul>

<b>Used for:</b>
<ul>
  <li><b>Singleton</b>: When we need only one instance for the entire program.</li>
  <li><b>Utility classes</b>: Classes like <code>Math</code>, which contain only static methods.</li>
  <li><b>Static Factory Methods</b>: When we want the user to call <code>MyClass.create()</code> instead of <code>new MyClass()</code>.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What is encapsulation?</b></summary>
<h1></h1>
Encapsulation (from the word "capsule") is the process of bundling data (state) and methods for working with that data (behavior) into a single logical unit (class), where access to the object's internal state is strictly restricted.

<b>Three pillars of "proper" encapsulation:</b>
<ol>
  <li><b>Data Hiding</b>: We make fields <code>private</code>. This is the foundation. The user of the object should not know exactly how data is stored (in a HashMap, an array, or a text file).</li>
  <li><b>Invariants (Integrity Protection)</b>: This is the most important part. The object must guarantee that its state is always valid.
    <ul>
      <li><i>Example from chess:</i> If the <code>row</code> field in your <code>Position</code> class is <code>public</code>, someone could write -100 into it. If the field is <code>private</code>, you can write in the setter or constructor:</li>
    </ul>
    
```java
if (row < 0 || row > 7) throw new Exception();
```

<ul>       
  <li>Encapsulation is a guard that prevents "dirty" data from entering the object.</li>   
</ul>
  </li>
  <li><b>Implementation Hiding</b>: You can completely rewrite the internal logic of a method (e.g., replace <code>HashMap</code> with <code>TreeMap</code> in <code>Board.java</code>), and as long as the public method signatures haven't changed, the rest of the code won't even notice.</li>
</ol>
<h1></h1>
</details>

<details>
<summary><b>What is the difference between encapsulation and data hiding?</b></summary>
<h1></h1>
<ul>
  <li><b>Data Hiding</b> is a technical mechanism (the <code>private</code> modifier).</li>
  <li><b>Encapsulation</b> is an architectural principle. it is about the object taking responsibility for its own data.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>How do access modifiers affect inheritance?</b></summary>
<h1></h1>
Access modifiers determine which part of the parent's "inheritance" will be available to the "child" and what remains a family secret.

<b>Visibility in inheritance:</b>
<ul>
  <li><b>private</b>: Not inherited. The successor doesn't even know the parent's private fields exist. If the <code>color</code> field in <code>Piece</code> is private, you cannot access it directly in <code>Pawn</code>—only via public/protected getters.</li>
  <li><b>default (package-private)</b>: Inherited and accessible only if the successor is in the same package as the parent.</li>
  <li><b>protected</b>: Inherited and accessible to the successor always, even if it is in a different package. This is the "gold standard" for methods needed only within the hierarchy (e.g., <code>calculateValidMoves()</code>).</li>
  <li><b>public</b>: Accessible always and to everyone.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>What is the most restrictive modifier?</b></summary>
<h1></h1>
The strictest is <b>private</b>.
<ul>
  <li><b>Scope:</b> Only inside the curly braces <code>{}</code> of the class where it is declared.</li>
  <li><b>Purpose:</b> It is the foundation of encapsulation. We "lock" data inside so no one can ruin it from the outside.</li>
</ul>
<h1></h1>
</details>

## **Advanced**

<details>
<summary><b>What are best practices for choosing access levels?</b></summary>
<h1></h1>
<ul>
  <li><b>Start with private:</b> This is Rule #1. Make everything private by default. Only open access (making a field <code>default</code> or <code>public</code>) when it is absolutely necessary. This minimizes the "blast radius" when changing code.</li>
  <li><b>Avoid public fields:</b> Fields should almost always be <code>private</code>. Access them through methods (getters/setters or, better yet, behavior methods like <code>applyMove()</code>). The only exception is <code>public static final</code> constants.</li>
  <li><b>Careful with protected:</b> Use it only if you are designing a class for extension. If you aren't sure someone will inherit from your class in another package, don't make fields <code>protected</code>.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>How do nested classes interact with access modifiers?</b></summary>
<h1></h1>
Unlike outer classes, which can only be <code>public</code> or <code>package-private</code>, nested classes can use all four access levels:
<ul>
  <li><b>private</b>: The nested class is visible only within its outer class. This is often used to implement patterns, such as <code>Node</code> inside <code>LinkedList</code> or <code>Map.Entry</code> inside specific map implementations.</li>
  <li><b>protected</b>: The class is visible within the package and to all successors of the outer class.</li>
  <li><b>package-private (default)</b>: Visible only within the package.</li>
  <li><b>public</b>: Visible to the whole world.</li>
</ul>
<b>Most important feature:</b> The outer and nested classes have full access to each other's private members. From the JVM's perspective, they are considered parts of the same entity.
<h1></h1>
</details>

<details>
<summary><b>How do access modifiers affect testing?</b></summary>
<h1></h1>
The main problem: "I want to test the complex logic of a private method, but my test doesn't see it."

<b>Main strategies and their impact:</b>
<ol>
  <li><b>Testing via Public API (The Gold Standard)</b>:
    <ul>
      <li><i>Approach:</i> We test only public methods. If a private method works incorrectly, it will manifest as an incorrect result in a public method.</li>
      <li><i>Pro:</i> Tests don't depend on internal implementation. You can completely rewrite private methods, and tests won't break.</li>
      <li><i>Con:</i> Sometimes private logic is so complex that covering all its branches through a public entry point is extremely difficult.</li>
    </ul>
  </li>
  <li><b>Using Package-Private (Default) access</b>:
    <ul>
      <li><i>Approach:</i> Make the method available by default (without a modifier). If the test is in the same package (e.g., in the <code>src/test/java/com/game/logic</code> folder), it will see this method.</li>
      <li><i>Pro:</i> Easy access for tests without exposing the method to the whole world (public).</li>
      <li><i>Con:</i> Perfect encapsulation is compromised.</li>
    </ul>
  </li>
  <li><b>@VisibleForTesting Annotation</b>:
    <ul>
      <li><i>Approach:</i> Technically, it remains package-private or protected, but the annotation (from Google Guava or Android libraries) warns other developers: "Do not call this in production code; access is open only for testing."</li>
    </ul>
  </li>
</ol>
<h1></h1>
</details>

<details>
<summary><b>What are common mistakes when using public?</b></summary>
<h1></h1>
<ul>
  <li><b>Public fields (Exposing State)</b>: This is a classic mistake. Class fields should almost never be <code>public</code>. The problem: You lose control over the data. Any class can change the field value bypassing your object's logic.</li>
  <li><b>"Leaking" internal collections (Leaking Internals)</b>: A frequent error for Middle developers: making a field <code>private</code> but returning a direct reference to it through a <code>public</code> getter.</li>
  <li><b>Public methods that should be implementation details.</b></li>
  <li><b>Public classes that could have been hidden</b>: If a class is used only within one package, there is no point in making it <code>public</code>.</li>
</ul>
<h1></h1>
</details>

<details>
<summary><b>How does reflection bypass access modifiers?</b></summary>
<h1></h1>
Reflection bypasses access modifiers using the <code>setAccessible(true)</code> method of the <code>AccessibleObject</code> class. This allows frameworks to work with objects without changing their public API.

However, this does not make modifiers useless: they protect against compilation errors and accidental use, and modern Java module systems (Jigsaw) can block even reflective access at the JVM level.
<h1></h1>
</details>
