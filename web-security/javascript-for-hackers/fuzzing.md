# Fuzzing

***

## The Truth About Fuzzing

Fuzzing is often associated with uncovering exploitable vulnerabilities or crashes. While it’s true that fuzzing can help find such issues, it can also be an effective way to understand browser behavior, which is the focus of this chapter. By using fuzzing, you can significantly accelerate your learning of JavaScript and discover nuances in browser implementations. Although specifications provide a source of information on JavaScript behavior, relying solely on them is insufficient due to potential browser quirks or incorrect implementations. Thus, fuzzing is crucial for discovering the actual behavior.

My initial experience with behavioral fuzzing involved identifying characters permissible in a JavaScript protocol URL. I began by manually injecting HTML entities into an anchor `href` attribute and checking if the link retained the JavaScript protocol by hovering over it. This manual method was inefficient, leading me to develop a server-side fuzzing tool in PHP in 2008. This tool looped through characters in chunks, uncovering interesting results, such as:

```plaintext
jav&#56325ascript:al&#56325ert(1)// worked in Firefox 2!
```

This discovery underscored the importance of fuzzing, as manually testing 56,000 entities would have been daunting. Back then, computers were slower, and I had to process characters in chunks. Today, with faster machines, fuzzing millions of characters takes only seconds.

## Fuzzing JavaScript URLs

With modern browsers, my fuzzing approach involves using `innerHTML` and DOM properties, as they produce different results. To fuzz JavaScript URLs, you can use the DOM like this:

```javascript
log = [];
let anchor = document.createElement('a');
for (let i = 0; i <= 0x10ffff; i++) {
    anchor.href = `javascript${String.fromCodePoint(i)}:`;
    if (anchor.protocol === 'javascript:') {
        log.push(i);
    }
}
console.log(log); // Outputs: 9, 10, 13, 58
```

This simple code creates an array and anchor, iterates through all possible Unicode code points (over 1 million), and checks if the generated link retains the JavaScript protocol. Browsers handle this quickly now, unlike the past when it could crash them. To fuzz other parts of the `href`, adjust the placeholder's position:

```javascript
anchor.href = `${String.fromCodePoint(i)}javascript:`;
```

Running the modified code yields different results, like:

```plaintext
0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,32
```

Notice the `NULL` at the start (character code 0 is `NULL`), specific to the DOM code path, which doesn't work with regular HTML. This highlights the need to fuzz both DOM and `innerHTML`. Verify interesting results by regenerating the DOM you fuzzed. For example, to use the form feed character before the protocol:

```javascript
let anchor = document.createElement('a');
anchor.href = `${String.fromCodePoint(12)}javascript:alert(1337)`;
anchor.append('Click me');
document.body.append(anchor);
```

By clicking the link, you confirm the fuzz code works. Experiment with different code points and ask questions like, “Can you use multiple characters?” Remember, when using the DOM, HTML entities aren’t decoded when directly editing properties, except for HTML-based ones. Thus, for HTML entities, use `innerHTML`. Here's an example:

```html
<a href="&#12;javascript:alert(1337)">Test</a><!-- JavaScript protocol works -->
```

It works, but `NULL` won’t in HTML, as shown:

```html
<a href="&#0;javascript:alert(1337)">Test</a><!-- JavaScript protocol doesn't work -->
```

The above doesn't work, demonstrating why it's crucial to verify results in both the DOM and `innerHTML` or HTML. Automation tools like Puppeteer can help verify results without manual intervention each time.

## Fuzzing HTTP URLs

You can also fuzz HTTP URLs using the hostname to check success. Similar to JavaScript URLs, loop through Unicode code points, inject characters into the `href`, and verify the hostname matches the expected value:

```javascript
let a = document.createElement('a');
let log = [];
for (let i = 0; i <= 0x10ffff; i++) {
    a.href = `${String.fromCodePoint(i)}https://garethheyes.co.uk`;
    if (a.hostname === 'garethheyes.co.uk') {
        log.push(i);
    }
}
console.log(log);
```

The code finds HTTP URLs supporting the same characters as JavaScript URLs. Again, `NULL` works in the DOM but not in HTML. To find client-side open redirects, fuzz protocol-relative URLs using double forward slashes, which inherit the page’s protocol. Fuzzing inside the forward slashes reveals supported characters:

```javascript
let a = document.createElement('a');
let log = [];
for (let i = 0; i <= 0x10ffff; i++) {
    a.href = `/${String.fromCodePoint(i)}/garethheyes.co.uk`;
    if (a.hostname === 'garethheyes.co.uk') {
        log.push(i);
    }
}
input.value = log; // Outputs: 9, 10, 13, 47, 92
```

Whitespace and backslash characters can be used between the slashes, like a forward slash.

## Fuzzing HTML

Beyond JavaScript URLs, the same approach works for fuzzing HTML using the `innerHTML` API to quickly discover parser quirks. Ask yourself questions like, “What characters are allowed in closing HTML comments?” If an HTML comment is closed, the tag after it should render. Verify this with the `querySelector` API:

```javascript
let log = [];
let div = document.createElement('div');
for (let i = 0; i <= 0x10ffff; i++) {
    div.innerHTML = `<!----${String.fromCodePoint(i)}><span></span>-->`;
    if (div.querySelector('span')) {
        log.push(i);
    }
}
console.log(log); // Outputs: 33, 45, 62
```

Similar to DOM properties fuzzing, this method takes longer as browsers do more work. Create a `div`, loop through Unicode code points, use `innerHTML` to create an HTML comment, and inject a Unicode character before the closing angle bracket. If the span is rendered, log the result. In Chrome, any of these characters close a comment after a double hyphen: `!-->`.

Try this in other browsers and experiment by moving the placeholder. Previously, in Firefox, new lines before the greater than symbol were possible. You can use `querySelector` inversely, checking if a starting comment tag worked by seeing if the span wasn’t rendered. Using this technique, I found a parsing flaw in Firefox, allowing NULLs inside opening comment tag hyphens.

Here's how to fuzz HTML comments after the hyphen:

```javascript
let log = [];
let div = document.createElement('div');
for (let i = 0; i <= 0x10ffff; i++) {
    div.innerHTML = `<!-${String.fromCodePoint(i)}- ><span></span>-->`;
    if (!div.querySelector('span')) {
        log.push(i);
    }
}
console.log(log); // Outputs: 45
```

The placeholder is inside the starting comment tag, and `querySelector` checks if the span doesn’t exist. Expect one result, 45 (hyphen character). If more appear, you’ve found a browser bug. When fuzzing, ensure your markup doesn’t create false positives. For example, include a deliberate greater than symbol after the space and hyphen to prevent the span being consumed as another tag by fuzzing characters. Defensive coding saves time.

## Fuzzing Known Behaviors

If you’re unsure where to start fuzzing for new behavior, you can test existing behavior for deviations. A good starting point is whitespace. Construct a fuzz string for characters that count as whitespace. Use a function call to include whitespace between the function identifier and parentheses. Define a function in a try-catch block and attempt to call it with an identifier and added character using `eval`:

```javascript
function x() {}
log = [];
for (let i = 0; i <= 0x10ffff; i++) {
    try {
        eval(`x${String.fromCodePoint(i)}()`);
        log.push(i);
    } catch (e) {}
}
console.log(log);
// Outputs: 9,10,11,12,13,32,160,5760,8192,8193,8194,8195,8196,8197,8198,8199,8200,8201,8202,8232,8233,8239,8287,12288,65279
```

This reveals many characters, showing whitespace can occur between an identifier and parentheses. To thoroughly fuzz, test various positions and contexts of characters. If you find unexpected behavior, report it. Deviations could allow JavaScript sandbox escapes by fooling parsers into misinterpreting characters.

You can also fuzz strings using character pairs, keeping operations fast. Slow performance arises with nested fuzzing, which may

be required for multiple character sequences. Start with fewer iterations, then increase. While slower, nested fuzzing reveals unique issues. Generally, fuzzing single characters suffices.

***
