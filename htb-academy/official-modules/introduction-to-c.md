# Introduction to C\#

## Cheat Sheet

### Basic Syntax

<table><thead><tr><th width="282">Content</th><th>Description</th></tr></thead><tbody><tr><td>Main Method</td><td>The main entry point for all C# programs. Defined as: <code>static void Main(string[] args) { }</code></td></tr><tr><td>Case Sensitivity</td><td>C# is case-sensitive. For instance, <code>MyVariable</code>, <code>myvariable</code>, and <code>myVariable</code> would be three different identifiers.</td></tr><tr><td>Identifiers</td><td>Names given to entities such as variables, methods, etc. Must start with a letter (A-Z or a-z), an underscore (_), followed by zero or more letters, underscores, and digits (0-9).</td></tr><tr><td>Keywords</td><td>Predefined reserved words with special meanings that cannot be used as identifiers. Examples: <code>public</code>, <code>class</code>, <code>void</code>, etc.</td></tr><tr><td>The ;</td><td>In C#, the semicolon is a statement terminator. Each statement must end with a semicolon. Example: <code>int x = 10;</code></td></tr><tr><td>Statements &#x26; Expressions</td><td>A statement performs an action, e.g., <code>x = 7;</code>. An expression is a construct comprising variables, operators, and method invocations evaluated to a single value, e.g., <code>x + 7</code>.</td></tr><tr><td>Blocks of Code</td><td>Blocks are used to group two or more C# statements and are defined by braces <code>{}</code>. Example: <code>{ int x = 7; Console.WriteLine(x); }</code></td></tr><tr><td>Comments</td><td>Comments are used to explain code and are ignored by the compiler. Single-line comments start with <code>//</code>. Multi-line comments start with <code>/*</code> and end with <code>*/</code>.</td></tr><tr><td>Read Compiler Errors</td><td>Compiler errors indicate issues in your code that prevent it from compiling. They often include the line number and a description of the error, which can guide you towards resolving the issue.</td></tr></tbody></table>

### Variables, Constants, and Data Types

<table><thead><tr><th width="200">Content</th><th>Description</th></tr></thead><tbody><tr><td>Variables</td><td>Variables are storage locations, each defined with a specific data type. They are declared using the syntax: <code>dataType variableName;</code> <code>int num;</code></td></tr><tr><td>Constants</td><td>Constants are similar to variables, but, as the name suggests, their value remains constant throughout the program. They are declared using the <code>const</code> keyword. <code>const double Pi = 3.14159;</code></td></tr><tr><td>Enums</td><td>Enum is short for "enumerations", which are a distinct type consisting of a set of named constants. Declared using the <code>enum</code> keyword. <code>enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};</code></td></tr><tr><td>Data Types</td><td>Data types specify the data type that a valid C# variable can hold. C# has several data types, including <code>int</code>, <code>double</code>, <code>char</code>, <code>bool</code>, and <code>string</code>. Each has its own range of values and behaviours.</td></tr></tbody></table>

### Operators and Type Conversion

<table><thead><tr><th width="289">Content</th><th>Description</th></tr></thead><tbody><tr><td>Arithmetic Operators</td><td>These include <code>+</code> (addition), <code>-</code> (subtraction), <code>*</code> (multiplication), <code>/</code> (division), <code>%</code> (modulus) and more.</td></tr><tr><td>Relational Operators</td><td>These include <code>==</code> (equal to), <code>!=</code> (not equal to), <code>&#x3C;</code> (less than), <code>></code> (greater than), <code>&#x3C;=</code> (less than or equal to) and <code>>=</code> (greater than or equal to).</td></tr><tr><td>Logical Operators</td><td>These include <code>&#x26;&#x26;</code> (logical AND), `</td></tr><tr><td>Bitwise Operators</td><td>These perform operations on binary representations of numbers. They include <code>&#x26;</code> (AND), `</td></tr><tr><td>Assignment Operators</td><td>The assignment operator is <code>=</code>. There are also compound assignment operators like <code>+=</code>, <code>-=</code>, etc.</td></tr><tr><td>Unary Operators</td><td>These operators work with only one operand. They include <code>++</code>, <code>--</code>, and the logical negation operator <code>!</code>.</td></tr><tr><td>Ternary Operator</td><td>A shorthand for conditional statements. Syntax: <code>(condition) ? true_expression : false_expression</code>.</td></tr><tr><td>Null Conditional Operators</td><td>Used to simplify checking for null values, denoted as <code>?.</code>.</td></tr><tr><td>Null-coalescing Operator</td><td>Used to define a default value for nullable value types or reference types, denoted as <code>??</code>.</td></tr><tr><td>Implicit Type Conversion</td><td>Also known as widening conversion, it is done automatically by the compiler where no data loss is expected. Example: converting an integer to a float.</td></tr><tr><td>Explicit Type Conversion</td><td>Also known as narrowing conversion, the programmer must do it manually when there might be data loss. Example: converting a float to an integer.</td></tr><tr><td>Type Checking 'is'</td><td>The 'is' keyword checks if an object is of a certain type.</td></tr><tr><td>Type Checking 'as'</td><td>The 'as' keyword performs certain types of conversions between compatible reference types.</td></tr></tbody></table>

### Namespaces

| Content                                       | Description                                                                                                                                                                                          |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Creating and Organizing Code Using Namespaces | Namespaces are used to organise code and create globally unique types. Declare a namespace with `namespace` keyword followed by name and body enclosed in `{}`. `namespace MyNamespace { // code }`. |
| Importing and Using Namespaces in C# Programs | Use the `using` directive at the beginning of your code to include a namespace in your program. `using System;`                                                                                      |
| Resolving Naming Conflicts with Namespaces    | If two namespaces contain types with the same name, fully qualify the name by including the namespace to avoid conflict. `System.Console.WriteLine("Hello, world!");`                                |

### Console I/O

<table><thead><tr><th width="237">Content</th><th>Description</th></tr></thead><tbody><tr><td>Console.Read</td><td>Reads the next character from the standard input stream. Returns the ASCII value of the character read, or -1 if no more characters are available.</td></tr><tr><td>Console.ReadLine</td><td>Reads the next line of characters from the standard input stream. Returns a string containing the line read or null if no more lines are available.</td></tr><tr><td>Console.Write</td><td>Writes data to the standard output stream without a newline character at the end. Can take a string or other data types as argument(s). <code>Console.Write("Hello, world");</code></td></tr><tr><td>Console.WriteLine</td><td>Similar to <code>Console.Write</code>, but appends a newline character () at the end, causing subsequent output to appear on a new line. <code>Console.WriteLine("Hello, world");</code></td></tr></tbody></table>

### Control Statements and Loops

<table><thead><tr><th width="146">Content</th><th>Description</th></tr></thead><tbody><tr><td>if</td><td>A control statement executes a block of code if a specified condition is <code>true</code>.</td></tr><tr><td>else</td><td>Used after an <code>if</code> statement. Its block of code executes if the <code>if</code> condition is <code>false</code>.</td></tr><tr><td>else if</td><td>Used after an <code>if</code> or another <code>else if</code> to test multiple conditions.</td></tr><tr><td>switch</td><td>A control statement that selects one of many code blocks to be executed.</td></tr><tr><td>for</td><td>A loop that repeats a block of code a certain number of times, defined at the start of the loop.</td></tr><tr><td>while</td><td>A loop that repeats a block of code as long as a specified condition is <code>true</code>.</td></tr><tr><td>do-while</td><td>Similar to the <code>while</code> loop, but checks the condition at the end of the loop. This means the loop will always run at least once.</td></tr><tr><td>break</td><td>Used to exit a loop or a <code>switch</code> statement prematurely.</td></tr><tr><td>continue</td><td>Skips the rest of the current iteration and moves directly to the next iteration of the loop.</td></tr><tr><td>goto</td><td>Transfers control to another part of the program marked with a label.</td></tr></tbody></table>

### Arrays

| Content                       | Description                                                                                                                                                              |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Arrays in C#                  | An array is a collection of elements of the same type stored in contiguous memory locations. It is declared with the type followed by square brackets `[]`. `int[] arr;` |
| Multidimensional Arrays in C# | C# supports multidimensional arrays, declared with commas in the square brackets. `int[,] arr;`                                                                          |
| The Array Class               | Provides various properties and methods to work with arrays. It is defined within the `System` namespace.                                                                |
| Array.Sort()                  | A method that sorts the elements in an entire one-dimensional Array. `Array.Sort(arr);`                                                                                  |
| Array.Reverse()               | Reverses the sequence of the elements in the entire one-dimensional Array or in a portion of it. `Array.Reverse(arr);`                                                   |
| Array.IndexOf()               | Returns the index of the first occurrence of a value in a one-dimensional Array or in a portion of it. `int index = Array.IndexOf(arr, value);`                          |
| Array.Clear()                 | Sets a range of elements in the Array to zero, to false, or to null, depending on the element type. `Array.Clear(arr, startIndex, length);`                              |

### Strings

<table><thead><tr><th width="269">Content</th><th>Description</th></tr></thead><tbody><tr><td>String Declaration</td><td>In C#, a string is declared as: <code>string str = "Hello World";</code></td></tr><tr><td>String Concatenation</td><td>Strings can be concatenated using the <code>+</code> operator. Example: <code>string str = "Hello" + " World";</code></td></tr><tr><td>String Interpolation</td><td>Insert variables directly in a string with <code>{}</code>. Example: <code>string str = $"Hello {name}";</code></td></tr><tr><td>Length Property</td><td>To get the length of a string, use the <code>Length</code> property. Example: <code>int length = str.Length;</code></td></tr><tr><td>Indexing</td><td>Access individual characters in a string with an index, starting from 0. Example: <code>char ch = str[0];</code></td></tr><tr><td>Substrings</td><td>Extract part of a string using the <code>Substring</code> method. Example: <code>string substr = str.Substring(startIndex, length);</code></td></tr><tr><td>String Comparison</td><td>Compare two strings using the <code>==</code> operator or the <code>String.Equals</code> method.</td></tr><tr><td>String Case Conversion</td><td>Convert to uppercase or lowercase using the <code>ToUpper()</code> and <code>ToLower()</code> methods.</td></tr><tr><td>Trimming Strings</td><td>Remove whitespace from start/end of a string with <code>Trim()</code>, <code>TrimStart()</code>, or <code>TrimEnd()</code>.</td></tr><tr><td>Searching in Strings</td><td>Find a substring or character using the <code>IndexOf()</code> or <code>Contains()</code> methods.</td></tr><tr><td>Replacing in Strings</td><td>Replace a substring or character using the <code>Replace()</code> method.</td></tr></tbody></table>

### Collections

<table><thead><tr><th width="286">Content</th><th>Description</th></tr></thead><tbody><tr><td>Iterating through a collection</td><td>You can iterate through a collection using a <code>foreach</code> loop. <code>foreach(var item in collection) { // actions }</code>.</td></tr><tr><td>List</td><td>A list is an ordered collection of items that can contain duplicates. Use the <code>Add</code>, <code>Remove</code>, and <code>Sort</code> methods to manipulate a list.</td></tr><tr><td>Dictionary</td><td>A dictionary is a collection of key-value pairs where each key must be unique. Use the <code>Add</code>, <code>Remove</code>, and <code>TryGetValue</code> methods to manipulate a dictionary.</td></tr><tr><td>HashSet</td><td>A HashSet is an unordered collection of unique elements. It provides high-performance set operations like union, intersection, and difference.</td></tr><tr><td>List vs Dictionary vs HashSet</td><td>Lists are best for accessing elements by index or iterating in order. Dictionaries provide fast lookups for elements based on a unique key. HashSets provide fast lookups like dictionaries but only store individual values instead of key-value pairs.</td></tr><tr><td>Performance considerations</td><td>In general, Dictionaries and HashSets provide faster lookups than Lists, especially for large collections. However, the choice between these depends on the specific requirements of your program.</td></tr></tbody></table>

### LINQ (Language Integrated Query)

| Content                   | Description                                                                                                                                                                        |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| LINQ Query Syntax         | LINQ queries consist of three parts: `from clause`, `where clause`, and `select clause`. `var result = from s in source where s.condition select s.property;`                      |
| Where                     | Filters a collection based on a condition. `var result = data.Where(x => x > 5);`                                                                                                  |
| Select                    | Projects each sequence element into a new form. `var result = data.Select(x => x * 2);`                                                                                            |
| OrderBy/OrderByDescending | Sorts the elements of a sequence in ascending/descending order. `var result = data.OrderBy(x => x);` or `var result = data.OrderByDescending(x => x);`                             |
| GroupBy                   | Groups the elements of a sequence according to a specified key selector function. Example: `var result = data.GroupBy(x => x.Key);`                                                |
| Join                      | Joins two collections based on matching keys. `var result = list1.Join(list2, x => x.Key, y => y.Key, (x, y) => new { X = x, Y = y });`                                            |
| Aggregate                 | Applies an accumulator function over a sequence. `var result = data.Aggregate((a, b) => a + b);`                                                                                   |
| Count/Sum/Average/Min/Max | Performs calculations on a sequence of values. `var count = data.Count();`, `var sum = data.Sum();`, `var avg = data.Average();`, `var min = data.Min();`, `var max = data.Max();` |

### Methods and Exception Handling

<table><thead><tr><th width="293">Content</th><th>Description</th></tr></thead><tbody><tr><td>Creating a method</td><td>Methods are declared with a return type, name, and parameters. <code>public int Add(int x, int y) { return x + y; }</code></td></tr><tr><td>Method Scope</td><td>The scope of a method is the region of code within which a method can be accessed. Typically defined by the access modifier (<code>public</code>, <code>private</code>, etc.).</td></tr><tr><td>Static vs Non-Static Methods</td><td>Static methods belong to the class itself and can be called without creating an instance of the class. Non-static methods belong to an instance of the class.</td></tr><tr><td>try catch finally</td><td><code>try</code> contains code that might throw an exception. <code>catch</code> defines what to do if an exception is thrown in the try block. <code>finally</code> contains code that will always be executed, whether an exception is thrown or not.</td></tr><tr><td>throw</td><td>The <code>throw</code> keyword is used to throw an exception from within your code explicitly. <code>throw new Exception("An error occurred.");</code></td></tr></tbody></table>

### Lambda Expressions

| Content                                | Description                                                                                                                            |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Simple Lambda Expression               | A lambda expression with no parameters, represented as: `() => SomeMethod();`                                                          |
| Lambda Expression with Parameters      | A lambda expression with one or more parameters. `(param1, param2) => param1 + param2;`                                                |
| Lambda Expression with Statement Block | A lambda expression with multiple statements enclosed in `{}`. `(param1, param2) => { var result = param1 + param2; return result; };` |

### Libraries

<table><thead><tr><th width="217">Content</th><th>Description</th></tr></thead><tbody><tr><td>NuGet</td><td>NuGet is a package manager for .NET. It allows you to add third-party libraries to your project with ease. You can add a NuGet package using the Package Manager Console or the Manage NuGet Packages dialogue box in an IDE.</td></tr><tr><td>Manual Referencing</td><td>If a library isn't available on NuGet, or you have a local library that you want to use, you can manually add a reference to it in your project.</td></tr></tbody></table>

### Object-Oriented Programming

<table><thead><tr><th width="235">Content</th><th>Description</th></tr></thead><tbody><tr><td>Classes</td><td>A blueprint for creating objects. Defined with the <code>class</code> keyword.</td></tr><tr><td>Accessors</td><td>Methods that get and set the value of class properties (<code>get</code> and <code>set</code>).</td></tr><tr><td>Automatic Properties</td><td>C# allows you to define a property without specifying a field (also known as auto-implemented properties). <code>public string Name { get; set; }</code></td></tr><tr><td>Structs</td><td>Similar to classes but are value types and don't support inheritance. Defined with the <code>struct</code> keyword.</td></tr><tr><td>Encapsulation</td><td>The process of hiding internal details and exposing only what's necessary. Achieved with access modifiers like <code>public</code>, <code>private</code>, etc.</td></tr><tr><td>Inheritance</td><td>The ability for one class to inherit properties and methods from another class. Defined using the <code>:</code> symbol. <code>public class ChildClass : ParentClass</code></td></tr><tr><td>Single Inheritance</td><td>A class can inherit from one base class only.</td></tr><tr><td>Multilevel Inheritance</td><td>A chain of inheritance where a class inherits from a base class, which itself inherits from another base class, and so on.</td></tr><tr><td>base</td><td>The <code>base</code> keyword is used to access members of the base class from within a derived class. <code>base.MethodName()</code></td></tr></tbody></table>

### Polymorphism and Abstraction

<table><thead><tr><th width="226">Content</th><th>Description</th></tr></thead><tbody><tr><td>Polymorphism</td><td>Allows objects of different types to be treated as objects of a common supertype. Enables us to write more generic and reusable code.</td></tr><tr><td>Method Overloading</td><td>The ability to define multiple methods in the same scope with the same name but different parameters.</td></tr><tr><td>Method Overriding</td><td>Allows a subclass to provide a specific implementation of a method that is already provided by its superclass. Achieved using <code>override</code> keyword.</td></tr><tr><td>Operator Overloading</td><td>The ability to redefine or overload most of the built-in operators available in C#. This allows using operators with user-defined types as well.</td></tr><tr><td>Property Overriding</td><td>Similar to method overriding but for properties. Allows a subclass to override a property in the base class.</td></tr><tr><td>Abstraction</td><td>Hiding complex details and providing a simpler interface. In C#, it's achieved through abstract classes and interfaces. Abstract classes contain abstract methods that have a declaration but no implementation.</td></tr></tbody></table>

### Generics

<table><thead><tr><th width="239">Content</th><th>Description</th></tr></thead><tbody><tr><td>Benefits of Generics</td><td>Generics increase the reusability of code, type safety, and performance by eliminating boxing and unboxing.</td></tr><tr><td>Generic Classes</td><td>A class that can be customized to work with a specified data type. <code>public class GenericClass&#x3C;T> { }</code></td></tr><tr><td>Generic Methods</td><td>Methods with a type parameter in its declaration. <code>public T GenericMethod&#x3C;T>(T param) { return param; }</code></td></tr><tr><td>Generic Constraints</td><td>Constraints are used to restrict the types that can be used as arguments for a type parameter in a generic class or method. <code>public class GenericClass&#x3C;T> where T : IComparable { }</code></td></tr></tbody></table>

### File I/O

<table><thead><tr><th width="333">Content</th><th>Description</th></tr></thead><tbody><tr><td>StreamReader</td><td><code>StreamReader</code> is used for reading characters from a byte stream in a particular encoding. <code>StreamReader sr = new StreamReader(path);</code></td></tr><tr><td>Reading Data with StreamReader</td><td>Use <code>sr.ReadToEnd();</code> to read all data.</td></tr><tr><td>StreamWriter</td><td><code>StreamWriter</code> is used for writing characters to a stream in a particular encoding. <code>StreamWriter sw = new StreamWriter(path);</code></td></tr><tr><td>Writing Data with StreamWriter</td><td>Use <code>sw.Write("Hello World");</code> to write data.</td></tr></tbody></table>

### Network I/O

<table><thead><tr><th width="183">Content</th><th>Description</th></tr></thead><tbody><tr><td>HttpClient</td><td><code>HttpClient</code> is a class in .NET used for sending HTTP requests and receiving HTTP responses.</td></tr><tr><td>GetAsync</td><td>Sends a <code>GET</code> request to the specified Uri and returns the response. Example: <code>var response = await client.GetAsync(url);</code></td></tr><tr><td>PostAsync</td><td>Sends a <code>POST</code> request to the specified Uri with a specified content. Example: <code>var response = await client.PostAsync(url, content);</code></td></tr><tr><td>PutAsync</td><td>Sends a <code>PUT</code> request to the specified Uri with a specified content. Example: <code>var response = await client.PutAsync(url, content);</code></td></tr><tr><td>DeleteAsync</td><td>Sends a <code>DELETE</code> request to the specified Uri and returns the response. Example: <code>var response = await client.DeleteAsync(url);</code></td></tr></tbody></table>

### Asynchronous Programming

| Content                            | Description                                                                                                                                                                                                                           |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| async & await                      | `async` modifier indicates that a method, lambda expression, or anonymous method is asynchronous. `await` operator is applied to a task in an `async` method to suspend the execution of the method until the awaited task completes. |
| Tasks                              | A `Task` represents a single operation that does not return a value and that usually executes asynchronously. A `Task<TResult>` represents a single operation that returns a value.                                                   |
| Task Cancellation                  | The cooperative cancellation model provided by .NET allows you to cancel running tasks using `CancellationTokenSource` and `CancellationToken`.                                                                                       |
| Exception Handling with Async Code | In async methods, use `try-catch` blocks to handle exceptions. Exceptions are propagated when the task is awaited.                                                                                                                    |



## Arrays

***

Arrays are a crucial aspect of C# programming and most other programming languages as well. Their importance is due to their ability to store multiple values of the same type in a structured manner.

### Arrays in C\#

To declare an array in C#, the syntax involves specifying the type of elements that the array will hold, followed by square brackets `[]`. This tells the compiler that this variable will hold an array, but it does not yet specify the size or elements of the array.

Code: csharp

```csharp
int[] array;
```

This line of code simply declares an array named `array` that will hold integers. The array does not yet exist in memory at this point - it is simply a declaration.

To create the array in memory, we instantiate it using the `new` keyword, followed by the type of the array elements and the number of elements enclosed in square brackets.

Code: csharp

```csharp
array = new int[5];
```

In this line of code, we are telling the compiler to create an array of integers with a size of 5. At this point, the `array` variable references an array of five integer elements, all of which are initialised to 0, the default value for integers.

Arrays can also be declared, instantiated, and initialised in a single line of code.

Code: csharp

```csharp
int[] array = new int[] { 1, 2, 3, 4, 5 };
```

This line declares an array of integers, creates it with a size of 5, and assigns the specified values to the five elements.

### Multidimensional Arrays in C\#

C# supports multidimensional arrays. This concept can be extended to two, three, or more dimensions. A two-dimensional array can be considered a table with rows and columns.

The syntax for declaring a two-dimensional array involves specifying the type of elements that the array will hold, followed by two sets of square brackets `[,]`.

Code: csharp

```csharp
int[,] matrix;
```

Here, `matrix` is a two-dimensional array that will hold integers. The new keyword is used to instantiate the matrix, followed by the type of the array elements and the number of rows and columns enclosed in square brackets.

Code: csharp

```csharp
matrix = new int[3, 3];
```

This line creates a matrix with 3 rows and 3 columns.

Two-dimensional arrays can also be declared, instantiated, and initialised in a single line of code.

Code: csharp

```csharp
int[,] matrix = new int[,] { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };

// Use the GetLength method to get the number of rows (dimension 0) and columns (dimension 1)
for (int i = 0; i < matrix.GetLength(0); i++) {
    for (int j = 0; j < matrix.GetLength(1); j++)
    {
        // Access each element of the array using the indices
        Console.Write(matrix[i, j] + " ");
    }
    Console.WriteLine(); // Print a newline at the end of each row
}
```

This example will output:

```
1 2 3 
4 5 6 
7 8 9 
```

This representation shows the `matrix` as it is, conceptually, a 3x3 grid. Each row of numbers in the output corresponds to a row in the matrix, and each number in a row corresponds to a column for that row in the matrix.

You can access the elements in the array using their indices. In a 2D array, the first index represents the row number, and the second index represents the column number. For instance, `matrix[0, 1];` will access the second element of the first row.

### The Array Class

The `Array` class, part of the `System` namespace, offers various methods that help in efficiently managing and manipulating arrays.

The distinction between `Array` and `array` in C# can be somewhat confusing, primarily because both represent similar concepts but in different ways. `Array` is an abstract base class provided by the `System` namespace in `C#`. It provides various properties and methods like `Length`, `Sort()`, `Reverse()`, and many more that allow you to manipulate arrays.

An `array`, on the other hand, is a fundamental data type in C#. It is a low-level construct supported directly by the language. An `array` represents a fixed-size, sequential collection of elements of a specific type, such as int, string, or custom objects.

Let's look at an example:

Code: csharp

```csharp
int[] arr = new int[5]; //arr is an array
```

Here, `arr` is an array of integers. You can add, retrieve, or modify elements using their indices.

Code: csharp

```csharp
arr[0] = 1; // Assigns the value 1 to the first element of the array.
```

On the other hand, if you want to use the functionality provided by the `Array` class on this array:

Code: csharp

```csharp
Array.Sort(arr); // Uses the Sort method from Array class to sort 'arr'.
```

#### Array.Sort()

The `Sort()` method is used to sort the elements in an entire one-dimensional `Array` or, alternatively, a portion of an `Array`.

Code: csharp

```csharp
int[] numbers = {8, 2, 6, 3, 1};
Array.Sort(numbers);
```

After sorting, our array would look like:`{1, 2, 3, 6, 8}`.

#### Array.Reverse()

The `Reverse()` method reverses the sequence of the elements in the entire one-dimensional `Array` or a portion of it.

For instance:

Code: csharp

```csharp
int[] numbers = {1, 2, 3};
Array.Reverse(numbers);
```

The result will be a reversed array: `{3, 2, 1}`.

#### Array.IndexOf()

The `IndexOf()` method returns the index of the first occurrence of a value in a one-dimensional `Array` or in a portion of the `Array`.

Consider this example:

Code: csharp

```csharp
int[] numbers = {1, 2, 3};
int index = Array.IndexOf(numbers, 2);
```

The variable `index` now holds the value `1`, which is the index of number `2` in the array.

#### Array.Clear()

The `Clear()` method sets a range of elements in the `Array` to zero (in case of numeric types), false (in case of boolean types), or null (in case of reference types).

Take a look at this example:

Code: csharp

```csharp
int[] numbers = {1, 2, 3};
Array.Clear(numbers, 0, numbers.Length);
```

Now all elements in our array are set to zero: `{0, 0, 0}`.



## Strings

In C#, a string is not simply a character array, although it can be thought of as akin to an array of characters for some operations. In essence, a string is an instance of the `System.String` class that provides a range of sophisticated methods and properties, encapsulating a sequence of Unicode characters.

The main differentiation between a string and a character array is that strings in C# are immutable, meaning that once created, they cannot be changed. Any operations that appear to alter the string are actually creating a new string and discarding the old one. This design enhances security and improves performance for static or rarely changing text.

On the other hand, character arrays are mutable, and individual elements can be changed freely. This mutability comes at the cost of not having built-in text manipulation and comparison methods, as strings do.

For instance, we create a string as follows:

Code: csharp

```csharp
string welcomeMessage = "Welcome to Academy!";
```

Once you have a string in C#, there are many operations you can perform on it. The `Length` property, for example, returns the number of characters in the string.

Code: csharp

```csharp
Console.WriteLine(welcomeMessage.Length); // Outputs: 19
```

This tells us that our `welcomeMessage` string is 19 characters long.

String concatenation is another operation that is used frequently. It is performed using the `+` operator.

Code: csharp

```csharp
string firstString = "Welcome ";
string secondString = "to Academy!";
string concatenatedString = firstString + secondString;
Console.WriteLine(concatenatedString); // Outputs: "Welcome to Academy!"
```

When it comes to manipulating the casing of strings, the `String` class provides the `ToLower` and `ToUpper` methods. `ToLower` converts all the characters in a string to lowercase, while `ToUpper` converts them all to uppercase.

Code: csharp

```csharp
string lowerCaseString = welcomeMessage.ToLower();
Console.WriteLine(lowerCaseString); // Outputs: "welcome to academy!"

string upperCaseString = welcomeMessage.ToUpper();
Console.WriteLine(upperCaseString); // Outputs: "WELCOME TO ACADEMY!"
```

There are also methods to check whether a string starts or ends with a specific substring. These are the `StartsWith` and `EndsWith` methods, respectively.

Code: csharp

```csharp
bool startsWithWelcome = welcomeMessage.StartsWith("Welcome");
Console.WriteLine(startsWithWelcome); // Outputs: True

bool endsWithProgramming = welcomeMessage.EndsWith("Academy!");
Console.WriteLine(endsWithProgramming); // Outputs: True
```

A common requirement in programming is to determine whether a specific substring exists within a larger string. This can be accomplished with the `Contains` method.

Code: csharp

```csharp
bool containsCsharp = welcomeMessage.Contains("C#");
Console.WriteLine(containsCsharp); // Outputs: False
```

Sometimes, you may need to replace all occurrences of a substring within a string with another substring. The `Replace` method allows you to do this.

Code: csharp

```csharp
string replacedMessage = welcomeMessage.Replace("Academy", "HTB Academy");
Console.WriteLine(replacedMessage); // Outputs: "Welcome to HTB Academy!"
```

You can use the `Equals` method or the `==` operator when comparing two strings for equality. Both perform a case-sensitive comparison by default.

Code: csharp

```csharp
string str1 = "Welcome";
string str2 = "welcome";
bool areEqual = str1.Equals(str2);
Console.WriteLine(areEqual); // Outputs: False
```

In addition to the basic operations mentioned above, there are several advanced operations that C# offers for string manipulation.

One of these operations is string interpolation, which provides a more readable and convenient syntax to format strings. Instead of using complicated string concatenation to include variable values within strings, string interpolation allows us to insert expressions inside string literals directly. To create an interpolated string in C#, prefix the string with a `$` symbol, and enclose any variables or expressions you want to interpolate in curly braces `{}`. When the string is processed, these expressions are replaced by their evaluated string representations.

Code: csharp

```csharp
string name = "Alice";
string greeting = $"Hello, {name}!";
Console.WriteLine(greeting); // Outputs: "Hello, Alice!"
```

In the above example, `{name}` inside the string literal is replaced by the value of the variable `name`.

Another important string operation is trimming, which is performed using the `Trim` method. This is commonly used to remove a string's leading and trailing white space.

Code: csharp

```csharp
string paddedString = "    Extra spaces here    ";
string trimmedString = paddedString.Trim();
Console.WriteLine(trimmedString); // Outputs: "Extra spaces here"
```

The `Substring` method extracts a portion of a string starting at a specified index and continuing for a specified length. For instance:

Code: csharp

```csharp
string fullString = "Hello, World!";
string partialString = fullString.Substring(7, 5);
Console.WriteLine(partialString); // Outputs: "World"
```

In the above example, `Substring(7, 5)` returns a new string starting at index 7 and of length 5 from the `fullString`.

Moreover, using the `Split` method, strings can be split into arrays of substrings based on delimiters. This is especially useful when parsing input or handling data that comes in string form.

Code: csharp

```csharp
string sentence = "This is a sentence.";
string[] words = sentence.Split(' ');
foreach (string word in words)
{
    Console.WriteLine(word);
}
// Outputs: 
// "This"
// "is"
// "a"
// "sentence."
```

In this example, the `Split` method splits the `sentence` string into an array of words based on the space character delimiter.

Lastly, the `Join` method concatenates all elements in a string array or collection, using a specified separator between each element.

Code: csharp

```csharp
string[] words = { "This", "is", "a", "sentence" };
string sentence = string.Join(" ", words);
Console.WriteLine(sentence); // Outputs: "This is a sentence"
```

In this case, `Join` constructs a single string from all the elements in the `words` array, with a space character as the separator.



## Collections

***

In C#, a collection is used to group related objects. Collections provide a more flexible way to work with groups of objects, as unlike arrays, the group of objects you work with can grow and shrink dynamically as the demands of the application change. Collections are defined in the `System.Collections` namespace.

### Iterating through a collection

The `foreach` loop is an efficient and straightforward way to iterate through any collection. It automatically moves to the next item in the collection at the end of each loop iteration, making it an excellent choice for reading collections. Suppose you want to modify the collection while iterating over it. In that case, you might need to use a different looping construct, like a `for` loop, as `foreach` does not support collection modification during iteration.

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

for (int i = 0; i < numbers.Count; i++)
{
    // Modify the element at index i
    numbers[i] *= 2;
}

foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

We use a `for` loop to iterate over the numbers list in this example. The loop variable `i` represents the index of each element in the list. Within the loop, we can modify the element at the current index by performing the desired operation, in this case, multiplying it by 2. After the `for` loop completes, we use a `foreach` loop to iterate over the modified `numbers` list and print each number to the console.

### List

A `List<T>` is one of the most commonly used types in .NET, especially when we need a resizable array-like collection. This type is found in the `System.Collections.Generic` namespace is a generic class which supports storing values of any type. However, all `List<T>` elements must be the same type.

```csharp
List<string> namesList = new List<string>();

// Adding elements to the list
namesList.Add("John");
namesList.Add("Jane");
namesList.Add("Alice");

// Accessing elements by index
string firstElement = namesList[0]; // O(1) indexed access

// Modifying an element
namesList[1] = "Emily";

// Checking if an element exists
bool hasAlice = namesList.Contains("Alice");

// Removing an element
namesList.Remove("John");

// Iterating over the elements
foreach (string name in namesList)
{
    Console.WriteLine(name);
}
```

A `List<T>` provides the advantage of dynamic resizing compared to an array. However, this also means that a `List<T>` generally uses more memory than an array, as it allocates extra space to allow for potential growth. If the size of your collection is fixed, using an array could be more memory-efficient.

However, the flexibility and utility of the `List<T>` class methods often outweigh the minor performance and memory usage benefits of arrays in many scenarios. This is especially true in applications where the exact count of elements may change over time.

### Dictionary

A `Dictionary<TKey, TValue>` is a collection that stores and retrieves data using a key-value relationship. It is part of the `System.Collections.Generic` namespace in C#.

To use a `Dictionary<TKey, TValue>`, specify the key type (`TKey`) and the value (`TValue`) in the angle brackets. For example, `Dictionary<int, string>` indicates a dictionary where the keys are integers and the values are strings.

```csharp
Dictionary<string, int> studentGrades = new Dictionary<string, int>();

// Adding key-value pairs to the dictionary
studentGrades.Add("John", 85);
studentGrades.Add("Jane", 92);
studentGrades.Add("Alice", 78);

// Accessing values by key
int johnGrade = studentGrades["John"]; // O(1) lookup by key

// Modifying an existing value
studentGrades["Jane"] = 95;

// Checking if a key exists
bool hasAlice = studentGrades.ContainsKey("Alice");

// Removing a key-value pair
studentGrades.Remove("John");

// Iterating over the key-value pairs
foreach (KeyValuePair<string, int> pair in studentGrades)
{
    Console.WriteLine($"Name: {pair.Key}, Grade: {pair.Value}");
}
```

### HashSet

A `HashSet<T>` collection stores an unordered set of unique elements. The primary characteristic of a `HashSet` is its ability to store unique elements, completely disallowing duplication. Adding elements to a `HashSet` will check if the element already exists before adding it. This makes `HashSet` an optimal choice when you need to store a collection of items without any duplicates and do not require a specific order.

To use a `HashSet`, specify the type of elements (`T`) within the angle brackets. For example, `HashSet<int>` indicates a set of integers.

```csharp
HashSet<string> namesHashSet = new HashSet<string>();

// Adding elements to the set
namesHashSet.Add("John");
namesHashSet.Add("Jane");
namesHashSet.Add("Alice");

// Checking if an element exists
bool hasAlice = namesHashSet.Contains("Alice"); // O(1) membership check

// Removing an element
namesHashSet.Remove("John");

// Iterating over the elements
foreach (string name in namesHashSet)
{
    Console.WriteLine(name);
}
```

### List vs Dictionary vs HashSet

Each collection type has its unique characteristics, behaviours, and use cases.

|                   | List                               | Dictionary                                     | HashSet                                                |
| ----------------- | ---------------------------------- | ---------------------------------------------- | ------------------------------------------------------ |
| Data Structure    | Ordered                            | Key-Value Pairs                                | Unordered, Unique Elements                             |
| Duplication       | Allows duplicates                  | Keys must be unique                            | Ensures uniqueness                                     |
| Access and Lookup | Indexed access by index            | Fast lookup by unique key                      | Membership checks                                      |
| Ordering          | Maintains order                    | No specific order                              | No specific order                                      |
| Element Removal   | By index or value                  | By key                                         | By value                                               |
| Memory Overhead   | Consumes memory based on elements  | Memory for keys and values                     | Memory for unique elements                             |
| Use Cases         | Ordered collection, indexed access | Associating values with keys, key-based lookup | Unordered collection, uniqueness and membership checks |

### Collection Performance

Performance considerations vary for each collection type based on the operations performed and the specific use case.

`Big-O notation` is a notation used in computer science to describe the performance characteristics of an algorithm, specifically its time complexity and space complexity.

In terms of time complexity, `Big-O notation` quantifies the worst-case scenario of an algorithm as the size of the input data approaches infinity. For instance, if an algorithm has a time complexity of `O(n)`, it indicates that the time it takes to execute the algorithm grows linearly with the input data size. On the other hand, an algorithm with a time complexity of `O(n^2)` would suggest that the execution time increases quadratically with the input size.

While analysed less frequently, `Big-O` notation can also describe space complexity by measuring the amount of memory an algorithm needs relative to the input size. For example, an algorithm with a space complexity of `O(1)` uses a constant amount of memory regardless of the input size.

Here are some general performance considerations for `List`, `Dictionary`, and `HashSet`:

|                   | List                                                      | Dictionary                                   | HashSet                                      |
| ----------------- | --------------------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| Access Speed      | Very fast, O(1)                                           | Average: O(1), Worst: O(n)                   | Average: O(1), Worst: O(n)                   |
| Insertion/Removal | Insertion and removal at ends: O(1)                       | Average: O(1), Worst: O(n)                   | Average: O(1), Worst: O(n)                   |
| Searching         | <p>Unsorted: O(n)<br>Sorted (Binary Search): O(log n)</p> | Key-based lookup: Average O(1), Worst O(n)   | Membership check: Average O(1), Worst O(n)   |
| Memory Overhead   | Relatively low                                            | Keys and values, additional structure fields | Unique elements, additional structure fields |

Please note that the access speed represents the time complexity of accessing elements in the collection, whether it's by index (for List) or by key (for Dictionary) or membership check (for HashSet). The performance characteristics in this table are general guidelines and may vary based on the specific implementation and use case.



## LINQ (Language Integrated Query)

***

Language Integrated Query (LINQ) is a feature in C# that provides a consistent model for working with data across various kinds of data sources and formats. You use LINQ to query data with C# irrespective of the data source.

In a more technical sense, LINQ is a set of methods, provided as extension methods in .NET, that provide a universal approach to querying data of any type. This data can be in-memory objects (like lists or arrays), XML, databases, or any other format for which a LINQ provider is available. These methods take lambda expressions as arguments, which behave like in-line functions that work on the dataset being queried.

There are several benefits to using LINQ in your C# applications:

1. `Simplicity`: LINQ simplifies querying and manipulating data by providing a consistent query syntax across different data sources, making code cleaner and more maintainable.
2. `Type Safety`: LINQ is strongly typed, meaning compile-time type checking is performed on query expressions.
3. `Expressiveness`: LINQ offers a rich set of query operators that allow you to express complex data operations concisely and declaratively, making queries easy to read.
4. `Integration`: LINQ is seamlessly integrated into the C# language and can be used with various data sources, including in-memory collections, databases (via LINQ to SQL or Entity Framework), XML, and web services.

### LINQ Query Syntax

LINQ provides two main syntaxes for writing queries: query syntax and method syntax. The query syntax is often preferred for its readability and resemblance to SQL, while the method syntax offers more flexibility and composability. Let us explore both syntaxes with examples.

Consider a simple example where we have a list of integers and want to retrieve all the even numbers from the list:

Code: csharp

```csharp
// This creates a new list of integers named 'numbers' and populates it with the numbers from 1 to 10.
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

// This is a LINQ query that will create a new collection called 'evenNumbers'. 
// The 'from num in numbers' part signifies that we're querying over the 'numbers' list and will refer to each element as 'num'.
// The 'where num % 2 == 0' part is a condition that each number in the list must satisfy to be included in the new collection - in this case, the number must be even. 
// The '%' operator is the modulus operator, which gives the remainder of integer division. So 'num % 2' gives the remainder when 'num' is divided by 2. If this remainder is 0, then the number is even.
// The 'select num' part signifies that if a number satisfies the condition, then it should be included in the 'evenNumbers' collection.
var evenNumbers = from num in numbers
                  where num % 2 == 0
                  select num;

```

In the above code, we use the `from` clause to define a range variable `num` representing each element in the `numbers` list. The `where` clause filters the numbers based on the condition `num % 2 == 0`, selecting only the even numbers. Finally, the `select` clause projects the selected numbers into the `evenNumbers` variable.

The equivalent code using method syntax would look like this:

Code: csharp

```csharp
// This creates a new list of integers named 'numbers' and populates it with the numbers from 1 to 10.
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

// This is a LINQ query using method syntax. It creates a new collection called 'evenNumbers' from the 'numbers' list.
// The 'Where' method filters the 'numbers' list based on the provided lambda expression 'num => num % 2 == 0'.
// The lambda expression takes each number 'num' in the 'numbers' list and returns true if 'num' is even (i.e., if the remainder when 'num' is divided by 2 is 0), and false otherwise.
// The 'Where' method then includes in 'evenNumbers' only those numbers for which the lambda expression returned true.
// As a result, 'evenNumbers' will include all even numbers from the original 'numbers' list. The output will be: 2, 4, 6, 8, 10.
var evenNumbers = numbers.Where(num => num % 2 == 0); // Output: 2, 4, 6, 8, 10
```

In the method syntax, we use the `Where` operator to filter the numbers based on the provided condition.

### LINQ Operators

LINQ provides a series of `query operators`, each performing a specific operation on a data source. The power of LINQ comes from these operators, which can be combined in various ways to compose complex queries.

#### Where

The `Where` operator filters a sequence based on a specified condition.

Code: csharp

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

// This line filters the 'numbers' list using a LINQ query. The query uses a lambda expression to select only the numbers that are even (i.e., numbers where the remainder of the division by 2 is equal to zero). 
// The result is a new collection 'evenNumbers' containing all the even numbers from the original 'numbers' list.
var evenNumbers = numbers.Where(num => num % 2 == 0);

// Output: 2, 4, 6, 8, 10
foreach (var num in evenNumbers)
{
    Console.WriteLine(num);
}
```

#### Select

The `Select` operator projects each element of a sequence into a new form.

Code: csharp

```csharp
List<string> names = new List<string> { "John", "Alice", "Michael" };

// This line uses a LINQ query with the Select method to create a new collection 'upperCaseNames'. 
// The query takes the 'names' collection and applies the 'ToUpper' method to each element. 
// The ToUpper method is a built-in C# method that converts all the characters in a string to uppercase.
// The result is a new collection where all the names from the original 'names' collection are transformed into uppercase.
var upperCaseNames = names.Select(name => name.ToUpper());

// Output: JOHN, ALICE, MICHAEL
foreach (var name in upperCaseNames)
{
    Console.WriteLine(name);
}
```

#### OrderBy/OrderByDescending

The `OrderBy` and `OrderByDescending` operators sort the elements of a sequence in ascending or descending order.

Code: csharp

```csharp
List<int> numbers = new List<int> { 5, 2, 8, 1, 9 };

// The OrderBy method is a LINQ operation that sorts the elements of a collection in ascending order according to a key. In this case, the key is the numbers themselves.
var sortedNumbersAsc = numbers.OrderBy(num => num);

// Output: 1, 2, 5, 8, 9
foreach (var num in sortedNumbersAsc)
{
    Console.WriteLine(num);
}

// The OrderByDescending method is similar to OrderBy, but sorts the elements in descending order. Like in the previous example, the key is the numbers themselves.
var sortedNumbersDesc = numbers.OrderByDescending(num => num);

// Output: 9, 8, 5, 2, 1
foreach (var num in sortedNumbersDesc)
{
    Console.WriteLine(num);
}
```

#### GroupBy

The `GroupBy` operator groups elements of a sequence based on a specified key.

Code: csharp

```csharp
// Define a class 'Student' with two properties: 'Name' and 'Grade'. The 'get' and 'set' are accessors which control the read-write status of these properties.

class Student
{
    public string Name { get; set; }
    public string Grade { get; set; }
}

// Create a list of students, where each student is an instance of the 'Student' class. Each student has a 'Name' and a 'Grade'.
List<Student> students = new List<Student>
{
    new Student { Name = "John", Grade = "A" },
    new Student { Name = "Alice", Grade = "B" },
    new Student { Name = "Michael", Grade = "A" },
    new Student { Name = "Emily", Grade = "B" }
};

// Using the LINQ GroupBy method, we group the students by their grades. This method returns a collection of `IGrouping<TKey,TElement>` objects, where each `IGrouping` object contains a collection of objects that have the same key.
var studentsByGrade = students.GroupBy(student => student.Grade);

foreach (var group in studentsByGrade)
{
    Console.WriteLine("Students in Grade " + group.Key + ":");
    foreach (var student in group)
    {
        Console.WriteLine(student.Name);
    }
}
// Students in Grade A:
// John
// Michael
// Students in Grade B:
// Alice
// Emily
```

When the `GroupBy` method is called, it groups the elements of the original collection (`students` in this case) based on a specified key. In this case, the key is `student.Grade`, which means the students are grouped by their grades. Each `group` is an `IGrouping<TKey, TElement>` object (where `TKey` is the type of the key and `TElement` is the type of the elements in the group). In this specific case, `TKey` is a `string` (the grade) and `TElement` is a `Student`.

So, in the foreach loop, `group` represents each of these `IGrouping<string, Student>` objects. The `Key` property of each `group` holds the grade (A or B in this example), and iterating over `group` gives you each student in that grade.

#### Join

The `Join` operator combines two sequences based on a common key.

Code: csharp

```csharp
// This is the Student class with properties for Id, Name, and CourseId. The 'get' and 'set' are accessors which control the read-write status of these properties.
class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int CourseId { get; set; }
}

// This is the Course class with properties for Id and Title. The 'get' and 'set' are accessors which control the read-write status of these properties.
class Course
{
    public int Id { get; set; }
    public string Title { get; set; }
}

// Here we create a list of students, where each student is an instance of the 'Student' class. Each student has an 'Id', 'Name', and a 'CourseId'.
List<Student> students = new List<Student>
{
    new Student { Id = 1, Name = "John", CourseId = 101 },
    new Student { Id = 2, Name = "Alice", CourseId = 102 },
    new Student { Id = 3, Name = "Michael", CourseId = 101 },
    new Student { Id = 4, Name = "Emily", CourseId = 103 }
};

// We create a list of courses, where each course is an instance of the 'Course' class. Each course has an 'Id' and a 'Title'.
List<Course> courses = new List<Course>
{
    new Course { Id = 101, Title = "Mathematics" },
    new Course { Id = 102, Title = "Science" },
    new Course { Id = 103, Title = "History" }
};

// Here we perform a join operation between the 'students' and 'courses' lists using LINQ's Join method.
// We match each student with their corresponding course based on the CourseId from the student and the Id from the course.
// The result is a new anonymous object that includes each student's name and the title of their course.
var studentCourseInfo = students.Join(courses,
                                      student => student.CourseId,
                                      course => course.Id,
                                      (student, course) => new
                                      {
                                          student.Name,
                                          course.Title
                                      });

foreach (var info in studentCourseInfo)
{
    Console.WriteLine(info.Name + " - " + info.Title);
}

// John - Mathematics
// Alice - Science
// Michael - Mathematics
// Emily - History
```

#### Aggregate

The `Aggregate` operator applies an accumulator function over a sequence.

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// This line uses the LINQ Aggregate method to generate a single value from the 'numbers' collection.
// The Aggregate method applies a specified function to the first two elements of the collection, then to the result and the next element, and so on. 
// In this case, the function is a lambda expression '(acc, num) => acc + num', where 'acc' represents the accumulated value so far and 'num' represents the current element.
// So essentially, this code sums up all the numbers in the 'numbers' collection. The resulting sum is then stored in the 'sum' variable.
var sum = numbers.Aggregate((acc, num) => acc + num);

// Output: 15
Console.WriteLine(sum);
```

#### Count/Sum/Average/Min/Max

These methods compute a sequence's `count`, `sum`, `average`, `minimum`, or `maximum` value.

```csharp
List<int> numbers = new List<int> { 5, 2, 8, 1, 9 };

// The Count method is a LINQ extension method that returns the number of elements in the 'numbers' collection. The result is stored in the 'count' variable.
int count = numbers.Count();
// The Sum method calculates the sum of all elements in the 'numbers' collection. The resulting sum is stored in the 'sum' variable.
int sum = numbers.Sum();
// The Average method calculates the average value of all elements in the 'numbers' collection. Since an average can be a fractional number, it's stored in a variable of type double.
double average = numbers.Average();
// The Min method finds the smallest number in the 'numbers' collection. The minimum value found is stored in the 'min' variable.
int min = numbers.Min();
// The Max method finds the largest number in the 'numbers' collection. The maximum value found is stored in the 'max' variable.
int max = numbers.Max();

Console.WriteLine("Count: " + count);        // Output: Count: 5
Console.WriteLine("Sum: " + sum);            // Output: Sum: 25
Console.WriteLine("Average: " + average);    // Output: Average: 5
Console.WriteLine("Min: " + min);            // Output: Min: 1
Console.WriteLine("Max: " + max);            // Output: Max: 9
```

This code has a `List<int>` called numbers with five elements. We use various LINQ extension methods (`Count()`, `Sum()`, `Average()`, `Min()`, `Max()`) to perform calculations on the list. The expected output comments indicate the results when printing the count, sum, average, minimum, and maximum values to the console.



## Methods and Exception Handling

***

### Functions

Functions, known as methods in C#, are a significant feature of programming, providing a means to create reusable code. They allow programmers to build modular programs, improving efficiency, readability, and maintainability.

#### Creating a method

In C#, a method declaration specifies the method’s name, return type, and parameters within the class definition. Here's an example of a method declaration for a simple method that multiplies two numbers:

Code: csharp

```csharp
public int Multiply(int a, int b);
```

The method is declared `public`, which means it can be accessed from other classes. `int` signifies the return type, indicating that the method will return an integer value. `Multiply` is the method's name, and within the parentheses `(int a, int b)`, we define the parameters the method will take.

The definition of a method involves providing the body of the method or what the method does. The code block inside the curly brackets `{}` forms the method’s body. Let's define our `Multiply` method:

Code: csharp

```csharp
public int Multiply(int a, int b) 
{
    return a * b;
}
```

The `return` statement specifies the output of the method . In this case, it returns the product of `a` and `b`.

In C#, the terms "declaration" and "definition" of a method aren't typically differentiated, as they are in some languages such as C or C++. This is because C# does not permit separate declaration and definition of methods - when you declare a method, you must also provide its implementation, thus effectively defining it.

#### Method Scope

Scope pertains to the visibility or accessibility of variables within the program. In C#, variables declared inside a method, known as local variables, are not accessible outside that method. For instance:

Code: csharp

```csharp
public int Multiply(int a, int b) 
{
    int result = a * b;
    return result;
}

public void DisplayResult() 
{
    Console.WriteLine(result); // This will lead to an error
}
```

In the `DisplayResult()` method, accessing the `result` variable local to the Multiply method would result in a compile-time error. This is because the `result` is out of scope in `DisplayResult()`.

However, if a variable is declared in a class but outside any method, it is a global variable and can be accessed from any method within that class.

#### Static vs Non-Static Methods

The `static` keyword is used to declare members that `belong to the type` rather than `any instance of the type`. This means that static members are shared across all instances of a type and can be accessed directly using the type name, without creating an instance of the class.

Methods can be declared as `static` or `non-static`, also known as `instance` methods.

Details about `classes` and `instances` will be explored in the `Object-oriented Programming` section, but for now, just note the following.

A `static` method belongs to the class itself rather than any specific class instance. It is declared with the keyword `static`.

Code: csharp

```csharp
public class MyClass
{
    // Static method
    public static void MyStaticMethod()
    {
        Console.WriteLine("This is a static method.");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        // Call the static method
        MyClass.MyStaticMethod();  // Outputs: This is a static method.
    }
}
```

To call a static method, you don't need to create an instance of the class. Instead, you use the class name itself.

Code: csharp

```csharp
MyClass.MyStaticMethod();
```

Since static methods are tied to the class itself, they can only access the class's other static members (methods, properties, etc.). They cannot access non-static members as those belong to specific instances of the class.

A `non-static` (or `instance`) method belongs to a particular class instance. It is declared without using the `static` keyword.

Code: csharp

```csharp
public class MyClass
{
    // Non-static (instance) method
    public void MyInstanceMethod()
    {
        Console.WriteLine("This is an instance method.");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        // Create an instance of MyClass
        MyClass myObject = new MyClass();

        // Call the instance method
        myObject.MyInstanceMethod();  // Outputs: This is an instance method.
    }
}
```

To call a non-static method, you must create an instance of the class.

Code: csharp

```csharp
MyClass myObject = new MyClass();
myObject.MyInstanceMethod();
```

Instance methods can access the class's `static` and `non-static` members since they belong to a specific class instance.

Static members can also include `fields`, `properties`, `events`, `operators`, and `constructors`.

### Exceptions

Exception handling in C# is a robust mechanism used to handle runtime errors so that the normal flow of the application can be maintained. C# provides a structured solution to error handling through try-and-catch blocks. Using these blocks, we can isolate code that may throw an exception and enable the program to respond rather than letting the program crash.

#### try catch finally

A `try` block is used to encapsulate a region of code. If any statement within the try block throws an exception, that exception will be handled by the associated catch block.

Code: csharp

```csharp
try
{
    // Code that could potentially throw an exception.
}
```

The `catch` block is used to catch and handle an exception. It follows a try block or another catch block. Each try block can have multiple catch blocks associated with it, each designed to handle specific or multiple exceptions. A `catch` block without a specified type will catch all exceptions.

Code: csharp

```csharp
catch (Exception ex)
{
    // Handle the exception
}
```

A `finally` block lets you execute code after a try block has been completed, regardless of whether an exception has been thrown. It is optional and cleans up resources inside the try block (like database connections, files, or network resources).

Code: csharp

```csharp
finally
{
    // Code to be executed after the try block has completed,
    // regardless of whether an exception was thrown.
}
```

Here's an example of try, catch, and finally all used together:

Code: csharp

```csharp
try
{
    // Code that could potentially throw an exception.
    int divisor = 0;
    int result = 10 / divisor;
}
catch (DivideByZeroException ex)
{
    // Handle the DivideByZeroException.
    Console.WriteLine("Cannot divide by zero");
}
finally
{
    // Code to be executed after the try block has completed,
    // regardless of whether an exception was thrown.
    Console.WriteLine("This code is always executed.");
}
```

When dealing with `catch blocks`, remember that they can handle multiple exception exceptions. The order in which you specify different catch blocks matters; they're examined top to bottom, so the first one that matches the exception type will be executed. If you have a catch block that handles all exceptions at the top, it will catch all exceptions, and none of the catch blocks below it will execute. This is why the catch block for the most general exception type, `Exception`, is usually last.

Code: csharp

```csharp
try
{
    // Code that could throw an exception
    int[] arr = new int[5];
    arr[10] = 30; // This line throws an IndexOutOfRangeException.
}
catch (IndexOutOfRangeException ex)
{
    // Handle specific exception first
    Console.WriteLine("An IndexOutOfRangeException has been caught: " + ex.Message);
}
catch (Exception ex)
{
    // General exception catch block
    Console.WriteLine("An exception has been caught: " + ex.Message);
}
```

The `finally` block is executed regardless of whether an exception is thrown. If you have any code that must execute, whether an exception is thrown or not, it should be placed in a finally block. For example, if you open a file in a try block, you should close it in a finally block, whether or not an exception is thrown when working with the file.

Code: csharp

```csharp
StreamReader reader = null;
try
{
    reader = new StreamReader("file.txt");
    // Code to read the file.
}
catch (FileNotFoundException ex)
{
    Console.WriteLine(ex.Message);
}
finally
{
    // Whether an exception is thrown or not, close the file.
    if (reader != null)
        reader.Close();
}
```

#### throw

The `throw` keyword can be used to raise exceptions. You can throw a pre-existing exception, or you can instantiate a new exception and throw it.

Code: csharp

```csharp
try
{
    // Throw a new exception.
    throw new Exception("A problem has occurred.");
}
catch (Exception ex)
{
    // Handle the exception.
    Console.WriteLine(ex.Message);
}
```





## Lambda Expressions

***

A lambda expression is a method without a name that calculates and returns a single value. They are simple methods to represent `anonymous methods` (methods without a name) or `functions` inline.

A lambda expression consists of three main parts: a `parameter list`, the `lambda operator` (`=>`), and an `expression or statement`. The general syntax for a lambda expression looks something like this:

Code: csharp

```csharp
(parameters) => expression or statement block
```

* The `parameters` represent the input values to the lambda expression. They can be zero or more, separated by commas. If there is only one parameter, parentheses are optional. For multiple parameters, parentheses are required.
* The `lambda Operator (=>)` separates the parameter list from the body of the expression. It denotes a relationship between the parameters and the code to execute.
* The `expression or statement block` represents the code that is executed when the lambda expression is invoked. For a single expression, the result is implicitly returned. A statement block is enclosed in curly braces `{}` for multiple statements.

Consider the example given in the `LINQ` section.

Code: csharp

```csharp
var evenNumbers = numbers.Where(num => num % 2 == 0); // Output: 2, 4, 6, 8, 10
```

The lambda expression `num => num % 2 == 0` specifies the condition for the `Where` method to filter the numbers. Here, `num` is the input parameter, and the condition to the right of the lambda operator is the statement block. This condition is applied to each element of the numbers list.

In plain English, this lambda expression reads, "For each number (num) in numbers, keep it if the remainder when num is divided by 2 equals 0." The % operator is the modulus operator, which gives the remainder of a division operation. Therefore, `num % 2 == 0` checks if a number is evenly divisible by 2, i.e., it's an even number.

### Simple Lambda Expression

Consider the following method.

Code: csharp

```csharp
void Greet()
{
    Console.WriteLine("Hello, world!");
}

// Invoke the method
Greet(); // Output: Hello, world!
```

In this example, we merely define a method that prints a message to the console when invoked. However, we can further simplify this code using a lambda function, which essentially condenses it into a single line.

Code: csharp

```csharp
// Lambda expression without parameters
var greet = () => Console.WriteLine("Hello, world!");
greet(); // Output: Hello, world!
```

In this instance, we've defined a lambda expression without any parameters. The lambda expression assigns a function to the variable `greet`, which prints "Hello, world!" to the console upon invocation.

While both achieve the same outcome, the lambda expression is far more succinct and can be employed as an inline function where required, contrasted with the method definition that necessitates a separate declaration.

### Lambda Expression with Parameters

A `Lambda Expression with Parameters` is a type of lambda expression in C# that takes one or more input parameters. This type of lambda expression is typically used when you want to perform an operation or evaluate a condition using the input parameters.

Code: csharp

```csharp
// Regular method
int Add(int a, int b)
{
    return a + b;
}

// Lambda expression with parameters
var add = (int a, int b) => a + b;
int result = add(5, 3);
Console.WriteLine(result); // Output: 8
```

Here, we define a lambda expression with two parameters `a` and `b`, which adds the values of `a` and `b`. The lambda expression is assigned to the variable `add`, and we invoke it with arguments `5` and `3`, resulting in the sum `8` being assigned to the variable `result`.

### Lambda Expression with Statement Block

A `Lambda Expression with a Statement Block`, often called a `Statement Lambda`, is a type of lambda expression in C# that contains a block of code instead of a single expression on the right side of the lambda operator (`=>`).

Code: csharp

```csharp
// Regular method
bool IsEven(int number)
{
    if (number % 2 == 0)
        return true;
    else
        return false;
}

// Lambda expression with statement block
var isEven = (int number) =>
{
    if (number % 2 == 0)
        return true;
    else
        return false;
};

bool even = isEven(6);
Console.WriteLine(even); // Output: True
```

In this example, we define a lambda expression with a parameter `number` and a statement block enclosed in curly braces. The lambda expression checks if the `number` is even and returns `true` or `false` accordingly. We assign the result of invoking the lambda expression with `6` to the variable `even`, which evaluates to `true`.



## Libraries

***

C# includes many predefined functions and libraries that developers can use to accomplish various tasks more easily and efficiently. The .NET Framework provides these libraries and includes functionalities for things like file I/O, database access, networking, and much more.

A library in C# is typically provided as a `.dll` (Dynamic Link Library) file. To use the library's functions and classes, you must first reference it in your project. This will be done automatically if the library is installed via a package manager like nuget, or if you use a library from within the .NET ecosystem.

The `using` directive then tells the compiler to use a specific namespace in the library. A `namespace` groups related class, structures, and other types under a single name. For instance, the `System` namespace includes fundamental classes and base types that are used in C# programming.

For example, to use the `File` class from the `System.IO` namespace for handling files, you would first need to add `using System.IO;` at the top of your code.

Code: csharp

```csharp
using System.IO;

class Program
{
    static void Main(string[] args)
    {
        // Check if a file exists
        if (File.Exists("test.txt"))
        {
            // Read the content of the file
            string content = File.ReadAllText("test.txt");
            Console.WriteLine(content);
        }
        else
        {
            Console.WriteLine("The file does not exist.");
        }
    }
}
```

In this example, `File.Exists` is a predefined function from the `System.IO` namespace that checks if a file exists at the provided path and `File.ReadAllText` is another predefined function that reads the entire content of the file as a string. Because `System` is a core library, the compiler will automatically include it.

Similarly, you can use predefined functions from other namespaces and libraries—for instance, the `System.Math` namespace contains mathematical functions such as `Math.Sqrt` for computing the square root of a number, `Math.Pow` for raising a number to a specified power, and `Math.Round` for rounding a number to the nearest integer.

Code: csharp

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        double num = 9.0;
        double squareRoot = Math.Sqrt(num);
        Console.WriteLine($"The square root of {num} is {squareRoot}");

        double baseNum = 2.0;
        double exponent = 3.0;
        double power = Math.Pow(baseNum, exponent);
        Console.WriteLine($"{baseNum} raised to the power of {exponent} is {power}");

        double toBeRounded = 9.5;
        double rounded = Math.Round(toBeRounded);
        Console.WriteLine($"{toBeRounded} rounded to the nearest integer is {rounded}");
    }
}
```

As you can see, leveraging the predefined functions and libraries provided by the .NET Framework can achieve complex functionality with less code.

### NuGet

In addition to the standard libraries, C# offers extensive support for using third-party libraries and packages. These can be added to your project through various means, including the [NuGet package manager](https://www.nuget.org/). `NuGet` is a free and open-source package manager designed for the Microsoft development platform, and it hosts thousands of libraries.

Adding a `NuGet` package to your project can be as easy as right-clicking on your project in the Solution Explorer in Visual Studio, selecting "`Manage NuGet Packages...`" and then searching for and installing the required package. If using a code editor, we use the `dotnet package add` command, but [Microsoft provides great documentation for using nuget from the CLI](https://learn.microsoft.com/en-za/nuget/consume-packages/install-use-packages-dotnet-cli).

Once a package is installed, you can utilise its functionality in your code by adding the appropriate `using` directive at the top of your file. The `Newtonsoft.Json` package, for instance, provides powerful tools for working with JSON data.

Code: csharp

```csharp
using Newtonsoft.Json;
using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        string json = "[{'Name':'John', 'Age':30}, {'Name':'Jane', 'Age':28}]";

        List<Person> people = JsonConvert.DeserializeObject<List<Person>>(json);

        foreach (var person in people)
        {
            Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
        }
    }
}

public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

In this example, the `JsonConvert.DeserializeObject<T>` method is used to parse the JSON string into a list of `Person` objects. This predefined function, part of the `Newtonsoft.Json` library, dramatically simplifies the task of JSON parsing.

### Manual Referencing

It is also possible to manually link a library to the project. If you use an IDE such as Visual Studio, or Jetbrains Rider, it's as simple as right-clicking on the `Project Dependencies` section under the solution explorer and selecting the `Add Project Reference...` option, and then finding the library you want to link.

Alternatively, if you are using a Code editor, such as VSCode, you will need to manually edit the project file to include the references, such as the example below, which is going to reference every `.dll` file in the libs subfolder:

Code: xml

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net7.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
    <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
  </PropertyGroup>
  <ItemGroup>
    <!-- references look like this -->
    <Reference Include="libs\*.dll" /> 
  </ItemGroup>

</Project>
```

It's also possible to hardcode paths and establish multiple `Reference` definitions for each individualreference specifically.

To identify the `namespaces`, `types`, `classes`, and `methods` provided by the library, it is generally considered best practice to consult the provided documentation. Both Visual Studio and Visual Studio Code will provide code auto-complete functionality for the functionality from imported libraries through their IntelliSense auto-complete tool.

While the .NET Framework and third-party libraries offer a wide array of predefined functions, it's essential to understand their usage and potential impact on your application. Some libraries may have licensing restrictions, or they may not be maintained actively. Always research before including a third-party library in your project.



## Object-Oriented Programming

***

Object-Oriented Programming (OOP) is a programming paradigm that relies on the concept of "objects". Objects are instances of classes, which can contain data in the form of fields, often known as attributes, and code, in the form of methods. In OOP, computer programs are designed by making them out of objects that interact with one another.

There are four main principles of Object-Oriented Programming:

1. `Encapsulation` is the practice of keeping fields within a class private and providing access to them via public methods. It's a protective barrier that keeps the data and implementation code bundled together within an object.
2. `Inheritance` is a process by which one class can acquire the properties (methods and fields) of another. With the use of inheritance, information is made manageable in a hierarchical order.
3. `Polymorphism` enables methods to be used as if they were the methods of a class's parent. It's the characteristic of an operation to behave differently based on the types of objects or arguments involved.
4. `Abstraction` represents essential features without including background details or explanations. It provides a simple interface and reduces complexity by hiding unnecessary details.

### Classes & Structs

In C#, a `class` is a blueprint for creating objects, and an object is an instance of a class. Class definitions start with the keyword `class` followed by the name of the class and typically encapsulate data and methods that operate on that data.

Classes are made up of two fundamental elements: `Properties` and `Methods`.

* `Properties` represent data about the class. They are often referred to as attributes or characteristics. For example, in a `Car` class, properties might include `Color`, `Model`, and `Year`.
* `Methods` represent actions or behaviour associated with the class. They are functions defined within a class. For instance, a `Car` class may have methods like `Drive()`, `Park()`, and `Brake()`.

Code: csharp

```csharp
class Car
{
    // Properties
    public string Color;
    public int Year;

    // Method
    public void Drive()
    {
        Console.WriteLine($"The {Color} car from {Year} is driving.");
    }
}
```

In the above example, `Car` is a class that contains two properties (`Color` and `Year`) and one method (`Drive`).

To create an object in C#, you use the `new` keyword followed by the class name. This process is often called `instantiation` because you create an "instance" of a class.

Code: csharp

```csharp
Car myCar = new Car();
```

In this line, `myCar` is an object of the `Car` class. You can now use the dot operator `.` to access its properties and methods:

Code: csharp

```csharp
myCar.Color = "Red";
myCar.Year = 2020;
myCar.Drive();
// output: The Red car from 2020 is driving.
```

Remember that each object has its own copy of properties. Thus, if you create another `Car` object, it will have its own `Color` and `Year`:

Code: csharp

```csharp
Car anotherCar = new Car();
anotherCar.Color = "Blue";
anotherCar.Year = 2021;
//output: The Blue car from 2021 is driving.
```

So even though `myCar` and `anotherCar` are both instances of the `Car` class, they have different property values. This allows objects to have unique states while sharing common behaviour from their respective classes.

Classes can also have a `constructor`, which is a special method in a class or struct that is automatically called when an object of that class or struct is created. The primary purpose of a constructor is to initialise the object and its data members.

The constructor has the same name as the class or struct, and it doesn't have any return type, not even void. It can take parameters if needed.

Code: csharp

```csharp
class Car
{
    // Properties
    public string Color;
    public int Year;
    
    // Constructor
    public Car(string c, int y)
    {
        Color = c;
        Year = y;
    }

    // Method
    public void Drive()
    {
        Console.WriteLine($"The {Color} car from {Year} is driving.");
    }
}
```

You can then pass the parameters when the object is instantiated to set the variables.

Code: csharp

```csharp
Car myNewCar = new Car("Pink", 2022);
myNewCar.Drive();
// output: The Pink car from 2022 is driving.
```

#### Accessors

An `accessor` is a class member function that provides access to the value of private or protected data members. There are two types of accessors - `get` and `set`.

The `get` accessor is used to return the property value. It provides read-only access to the attribute it is assigned to. If only a `get` accessor is specified, the property becomes read-only.

Code: csharp

```csharp
class Circle
{
    private double radius;

    public double Radius
    {
        get
        {
            return radius;
        }
    }
}
```

In this example, the `Radius` property has only a `get` accessor, making it read-only. Trying to set its value will result in a compile-time error.

The `set` accessor is used to set the property `value`. It provides write-only access to the attribute it is assigned to. If only a `set` accessor is specified, the property becomes write-only.

Code: csharp

```csharp
class Circle
{
    private double radius;

    public double Radius
    {
        set
        {
            if (value > 0)
                radius = value;
            else
                Console.WriteLine("Radius cannot be negative or zero");
        }
    }
}
```

In this example, the `Radius` property has only a `set` accessor. Its value can be set but not directly retrieved. The `value` keyword in C# is a special keyword that is used in the `set` accessor of a property or indexer. It represents the new value the code attempts to assign to the property.

Most commonly, you'll see both `get` and `set` accessors used together. This allows for both reading and writing the property value.

Code: csharp

```csharp
class Circle
{
    private double radius;

    public double Radius
    {
        get
        {
            return radius;
        }
        set
        {
            if (value > 0)
                radius = value;
            else
                Console.WriteLine("Radius cannot be negative or zero");
        }
    }
}
```

#### Automatic Properties

In C#, an automatic property, also known as auto-implemented property, allows you to define a class property in a concise way without explicitly declaring a backing field. A backing field is a private variable used to store a property’s data.

For example, consider a `full property` with a declared backing field:

Code: csharp

```csharp
class Circle
{
    private double radius;

    public double Radius
    {
        get
        {
            return radius;
        }
        set
        {
            radius = value;
        }
    }
}
```

Whereas an automatic property will automatically declare the backing field:

Code: csharp

```csharp
class Circle
{
    public double Radius { get; set; }
}
```

In this example, `Radius` is an automatic property. The `{ get; set; }` syntax tells C# to generate a hidden backing field behind the scenes automatically. This field stores the actual data, and the `get` and `set` accessors are used to read from and write to this field.

Functionally both properties are identical.

Code: csharp

```csharp
Circle c = new Circle();
c.Radius = 12345.54321;

Console.WriteLine(c.Radius);  // Outputs: 12345.54321
```

Automatic properties provide a shorter and more readable way to create properties, helping keep your code clean and efficient.

#### Structs

A `struct`, short for structure, is a value type in C#. This means when a `struct` is created, the variable to which the struct is assigned holds the struct's actual data. This contrasts with reference types, where the variable references the object's data, not the actual data itself.

Structs are useful for small data structures that have value semantics. They can contain fields, methods, and constructors just like classes, but there are some differences:

* Structs do not support inheritance, while classes do. However, both structs and classes can implement interfaces.
* Structs are instantiated without using the `new` keyword, and their constructors are called automatically.
* A struct cannot be `null`, as it's a value type. A class can be `null` because it's a reference type.

Code: csharp

```csharp
public struct Point
{
    public int X { get; set; }
    public int Y { get; set; }

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }
}
```

In this example, `Point` is a struct that represents a point in two-dimensional space. It includes two properties (`X` and `Y`) and a constructor that initialises those properties.

### Encapsulation

Encapsulation is one of the four fundamental principles of Object-Oriented Programming (OOP). It is often described as the bundling of data and the methods that operate on that data into a single unit known as a class. It serves as a protective shield that prevents the data from being accessed directly by outside code, hence enforcing data integrity and ensuring security.

In C#, data encapsulation is achieved through access modifiers, which control the visibility and accessibility of classes, methods, and other members. The key access modifiers are `public`, `private`, `protected`, and `internal`.

* A `public` member is accessible from any code in the program.
* A `private` member is only accessible within its own class. This is the most restrictive level of access.
* A `protected` member is accessible within its own class and by derived class instances.
* An `internal` member is accessible only within files in the same assembly.

The convention in C# is to make data members `private` to hide them from other classes (this is known as data hiding). Then, `public` methods known as getters and setters (or, more commonly, properties) are provided to get and set the values of the private fields. These methods serve as the interface to the outside world and protect the data from incorrect or inappropriate manipulation.

Code: csharp

```csharp
public class Employee
{
    // Private member data (fields)
    private string name;
    private int age;

    // Public getter and setter methods (properties)
    public string Name
    {
        get { return name; }
        set { name = value; }
    }

    public int Age
    {
        get { return age; }
        set 
        { 
            if(value > 0)
                age = value; 
            else 
                Console.WriteLine("Invalid age value");
        }
    }
}
```

In this example, the `Employee` class encapsulates the `name` and `age` fields. These fields are `private`, so they cannot be accessed directly from outside the `Employee` class. Instead, access is provided through the `public` properties `Name` and `Age`, which serve as the interface to the `Employee` class. Notice that the `Age` setter includes validation logic to ensure an invalid age cannot be set. This is an excellent example of encapsulation protecting the data in an object. The data (in this case, the `age`) is safeguarded and encapsulated within the `Employee` class.

### Inheritance

Inheritance is a fundamental principle of Object-Oriented Programming (OOP) that allows for the creation of hierarchical classifications of objects. It offers a mechanism where a new class can inherit members (fields, methods, etc.) of an existing class, thereby promoting code reusability and logical classification.

There are two types of inheritance: single inheritance and multilevel inheritance.

#### Single Inheritance

In single inheritance, a class (aka a derived or child class) inherits from a single-parent class (also known as a base or superclass). This allows the derived class to reuse (or inherit) the fields and methods of the base class, as well as to introduce new ones.

Consider an example where we have a base class, `Vehicle`, and a derived class, `Car`.

Code: csharp

```csharp
public class Vehicle {
    public string color;
    
    public void Start() {
        Console.WriteLine("Vehicle started");
    }
}

public class Car : Vehicle {
    public string model;
    
    public void Drive() {
        Console.WriteLine("Driving car");
    }
}
```

`Car` is a derived class that inherits from the `Vehicle` base class. It inherits the `color` field and the `Start()` method from `Vehicle` and also defines an additional field `model` and a method `Drive()`.

#### Multilevel Inheritance

Multilevel inheritance is a scenario where a derived class inherits from another. This creates a "chain" of inheritance where a class can inherit members from multiple levels up its inheritance hierarchy.

Let's extend the previous example to include a `SportsCar` class inherited from `Car`.

Code: csharp

```csharp
public class SportsCar : Car {
    public int topSpeed;
    
    public void TurboBoost() {
        Console.WriteLine("Turbo boost activated");
    }
}
```

In this case, `SportsCar` is a derived class that inherits from the `Car` class, which in turn inherits from the `Vehicle` class. This means that `SportsCar` has access to the `color` field and `Start()` method from `Vehicle`, the `model` field and `Drive()` method from `Car`, and also defines its own field `topSpeed` and method `TurboBoost()`.

Remember that C# doesn't support multiple inheritance, meaning a class cannot directly inherit from more than one class at the same level. However, as we've seen here, it supports multiple levels of inheritance and allows a class to implement multiple interfaces.

#### base

In C#, the `base` keyword is used to access base class members from within a derived class. This can include methods, properties, and fields of the base class. Furthermore, the `base` keyword is most commonly employed within the derived class's constructor to call the base class’s constructor.

To delve deeper, let's examine the use of the `base` keyword in a few examples. Consider a base-class `Vehicle` and a derived-class `Car`.

Code: csharp

```csharp
public class Vehicle
{
    public string Color { get; }

    public Vehicle(string color)
    {
        this.Color = color;
    }

    public void DisplayColor()
    {
        Console.WriteLine($"Color: {this.Color}");
    }
}

public class Car : Vehicle
{
    public string Brand { get; }

    public Car(string color, string brand) : base(color)
    {
        this.Brand = brand;
    }

    public void DisplayCarInformation()
    {
        base.DisplayColor();
        Console.WriteLine($"Brand: {this.Brand}");
    }
}
```

In the derived class `Car`, the `base` keyword is used in two distinct ways:

1. `Constructor`: Within the constructor of `Car`, `base(color)` is used to call the constructor of the base class `Vehicle`. Here, `base` allows `Car` to initialise the `Color` property defined in `Vehicle`.
2. `Methods`: Within the `DisplayCarInformation` method of `Car`, `base.DisplayColor()` is used to call the `DisplayColor` method from the base class `Vehicle`.

The `base` keyword hence provides an effective way to interact with the base class and utilise its members, enabling the principles of reuse and abstraction that are foundational to object-oriented programming. This leads to more manageable, scalable, and organised code.



## Polymorphism and Abstraction

***

### Polymorphism

Polymorphism is one of the four fundamental principles of Object-Oriented Programming (OOP), alongside Encapsulation, Inheritance, and Abstraction. The term originates from the Greek words "poly," meaning many, and "morph," meaning forms. Thus, polymorphism is the ability of an entity to take on many forms.

In C#, polymorphism is generally realised through method overloading and overriding.

#### Method Overloading

Method overloading, also known as static or compile-time polymorphism, is a technique that allows multiple methods with the same name but different parameters (in terms of number, type, or order) to coexist within a class.

Code: csharp

```csharp
public class Mathematics
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }
}
```

In the above class `Mathematics`, the method `Add` is overloaded: one version of the `Add` method accepts two integers, while the other accepts two doubles. The correct version of the method is selected at compile time-based on the arguments supplied.

#### Method Overriding

Method overriding, on the other hand, is a form of dynamic or run-time polymorphism. It allows a derived class to provide a different implementation for a method already defined in its base class or one of its base classes. The method in the base class must be marked with the `virtual` keyword, and the method in the derived class must use the `override` keyword.

Code: csharp

```csharp
public class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("The animal makes a sound");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("The dog barks");
    }
}
```

In the above example, the `Dog` class overrides the `MakeSound` method of the `Animal` class. When `MakeSound` is called on an object of type `Dog`, the overridden version in the `Dog` class is executed.

The concepts of overloading and overriding extend to operators and properties, adding flexibility and expressiveness to C# programming.

#### Operator Overloading

Just like methods, C# allows operators to be overloaded. This enables custom types to be manipulated using standard operators, enhancing code readability and intuitiveness. For example, for a `Vector` class representing a mathematical vector, you might overload the '+' operator to perform vector addition:

Code: csharp

```csharp
public class Vector
{
    public double X { get; set; }
    public double Y { get; set; }

    public Vector(double x, double y)
    {
        X = x;
        Y = y;
    }

    public static Vector operator +(Vector v1, Vector v2)
    {
        return new Vector(v1.X + v2.X, v1.Y + v2.Y);
    }
}
```

In this example, instances of `Vector` can be added using the `+` operator, just like primitive types:

Code: csharp

```csharp
Vector v1 = new Vector(1, 2);
Vector v2 = new Vector(3, 4);
Vector sum = v1 + v2;  // { X = 4, Y = 6 }
```

#### Property Overriding

In C#, properties, like methods, can be overridden in derived classes. A base class declares a virtual property, and derived classes can override this property to change its behaviour.

Code: csharp

```csharp
public class Animal
{
    public virtual string Name { get; set; }

    public Animal(string name)
    {
        Name = name;
    }
}

public class Dog : Animal
{
    public Dog(string name) : base(name) { }

    public override string Name
    {
        get { return base.Name; }
        set { base.Name = value + " the dog"; }
    }
}
```

In this case, a `Dog` object modifies the behaviour of the `Name` property to append " the dog" to any name assigned to it:

Code: csharp

```csharp
Dog myDog = new Dog("Rex");
Console.WriteLine(myDog.Name);  // "Rex the dog"
```

These examples underline the power of polymorphism in C# and object-oriented programming. It allows classes to provide tailored implementations of methods, operators, and properties, enabling more natural, expressive, and aligned code with the problem domain.

### Abstraction

In object-oriented programming, abstraction is the concept of simplifying complex reality by modelling classes appropriate to the problem and working at the most appropriate level of inheritance for a given aspect of the problem. It is a mechanism that represents the essential features without including the background details.

Abstraction in C# is achieved by using `abstract` classes and `interfaces`. An `abstract` class is a class that cannot be instantiated and is typically used as a base class for other classes. `Abstract` classes can have `abstract` methods which are declared in the `abstract` class and implemented in the derived classes.

Code: csharp

```csharp
public abstract class Animal
{
    public abstract void Speak();
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("The dog barks");
    }
}

public class Cat : Animal
{
    public override void Speak()
    {
        Console.WriteLine("The cat meows");
    }
}
```

In this example, `Animal` is an abstract class with an abstract method `Speak`. `Dog` and `Cat` classes are derived from `Animal` and provide their own implementation of `Speak`. When `Speak` is called on an object of type `Animal`, the appropriate version of `Speak` is invoked depending on the actual type of the object.

Abstraction using `Interfaces` is another way to achieve abstraction. An `interface` is like an `abstract` class with no implementation. It only declares the methods and properties but doesn't contain any code. A class that implements an interface must provide an implementation for all the interface methods.

Code: csharp

```csharp
public interface IAnimal
{
    void Speak();
}

public class Dog : IAnimal
{
    public void Speak()
    {
        Console.WriteLine("The dog barks");
    }
}

public class Cat : IAnimal
{
    public void Speak()
    {
        Console.WriteLine("The cat meows");
    }
}
```

In this example, `IAnimal` is an interface with a method `Speak`. The classes `Dog` and `Cat` both implement `IAnimal` and provide their own implementation of `Speak`.

In both examples, the user does not need to understand how each animal speaks; they only need to know that all animals can speak. This is the essence of abstraction. It allows you to focus on what the object does instead of how it does it.

Abstraction has several benefits in software development:

1. `Complexity Management`: It simplifies the complexity of designing and maintaining large codebases. By creating abstract classes or interfaces, developers can develop methods and variables that apply to a broad range of related classes. It's easier to manage and understand a few abstract concepts than a larger number of detailed ones.
2. `Reusability`: The use of abstraction promotes the reuse of code. Abstract classes and interfaces often create a template for future classes. Implementing these templates ensures consistent method use across classes and can reduce the amount of code that needs to be written.
3. `Security`: Using abstraction, certain details of an object's implementation can be hidden from the user. This can prevent unauthorised or inappropriate use of an object's methods or variables.
4. `Flexibility`: Abstraction provides a level of flexibility in the development process. As long as the interface between objects remains consistent, changes to the internal workings of an object do not affect the rest of the application. This allows for more freedom in future development and refactoring efforts.

In addition to abstract classes and interfaces, encapsulation is another way to achieve abstraction in C#. Encapsulation refers to bundling data and the methods of operating it into a single unit. This is typically accomplished by defining a class. The data is stored in private fields, and accessed through public methods, protecting the data from being altered in unexpected ways.

For example, consider a `BankAccount` class:

Code: csharp

```csharp
public class BankAccount
{
    private double balance;

    public void Deposit(double amount)
    {
        if (amount > 0)
        {
            balance += amount;
        }
    }

    public void Withdraw(double amount)
    {
        if (amount > 0 && balance >= amount)
        {
            balance -= amount;
        }
    }

    public double GetBalance()
    {
        return balance;
    }
}
```

In this example, the `balance` field is private, meaning it cannot be accessed directly from outside the class. Instead, it is accessed through the `Deposit`, `Withdraw`, and `GetBalance` methods, which ensure the balance cannot be set to an invalid state. This is an example of encapsulation providing abstraction, as users of the `BankAccount` class do not need to know how the balance is stored or how the methods are implemented; they only need to know what methods are available to use.



## Generics in C\#

***

Generics are a feature in C# that let you write type-safe and performant code that works with any data type. Without generics, developers often have to write separate versions of algorithms for different data types or resort to less type-safe options like casting to and from objects.

A type is a description of a set of data that specifies the kind of data that can be stored, the operations that can be performed on that data, and how the data is stored in memory. In C#, types are used extensively to ensure that code behaves as expected, i.e., a `string` can't be directly assigned to an `int` variable.

Generics extend this idea of types to type parameters. A generic type is a class, struct, interface, delegate, or method with a placeholder for one or more types it operates on. The actual types used by a generic type are specified when you create an instance of the type.

#### Benefits of Generics

1. `Type safety`: Generics enforce compile-time type checking. They can carry out strongly typed methods, classes, interfaces, and delegates. With generics, you can create type-safe collection classes at compile time.
2. `Performance`: With generics, performance is improved as boxing and unboxing are eliminated. For value types, this can represent a significant performance boost.
3. `Code reusability`: Generics promote reusability. You can create a generic class that can be used with any data type.

### Generic Classes

A generic class declaration looks much like a non-generic class declaration, except that a type parameter list inside angle brackets follows the class name. The type parameters can then be used in the body of the class as placeholders for the types specified when the class is instantiated.

Code: csharp

```csharp
public class GenericList<T>
{
    private T[] elements;
    private int count = 0;

    public GenericList(int size)
    {
        elements = new T[size];
    }

    public void Add(T value)
    {
        elements[count] = value;
        count++;
    }

    public T GetElement(int index)
    {
        return elements[index];
    }
}
```

In the above example, `T` is the type parameter. This `GenericList` class can be instantiated with any type.

Code: csharp

```csharp
var list1 = new GenericList<int>(10);
var list2 = new GenericList<string>(5);
```

### Generic Methods

Generic methods are methods that are declared with type parameters. Like generic classes, you can create a method that defers the specification of one or more types until the method is called.

Code: csharp

```csharp
public class Utilities
{
    public T Max<T>(T a, T b) where T : IComparable
    {
        return a.CompareTo(b) > 0 ? a : b;
    }
}
```

In the `Max` method above, `T` represents any type that implements `IComparable`. This method can now be used with any comparable types, like integers, floats, strings, etc.

Code: csharp

```csharp
var utility = new Utilities();
int max = utility.Max<int>(3, 4); // returns 4
```

### Generic Constraints

You may want to restrict the types allowed as type arguments when designing generic classes or methods. For example, you might want to ensure that your generic method only operates on value types or classes, types that implement a particular interface, or types with a default constructor. This is done using generic constraints, which you can specify with the `where` keyword.

Code: csharp

```csharp
public class Utilities<T> where T : IComparable, new()
{
    public T Max(T a, T b)
    {
        return a.CompareTo(b) > 0 ? a : b;
    }

    public T Init()
    {
        return new T();
    }
}
```

In the above example, the `Utilities` class has two constraints: `T` must implement `IComparable` and `T` must have a default constructor. Now, `Utilities` can be used with any type that satisfies these constraints.

Code: csharp

```csharp
var utility = new Utilities<int>();
int max = utility.Max(3, 4); // returns 4
int zero = utility.Init(); // returns 0
```



## Asynchronous Programming

`Asynchronous programming` is a powerful technique in modern software development that allows programs to `perform non-blocking operations` and efficiently utilise system resources. It enables applications to `handle time-consuming tasks without blocking the main execution thread`, improving responsiveness and scalability.

In traditional `synchronous programming`, when a method is invoked, the `program waits until the method completes` its execution before proceeding to the following line of code. This blocking behaviour can lead to poor performance and unresponsive applications, especially when dealing with I/O-bound or long-running operations. You can see this behaviour in applications when they appear to `freeze randomly` and `become unresponsive` when you try to load a large file, for instance. `Asynchronous programming` addresses this issue by `allowing tasks to execute independently` without blocking the main thread, enabling other `work to be done concurrently`.

To understand this concept better, it's important to distinguish between `concurrent` and `parallel` operations. `Concurrent` operations refer to tasks that `appear to occur simultaneously` but may not necessarily do so. On the other hand, `parallel` operations involve tasks that are `executed at the same time` on different cores or processors. Asynchronous programming primarily deals with `concurrent operations`, enabling multiple tasks to `progress independently of each other`.

Asynchronous methods return a `Task` or `Task<T>` object representing an ongoing operation. The calling code can continue its execution while the asynchronous operation progresses in the background. Once the operation completes, the result can be retrieved or further processed.

There are a few very important things to be aware of when utilising asynchronous programming:

* `Avoid Blocking Calls`: Use asynchronous versions of methods whenever possible to prevent blocking the main thread.
* `Configure async Methods Properly`: Ensure that `async` methods return `Task` or `Task<T>` and use the `await` keyword appropriately to await the completion of asynchronous operations.
* `Handle Exceptions`: Handle exceptions properly in asynchronous code. Use `try-catch` blocks to catch and handle exceptions that may occur during asynchronous operations. Unhandled exceptions can lead to unexpected application behaviour.
* `Use Cancellation Tokens`: Utilize cancellation tokens to allow the cancellation of asynchronous operations gracefully. This can improve the responsiveness and user experience of the application.

### async & await

In C#, asynchronous programming is facilitated by the `async` and `await` keywords.

The `async` keyword is used to specify that a method, lambda expression, or anonymous method is asynchronous. These methods usually return a `Task` or `Task<T>` object, representing ongoing work.

On the other hand, the `await` keyword is used in an `async` method to suspend the execution of the method until a particular task completes; the program is `awaiting Task<T>` completion. `await` can only be used in an `async` method.

The basic structure of an asynchronous method using `async` and `await` would look like this:

Code: csharp

```csharp
async Task<T> MethodName()
{
    //...Method body
    await SomeTask;
    //...Continue after SomeTask finishes
}
```

* `async`: This keyword is used to specify that a method is asynchronous.
* `Task<T>`: An asynchronous method should return a `Task` or `Task<T>`. A `Task` represents an ongoing job that might not have been completed when your method returns. The job is executed concurrently with the rest of your program.
* `MethodName`: This is where you put the name of your method.
* Inside the method body, you use the `await` keyword before a task to specify that the method can't continue until the awaited task completes—meanwhile, control returns to the caller of the method.

Code: csharp

```csharp
public async Task<int> CalculateSumAsync(int a, int b)
{
    await Task.Delay(500); //Simulate some delay
    return a + b;
}

public async void CallCalculateSumAsync()
{
    int result = await CalculateSumAsync(5, 6);
    Console.WriteLine($"The sum is {result}");
}
```

In this example, the method `CalculateSumAsync` is marked with the `async` keyword and returns a `Task<int>`. Inside the method, we simulate a delay with `Task.Delay`, which we `await`. This means that while we're waiting for the delay to finish, control can be given back to the caller of this method. After the delay is finished, we calculate the sum and return it. In `CallCalculateSumAsync`, we call our asynchronous method and immediately `await` its result. Once we have the result, we print it to the console.

Let's consider an example where we call a web service to fetch data. Fetching data from a web service can be time-consuming, so we will use `async` and `await` to ensure our application remains responsive during this operation.

Code: csharp

```csharp
using System.Net.Http; // Network I/O is explained in more detail on the related page
using System.Threading.Tasks;

class Program
{
    static readonly HttpClient client = new HttpClient();

    static async Task Main()
    {
        string responseBody = await GetWebsiteContentAsync("http://example.com");

        Console.WriteLine(responseBody);
    }

    static async Task<string> GetWebsiteContentAsync(string url)
    {
        HttpResponseMessage response = await client.GetAsync(url);
        response.EnsureSuccessStatusCode();
        string responseBody = await response.Content.ReadAsStringAsync();

        return responseBody;
    }
}
```

The `GetWebsiteContentAsync` method is responsible for fetching the content of a website. It uses an `HttpClient` to send an asynchronous GET request to the provided URL. The `await` keyword waits for the task to complete without blocking the rest of the code.

The `client.GetAsync` method returns a `Task<HttpResponseMessage>` representing the ongoing fetch operation. This task is awaited using the `await` keyword. After ensuring that the HTTP response status indicates success by calling the `EnsureSuccessStatusCode()` method, we read the content of the HTTP response message asynchronously using `response.Content.ReadAsStringAsync()`. This method returns a `Task<string>,` which is also awaited.

Finally, in our `Main` method, we call `GetWebsiteContentAsync` and await its result before writing it to the console.

### Tasks

A Task can be in one of three states: `created`, `running`, or `completed`. Once a Task is completed, it can either result in a value, an exception, or nothing at all.

There are two types of tasks: `Task` and `Task<T>`.

* A `Task` represents a single operation that does not return a value and usually executes asynchronously. After the operation is completed, the Task is marked as completed. This is essentially a `void` async method.
* `Task<T>` represents an asynchronous operation that returns a value. The value type (denoted by `T`) is known and can be retrieved once the Task has finished execution.

Creating tasks can be done using the `Task.Run` method or implement methods marked with the `async` keyword that return a `Task` or `Task<T>`. Here's an example of creating and running a task:

Code: csharp

```csharp
Task<int> task = Task.Run(() => {
    // Simulate work.
    Thread.Sleep(1000);
    return 69;
});
```

In this example, we create a task that sleeps for one second to simulate work and then returns the integer 69.

### Task Cancellation

If necessary, tasks can also be cancelled through the use of cancellation tokens.

Code: csharp

```csharp
CancellationTokenSource cts = new CancellationTokenSource();
Task<int> task = Task.Run(() => {
    // Simulate work.
    Thread.Sleep(1000);
    cts.Token.ThrowIfCancellationRequested();
    return 42;
}, cts.Token);

// Cancel the task.
cts.Cancel();
```

`CancellationToken` is a struct that can be checked periodically by an operation, and if cancellation is requested, the operation can stop itself in a controlled manner.

Cancellation is signalled via the `CancellationTokenSource`. When you want to cancel one or more operations, you call `Cancel` on the `CancellationTokenSource`, which sends a signal to all linked `CancellationToken` instances.

Code: csharp

```csharp
public async Task PerformOperationAsync(CancellationToken cancellationToken)
{
    for (int i = 0; i < 100; i++)
    {
        // Simulate some work.
        await Task.Delay(100);

        // Check for cancellation.
        cancellationToken.ThrowIfCancellationRequested();
    }
}

public async Task MainAsync()
{
    var cts = new CancellationTokenSource();

    var task = PerformOperationAsync(cts.Token);

    // After 500 ms, cancel the operation.
    await Task.Delay(500);
    cts.Cancel();

    try
    {
        await task;
    }
    catch (OperationCanceledException)
    {
        Console.WriteLine("Operation was cancelled.");
    }
}
```

In this example, we pass a `CancellationToken` to the `PerformOperationAsync` method. Inside the method, after each unit of work (simulated with `Task.Delay`), we check if cancellation has been requested using `cancellationToken.ThrowIfCancellationRequested()`. This method throws an `OperationCanceledException` if a cancellation has been requested.

In the `MainAsync` method, we start the operation and cancel it after 500 ms by calling `cts.Cancel()`. This sends a signal to the associated cancellation token. When we await the task, it throws an `OperationCanceledException`, which we catch and handle.

### Exception Handling with Async Code

Exception handling is a critical part of asynchronous programming. When you're dealing with asynchronous operations, there's always a possibility that something might go wrong. The operation could fail, the network could go down, data could be corrupted - the list goes on. Without proper exception handling, these errors could cause your application to crash or behave unpredictably.

Exceptions are propagated when you use `await` on the task. If the task has thrown any exceptions, `await` will re-throw that exception.

Code: csharp

```csharp
try
{
    string result = await GetWebsiteContentAsync();
}
catch (HttpRequestException ex)
{
    Console.WriteLine($"An error occurred: {ex.Message}");
}
```

In this example, we make a web request using the fictitious `FetchDataFromWebAsync` method. If the request fails and throws an `HttpRequestException`, our `catch` block will handle it and write an error message to the console.

If you're dealing with multiple `Tasks` and want to handle exceptions for each Task independently, you can use `Task.ContinueWith`. This method creates a continuation that executes when the task completes, regardless of the state of the antecedent task.

Code: csharp

```csharp
var task = FetchDataFromWebAsync();
task.ContinueWith(t =>
{
    if (t.IsFaulted)
    {
        Console.WriteLine($"An error occurred: {t.Exception.InnerException.Message}");
    }
});
```

In this example, `ContinueWith` is used to specify an action that will happen when the task completes. If the task is faulted (an unhandled exception was thrown), it writes an error message to the console.



## File I/O

***

File Input/Output (I/O) is a critical aspect of many applications and is well supported in C# through the `System.IO` namespace. This namespace provides numerous classes that enable reading from and writing to files, creating new files and directories, and performing operations such as moving, copying, or deleting files.

### FileStream

The `FileStream` class, part of the `System.IO` namespace, provides a powerful and flexible interface for reading from and writing to files. As a core component of C#'s I/O library, `FileStream` supports both sequential and random file access, allowing you to interact with a file's content anywhere, not just at its beginning or end.

A `FileStream` object can be seen as a cursor into the contents of a file, much like a text cursor that you move when editing a document. You can place this cursor at any position within the file and perform read or write operations.

#### Creating a FileStream

There are several ways to create a `FileStream`. One common approach is using its constructor directly, as shown in the following code snippet:

Code: csharp

```csharp
FileStream fs = new FileStream("test.dat", FileMode.OpenOrCreate, FileAccess.ReadWrite);
```

In this example, the `FileStream` constructor takes three arguments:

1. The first argument is a string specifying the path to the file.
2. The second argument is an enumeration of the type `FileMode`, which determines how the operating system should open the file. In this case, `FileMode.OpenOrCreate` means that the file should be opened if it exists; otherwise, a new file should be created.
3. The third argument is an enumeration of the type `FileAccess`, which indicates the type of access you want to the file. Here, `FileAccess.ReadWrite` grants the rights to read from and write to the file.

#### Reading and Writing with FileStream

To write data to a file, you use the `Write` method of the `FileStream` class.

Code: csharp

```csharp
byte[] data = new byte[] { 1, 2, 3, 4, 5 };
fs.Write(data, 0, data.Length);
```

In this example, `Write` is called on the `FileStream` object `fs` to write the byte array `data` to the file. The second and third arguments to `Write` are the starting point in the array and the number of bytes to write, respectively.

To read data from a file, you can use the `Read` method of the `FileStream` class, as shown in the following example:

Code: csharp

```csharp
byte[] data = new byte[1024];
int bytesRead = fs.Read(data, 0, data.Length);
```

In this case, `Read` is called on the `FileStream` object `fs` to read bytes into the `data` array. The second and third arguments to `Read` are the starting point in the array and the maximum number of bytes to read, respectively. `Read` returns the actual number of bytes read, which may be less than the requested number if the end of the file is reached.

#### Manipulating the File Position

An important feature of `FileStream` is the ability to get or set the position within the file, represented by the `Position` property. For example, you can move to the start of the file with the following code:

Code: csharp

```csharp
fs.Position = 0;
```

Or, you can move to a specific position within the file:

Code: csharp

```csharp
fs.Position = 50; // Moves to the 51st byte in the file.
```

This feature of random access is particularly useful when dealing with large files or when you need to jump to specific sections of a file.

#### Closing the FileStream

Finally, when you're done with a `FileStream`, it's essential to close it to free up the resources it's using. You can do this with the `Close` method:

Code: csharp

```csharp
fs.Close();
```

Alternatively, since `FileStream` implements `IDisposable`, you can take advantage of the `using` statement to automatically close the stream:

Code: csharp

```csharp
using (FileStream fs = new FileStream("test.dat", FileMode.OpenOrCreate, FileAccess.ReadWrite))
{
    // perform file operations...
}
```

When the `using` block is exited (either after normal execution or an exception), the `Dispose` method is called on `fs`, which in turn calls `Close`, ensuring that the file is properly closed.

### StreamReader and StreamWriter

`StreamReader` and `StreamWriter` are powerful classes within the `System.IO` namespace for reading and writing character data. As high-level abstractions, they provide a more convenient interface for dealing with text files than the `FileStream` class.

#### StreamReader

A `StreamReader` reads characters from a byte stream in a particular encoding (such as UTF-8). It's ideal for reading text files.

**Creating a StreamReader**

A `StreamReader` is typically instantiated with a `FileStream` or a file path. For example:

Code: csharp

```csharp
StreamReader sr = new StreamReader("test.txt");
```

This code creates a `StreamReader` to read from the file `test.txt`.

**Reading Data with StreamReader**

`StreamReader` provides several methods to read data from the stream. For instance, you can read one line at a time with `ReadLine`:

Code: csharp

```csharp
string line = sr.ReadLine();
```

To read the entire content of the file at once, you can use the `ReadToEnd` method:

Code: csharp

```csharp
string content = sr.ReadToEnd();
```

Remember to close the `StreamReader` when you're done with it:

Code: csharp

```csharp
sr.Close();
```

#### StreamWriter

While `StreamReader` is used for reading text data, `StreamWriter` is used for writing text data. It's an efficient way to write text to a file or a stream.

**Creating a StreamWriter**

A `StreamWriter` can be instantiated in a similar way to `StreamReader`. You can pass a `FileStream` or a file path to the constructor:

Code: csharp

```csharp
StreamWriter sw = new StreamWriter("test.txt");
```

This code creates a `StreamWriter` that writes to the file "test.txt".

**Writing Data with StreamWriter**

`StreamWriter` provides several methods for writing data to the stream. You can write a string with the `Write` method:

Code: csharp

```csharp
sw.Write("Hello, World!");
```

To write a string and then immediately follow it with a newline, use `WriteLine`:

Code: csharp

```csharp
sw.WriteLine("Hello, World!");
```

Remember to close the `StreamWriter` when you're done with it:

Code: csharp

```csharp
sw.Close();
```

In StreamReader and StreamWriter, you can use the `using` statement, which automatically closes the stream when the `using` block is exited. This ensures that resources are correctly disposed of, even if an exception is thrown within the block:

Code: csharp

```csharp
using (StreamWriter sw = new StreamWriter("test.txt"))
{
    sw.WriteLine("Hello, World!");
}
```

### File and Directory

The `File` and `Directory` classes in the `System.IO` namespace contain static methods for creating, copying, deleting, moving, and opening files and directories and performing various other file and directory operations.

#### File

The `File` class allows you to work with files. It provides static methods, so you don't need to instantiate the class to use these methods.

**Creating and Writing to a File**

The `WriteAllText` method writes a specified string to a file. If the file already exists, it will be overwritten. If it doesn't exist, the method will create it:

Code: csharp

```csharp
File.WriteAllText("test.txt", "Hello, World!");
```

**Reading from a File**

The `ReadAllText` method reads all text from a file and returns it as a string:

Code: csharp

```csharp
string content = File.ReadAllText("test.txt");
Console.WriteLine(content);
```

**Checking if a File Exists**

You can check whether a file exists using the `Exists` method:

Code: csharp

```csharp
if (File.Exists("test.txt"))
{
    Console.WriteLine("The file exists.");
}
```

#### Directory

The `Directory` class provides static methods for manipulating directories.

**Creating a Directory**

You can create a directory using the `CreateDirectory` method:

Code: csharp

```csharp
Directory.CreateDirectory("TestDirectory");
```

This code creates a new directory named `TestDirectory`. If the directory already exists, this method does not create a new directory but doesn’t return an error.

**Checking if a Directory Exists**

You can check whether a directory exists using the `Exists` method:

Code: csharp

```csharp
if (Directory.Exists("TestDirectory"))
{
    Console.WriteLine("The directory exists.");
}
```

**Getting Files and Subdirectories**

The `GetFiles` method returns the names of files in a directory, and the `GetDirectories` method returns the names of subdirectories:

Code: csharp

```csharp
string[] files = Directory.GetFiles("TestDirectory");
string[] subdirectories = Directory.GetDirectories("TestDirectory");
```



## Network I/O

***

Network Input/Output (I/O) forms the backbone of most modern applications. It's how applications interact with networks, allowing them to send and receive data to and from remote servers.

C# provides comprehensive support for `Network I/O` operations through its `System.Net` and `System.Net.Sockets` namespaces, among others. These namespaces include a variety of classes and methods that encapsulate the complexity of network programming, making it easier for developers to create network-centric applications.

### HttpClient

The `HttpClient` class in C# is a part of the `System.Net.Http` namespace and provides a modern, flexible, and highly configurable way to send HTTP requests and receive HTTP responses from a resource identified by a URI (Uniform Resource Identifier). It's frequently used to consume APIs, download files, or scrape web content.

The `HttpClient` class is designed to be re-used for multiple requests. As such, it's typically instantiated once and re-used throughout the life of an application, which can improve performance and system resource usage by allowing socket reuse.

The `HttpClient` class includes several methods to send HTTP requests. The primary methods are:

* `GetAsync`: Sends a GET request to the specified URI and returns the response body as a string.
* `PostAsync`: Sends a POST request to the specified URI with a specified content.
* `PutAsync`: Sends a PUT request to the specified URI with a specified content.
* `DeleteAsync`: Sends a DELETE request to the specified URI.

Code: csharp

```csharp
HttpClient client = new HttpClient();

// Send a GET request
var response = await client.GetAsync("https://api.example.com/data");

// Ensure we get a successful response
response.EnsureSuccessStatusCode();

// Read the response content
string content = await response.Content.ReadAsStringAsync();

```

In this example, we create an instance of `HttpClient`, send a `GET` request to a specified URI, ensure we received a successful response, and then read the response content into a string.

#### GetAsync

`GetAsync` sends a `GET` request to a specified URI. This is an asynchronous operation, meaning the method returns immediately after calling without waiting for the HTTP response. Instead, it returns a Task representing the ongoing operation, which eventually produces the `HttpResponseMessage` once completed.

Code: csharp

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static readonly HttpClient client = new HttpClient();

    static async Task Main()
    {
        try
        {
            HttpResponseMessage response = await client.GetAsync("http://api.example.com/data");
            response.EnsureSuccessStatusCode();
            string responseBody = await response.Content.ReadAsStringAsync();
            Console.WriteLine(responseBody);
        }
        catch(HttpRequestException e)
        {
            Console.WriteLine("Exception Caught!");
            Console.WriteLine($"Message: {e.Message}");
        }
    }
}
```

In this example, we send a `GET` request to `http://api.example.com/data`, and then read the response body into a string.

#### PostAsync

`PostAsync` is another method in the `HttpClient` class. It sends a POST request to a specified URI and some HTTP content. Like `GetAsync`, it's an asynchronous operation and returns a `Task<HttpResponseMessage>`.

Code: csharp

```csharp
using System;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

class Program
{
    static readonly HttpClient client = new HttpClient();

    static async Task Main()
    {
        try
        {
            var json = "{\"name\":\"John Doe\"}";
            HttpContent content = new StringContent(json, Encoding.UTF8, "application/json");
            HttpResponseMessage response = await client.PostAsync("http://api.example.com/data", content);
            response.EnsureSuccessStatusCode();
            string responseBody = await response.Content.ReadAsStringAsync();
            Console.WriteLine(responseBody);
        }
        catch(HttpRequestException e)
        {
            Console.WriteLine("Exception Caught!");
            Console.WriteLine($"Message: {e.Message}");
        }
    }
}
```

In this case, we send a JSON object as the body of our POST request.

#### PutAsync

`PutAsync` works much like `PostAsync`, but it sends a `PUT` request instead. It's used when you want to update a resource at a specific URI with some new data.

Code: csharp

```csharp
using System;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

class Program
{
    static readonly HttpClient client = new HttpClient();

    static async Task Main()
    {
        try
        {
            var json = "{\"id\":1,\"name\":\"John Doe Updated\"}";
            HttpContent content = new StringContent(json, Encoding.UTF8, "application/json");
            HttpResponseMessage response = await client.PutAsync("http://api.example.com/data/1", content);
            response.EnsureSuccessStatusCode();
            string responseBody = await response.Content.ReadAsStringAsync();
            Console.WriteLine(responseBody);
        }
        catch(HttpRequestException e)
        {
            Console.WriteLine("Exception Caught!");
            Console.WriteLine($"Message: {e.Message}");
        }
    }
}

```

In this example, we send a PUT request to update the resource at `http://api.example.com/data/1` with new data.

#### DeleteAsync

Finally, `DeleteAsync` sends a `DELETE` request to a specified URI. It's typically used when deleting a resource at a specific URI.

Code: csharp

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static readonly HttpClient client = new HttpClient();

    static async Task Main()
    {
        try
        {
            HttpResponseMessage response = await client.DeleteAsync("http://api.example.com/data/1");
            response.EnsureSuccessStatusCode();
            string responseBody = await response.Content.ReadAsStringAsync();
            Console.WriteLine(responseBody);
        }
        catch(HttpRequestException e)
        {
            Console.WriteLine("Exception Caught!");
            Console.WriteLine($"Message: {e.Message}");
        }
    }
}
```

In this case, we send a `DELETE` request to `http://api.example.com/data/1` to delete the resource.
