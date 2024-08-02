# Prototype Pollution

Certainly! Here’s a detailed and enhanced version of Chapter Six on Prototype Pollution, retaining and expanding on all details from your original text:

***

### Chapter Six: Prototype Pollution

## Introduction

Prototype pollution is a critical vulnerability that arises when user-controlled data is used to manipulate the prototype of objects in JavaScript. This manipulation can lead to serious security issues, such as DOM XSS (Cross-Site Scripting) or Remote Code Execution (RCE). In JavaScript, the `__proto__` property allows access to and modification of an object's prototype chain. When misused, especially in conjunction with functions like `JSON.parse()`, it can become a significant attack vector.

For instance:

```javascript
({__proto__:"foo"}).hasOwnProperty('__proto__') // false
(JSON.parse('{"__proto__":"foo"}')).hasOwnProperty('__proto__') // true
```

This shows that while `__proto__` is typically a special property, it becomes a regular property when JSON is parsed, creating a potential vulnerability.

Prototype pollution is not limited to `__proto__` but also involves `constructor.prototype` and other methods, potentially leading to additional exploits and vulnerabilities.

### Technique

Prototype pollution techniques vary depending on the targeted properties and methods. Key techniques include:

* **Direct Manipulation**: Altering `__proto__` or `constructor.prototype` to inject or modify properties directly.
* **Indirect Manipulation**: Exploiting insecure handling of user inputs, such as JSON or query parameters, to manipulate object properties.

### Source

A prototype pollution source is the method or vector through which the vulnerability is triggered. Sources can include:

* **JSON Payloads**: Malicious JSON data that alters prototype properties.
* **Query Strings**: URL parameters that can inject or modify properties.
* **URL Hashes**: URL fragments processed insecurely, leading to prototype pollution.

For example, an injection vector like `?__proto__[property]=value` represents a prototype pollution source.

### Gadget

A gadget is a property or method that becomes a tool for exploitation due to prototype pollution. Gadgets interact with vulnerable sinks within the application, such as:

* **Evaluation Functions**: Methods like `eval()` or `Function()` that execute code dynamically.
* **Sensitive Methods**: Functions that rely on object properties and are susceptible to manipulation.

The polluted property becomes a gadget when it impacts critical parts of the application, enabling potential exploits.

### Potential Gadget

A potential gadget is a property identified as vulnerable to prototype pollution but has not yet been confirmed to affect a relevant sink. To identify potential gadgets:

* **Explore Property Behavior**: Analyze how polluted properties interact with application functions.
* **Test for Impact**: Determine if the polluted properties influence security-sensitive operations.

## Client-side Prototype Pollution

Client-side prototype pollution often targets vulnerabilities that can lead to DOM XSS. The goal is to inject properties into `Object.prototype` and observe their impact on JavaScript or HTML execution.

### **Finding Prototype Pollution**

To detect client-side prototype pollution:

1.  **Inject Malicious Vectors**: Use vectors like `?__proto__[foo]=bar` to modify `Object.prototype`:

    ```javascript
    console.log(Object.prototype);
    // Output might include: {foo: 'bar', constructor: ƒ, ...}
    ```
2.  **Test Alternate Methods**: Check other access methods:

    ```plaintext
    ?constructor[prototype][foo]=bar
    ?__proto__.foo=bar
    ```
3.  **Inspect Application Behavior**: Verify if injected properties impact the application:

    ```javascript
    Object.prototype.someProperty = 'value';
    console.log(someObject.someProperty); // Check if this affects behavior
    ```

### **Modification of Native Methods**

Prototype pollution can alter native methods such as `Object.keys`. For example:

```plaintext
?__proto__[keys]=0 // Overwrites Object.keys method
```

While this is complex to exploit directly, it can be used in conjunction with other bugs to achieve significant impact.

### **Native Browser APIs**

Native browser APIs that accept object literals can also be vulnerable. Examples include:

*   **`fetch()` API**:

    ```javascript
    Object.prototype.body = 'foo=bar';
    const request = new Request('/myEndpoint', { method: 'POST' });
    fetch(request);
    ```
*   **Options Object**:

    ```javascript
    Object.prototype.headers = {foo: 'bar'};
    const init = { method: 'POST' };
    fetch('/end-point', init);
    ```
*   **`Object.defineProperty()`**:

    ```javascript
    Object.prototype.configurable = true;
    Object.prototype.writable = true;
    let obj = {};
    Object.defineProperty(obj, 'foo', {value: 123});
    obj.foo = 'overwritten';
    ```

### **Finding Gadgets**

To discover gadgets:

1. **Use Tools**: Employ tools like Burp Suite with its embedded browser to test for prototype pollution and gadgets.
2.  **Manual Testing**: Utilize methods such as `Object.defineProperty()` to monitor property access:

    ```javascript
    Object.defineProperty(Object.prototype, 'potentialGadget', {
      __proto__: null,
      get() {
        console.trace();
        return 'test';
      }
    });
    ```

## Server-side Prototype Pollution

Server-side prototype pollution (SSPP) is more challenging to detect, especially without source code access. Techniques for detection and exploitation include:

### **Blackbox Detection of SSPP**

1.  **Use Node.js Inspection Flags**:

    ```bash
    node --inspect your-app.js
    ```
2. **Analyze with Chrome DevTools**: Inspect `Object.prototype` and interact with it using Chrome DevTools.
3. **Pause Execution**: Use `--inspect-brk` to pause execution before the application runs and analyze the state.

## **Manual Testing for SSPP**

**Altering Parameter Limits**\
Manipulate parameter limits to probe for vulnerabilities:

```plaintext
/?a=1&b=1&...&targetParam=reflected
```

Prototype pollution can alter limits:

```json
{
  "__proto__": {
    "parameterLimit": 26
  }
}
```

**Using Question Marks in Parameter Names**\
Probe for vulnerabilities by manipulating query parameters:

```json
{
  "__proto__": {
    "ignoreQueryPrefix": true
  }
}
```

### &#x20;**Converting Parameters to JavaScript Objects**

Examine if parameters are treated as objects using `allowDots` options:

```json
{
  "__proto__": {
    "allowDots": true
  }
}
```

### Defense

**Avoid Using Objects as Maps**\
Prefer `Set` and `Map` instead of objects for maintaining collections to prevent prototype pollution:

```javascript
let allowedTags = new Set();
allowedTags.add('b');
```

**Harden Node.js**\
Use Node.js flags to disable prototype pollution:

```bash
node --disable-proto=delete app.js
```

**Use Null Prototypes**\
Create objects with null prototypes to avoid inheritance issues:

```javascript
Object.create(null);
```

## Summary

Prototype pollution is a serious vulnerability that allows attackers to manipulate global prototypes, leading to significant security risks like DOM XSS and RCE. This chapter provides a comprehensive guide to detecting and exploiting both client-side and server-side prototype pollution, including methods for identifying and leveraging gadgets, strategies for manual testing, and effective defense mechanisms.

***
