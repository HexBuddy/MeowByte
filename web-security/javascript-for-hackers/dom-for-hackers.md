# DOM for Hackers

## Where’s My Window?

### **Understanding the Window Object**

In web development, the **window object** is the global object in the browser environment. It represents the browser window and provides methods and properties that control the browser window itself. Accessing the window object is crucial in hacking scenarios because it allows you to execute JavaScript functions like `eval`, which can lead to potential security exploits.

### **Accessing the Window Object**

There are multiple ways to access the window object, even in restricted environments:

1. **Using `document.defaultView`:**
   * This property of the document object returns the window object.
   *   Example:

       ```javascript
       document.defaultView.alert(1337); // Displays an alert with the number 1337
       ```
2. **Via DOM Nodes:**
   * Every DOM node has an `ownerDocument` property, which refers to the document object. You can use this to reach the window object.
   *   Example:

       ```javascript
       let node = document.createElement('div');
       node.ownerDocument.defaultView.alert(1337);
       ```
3. **Using Event Properties:**
   * In some browsers, the `path` or `composedPath()` of an event contains the window object.
   *   Example using `composedPath()`:

       ```html
       <img src onerror="event.composedPath().pop().alert(1337)">
       ```
4. **Special Cases in SVG:**
   * SVG elements use `evt` instead of `event`, but you can still access the window object.
   *   Example:

       ```html
       <svg><image href=1 onerror="evt.composedPath().pop().alert(1337)"></svg>
       ```
5. **Using the Error Object:**
   * The `prepareStackTrace` method allows customization of stack traces, letting you retrieve the window object.
   *   Example:

       ```javascript
       Error.prepareStackTrace = function (error, callSites) {
         callSites.shift().getThis().alert(1337);
       };
       new Error().stack;
       ```

## Scope of an HTML Event

### **Event Scoping**

When JavaScript code runs as an event handler, it has access to the properties of the element on which it was triggered and the document object. This scoping allows you to reference properties without specifying their full paths.

### **Using Scoped Properties**

Because of the scoping rules, you can call functions and access properties directly within an event handler:

1. **Using `defaultView`:**
   *   Example:

       ```html
       <img src onerror="defaultView.alert(1337)">
       ```
   * Here, the `defaultView` is accessed from the document, which gives us the window object.
2. **Creating and Appending Elements:**
   * You can manipulate DOM elements directly.
   *   Example:

       ```html
       <img src onerror="s=createElement('script');s.append('alert(1337)');appendChild(s)">
       ```

## DOM Clobbering

### **What is DOM Clobbering?**

DOM clobbering occurs when a global JavaScript variable is overwritten or "clobbered" by a DOM element. This can lead to unexpected behaviors in the application.

### **How DOM Clobbering Works**

Historically, browsers allowed elements with `id` or `name` attributes to become global variables. This feature was intended as a shortcut for developers but can be exploited for malicious purposes.

1.  **Basic Example:**

    ```html
    <form id="loginForm"></form>
    <script>
      loginForm.submit(); // Refers to the form element with id "loginForm"
    </script>
    ```
2. **Exploiting DOM Clobbering:**
   * If a script checks for the existence of a variable and uses a default if it doesn't exist, you can inject an element to alter its behavior.
   *   Example:

       ```html
       <a name="currentUrl"></a>
       <script>
         let url = window.currentUrl || 'http://example.com';
         console.log(url); // Outputs [object HTMLAnchorElement] instead of the URL
       </script>
       ```

## Summary

In this chapter, we explored several techniques for accessing the window object and manipulating the DOM to demonstrate potential security risks. By understanding these methods, developers can better safeguard their applications against similar attacks.

* **Accessing the window object** is critical for executing arbitrary JavaScript code, which can lead to security vulnerabilities.
* **Event scoping** allows for convenient shortcuts but can be exploited if not properly understood.
* **DOM clobbering** illustrates the importance of not relying on implicit global variables, especially those that can be controlled via DOM manipulation.

***
