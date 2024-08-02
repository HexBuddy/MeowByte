# JavaScript Without Parentheses

## **Calling Functions Without Parentheses**

The concept of calling functions without parentheses in JavaScript is fascinating and opens up various intriguing possibilities. By leveraging JavaScript's unique features, we can achieve this goal and understand the language's depth more quickly. My initial attempt involved experimenting with the `valueOf` method. This method is useful when you want an object to return a primitive value, such as a number. It's commonly used with object literals to make them interact with primitives, enabling operations like addition or subtraction.

**Example: Using `valueOf()`**

```javascript
let obj = {valueOf(){return 1}};
obj + 1; // 2
```

Here, `valueOf` allows us to define a function that gets called when the object is used as a primitive. Attempting to use `alert` directly with `valueOf` results in an "illegal invocation" error because `alert` requires the `this` context to be the `window` object.

**Example: Incorrect Use of `valueOf` with `alert`**

```javascript
let obj = {valueOf: alert};
obj + 1; // Illegal invocation
```

The error occurs because `alert` is not called in the correct context. However, we can override the `window` object's `valueOf` method to achieve our goal.

**Example: Overriding `window.valueOf`**

```javascript
window.valueOf = alert;
window + 1; // calls alert()
```

By changing `window.valueOf`, the `this` context is correct, and `alert` is called successfully. This works because the `window` object is implied, so `valueOf` without `window.` also works:

**Example: Using `valueOf` without `window.`**

```javascript
valueOf = alert;
window + 1; // calls alert()
```

We can also use `toString` similarly:

**Example: Using `toString`**

```javascript
toString = alert;
window + ''; // calls alert()
```

## **Calling Functions with Arguments Without Parentheses**

Next, we can try calling functions with arguments without using parentheses. One approach involves using the `onerror` handler, a global handler for exceptions on the `window` object. The `onerror` handler receives arguments like the error message, URL, line number, column number, and error object. By setting the handler and causing an exception, we can influence the arguments passed to the handler.

**Example: Using `onerror` with `throw`**

```javascript
onerror = alert;
throw 'foo'; // Uncaught foo
```

To execute arbitrary code, replace `alert` with `eval` and inject an equals sign to create a valid JavaScript statement:

**Example: Using `onerror` with `eval`**

```javascript
onerror = eval;
throw "=alert(1)";
```

The throw statement can't be used as an expression, but we can use block statements or JavaScript's automatic semicolon insertion (ASI) to bypass restrictions.

**Example: Using Block Statements**

```javascript
{onerror = eval} throw "=alert(1337)";
```

**Example: Using New Lines**

```javascript
onerror = alert;
throw 1337;
```

JavaScript supports paragraph and line separators for new lines, which can help bypass certain restrictions.

**Example: Using Line and Paragraph Separators**

```javascript
eval("onerror=\u2028alert\u2029throw 1337");
```

## **Throw Expressions**

The `throw` statement accepts expressions, and the comma operator can be used to evaluate expressions from left to right, returning the last operand.

**Example: Comma Operator with `throw`**

```javascript
throw onerror = alert, 1337; // Uncaught 1337
```

This approach can be combined with other techniques to call functions in unexpected ways.

## **Tagged Templates**

Tagged template strings provide another method to call functions without parentheses. By using template literals, we can pass arguments as placeholders, and JavaScript expressions can be embedded within these placeholders.

**Example: Simple Tagged Template**

```javascript
alert`1337`;
```

Placeholders can be defined with `${}` and support nested template strings.

**Example: Placeholders in Template Strings**

```javascript
`${alert(1337)}`;
`${`${alert(1337)}`}`;
```

Using the `Function` constructor with tagged templates allows us to call functions with arbitrary JavaScript.

**Example: Using the Function Constructor**

````javascript
Function`x${'alert(1337)'}```; // calls alert(1337)
````

Reflect object methods like `apply` can also be used to call functions with arguments.

**Example: Using Reflect.apply**

```javascript
Reflect.apply.call`${alert}${window}${[1337]}`; // alert(1337)
```

## **Has Instance Symbol**

Symbols provide unique property keys, and the `hasInstance` symbol allows customization of the `instanceof` operator's behavior, enabling function calls without parentheses.

**Example: Using the HasInstance Symbol**

```javascript
'alert(1337)' instanceof { [Symbol.hasInstance]: eval }; // calls alert(1337)
```

#### Summary

This chapter demonstrated how to define a goal and sub-goals, allowing you to learn various JavaScript features rapidly. We explored the `onerror` handler, tagged template strings, and the `hasInstance` symbol, uncovering surprising behaviors and leveraging them to call functions without parentheses. By having clear goals, you can focus on interesting features and continuously learn new aspects of JavaScript.
