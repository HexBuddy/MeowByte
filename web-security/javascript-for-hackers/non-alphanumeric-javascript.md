# Non-Alphanumeric JavaScript

It all started when the users of the Slackers forum noticed a surprising new post from Yosuke Hasegawa, an outstanding Japanese security researcher. In the post, he detailed how you can execute JavaScript without using alphanumeric characters. This was a revelation to all of us, and we started to dissect how it works. The basic idea was to use square brackets and JavaScript expressions to create strings, then use numeric indexes based on expressions to access and concatenate strings to create valid property names and eventually write arbitrary JavaScript, all without alphanumeric characters. This technique is also known as JSF\*ck (obscuring the "u" to avoid displaying swear words). From now on, I’ll refer to it as "non-alphanumeric" JavaScript or non-alpha JS.

To construct non-alpha JS, you first need a way of generating a number. Because JavaScript is loosely typed, you can do that using the infix operator “+”. This operator will attempt to convert the expression that follows into a number or NaN (Not a Number) if it can’t be converted. So the first step is getting a zero:

```javascript
+[] // 0
```

Great, so we have zero, but this will only allow us to get the first character of a string:

```javascript
'abc'[+[]] // 'a'
```

To get “b”, you can combine the square bracket accessor with an array and get a reference to an item in the array. JavaScript allows you to increment/decrement this value just like it was an identifier:

```javascript
[+[]] // creates an array with 0 in it
[+[]][+[]] // gets the first element in the array
++[+[]][+[]] // increments the first element in the array to create 1
'abc'[++[+[]][+[]]] // 'b'
```

Hope you’re following along. It might be worth trying each individual code snippet in the console to understand what’s going on. Once you’ve grasped this concept, you can begin generating strings and numbers quite easily. You simply need to nest the generated arrays, keep incrementing them, and concatenate the letters to form JavaScript properties. Let’s generate the number two, I’ll use spaces to help distinguish each number:

```javascript
++[ ++[+[]][+[]] ] [+[]] // 2
```

Normally, you wouldn’t use spaces; I’ve just added them so it’s easier to follow. So as you can see with the above code, you create an array with +\[], which is a zero, then you access the first element in the array again using +\[], and then use the increment operator to increase the number. You wrap that in another array and follow the same process. It becomes harder to read as you nest further, but once you get the concept, you should be able to write it.

We can now get “c” in our text:

```javascript
'abc'[++[ ++[+[]][+[]] ] [+[]]] // 'c'
```

Right, so we have the basics of generating numbers without alphanumeric characters, but how do you generate strings? We again take advantage of JavaScript’s loosely typed nature to convert different types into strings. For example, let’s look at booleans. We can extract the characters “f”, “a”, “l”, “s”, “e” from "false", and follow a similar process as we did for numbers, but this time we’ll use the logical not operator, which returns false if the operand can be converted to true and vice versa. This means we can use a blank array again and convert it to a boolean:

```javascript
![] // false
```

When we’ve got a boolean, we need to convert it to a string so we can extract the required characters. To do this, we simply concatenate it with another array, which forms a string with the boolean and a blank array that gets converted to a blank string:

```javascript
![] + [] // "false" (string)
```

Great, so now we have our characters, but how do we extract them? We can follow the same process as before: we place the expression inside an array, get the first element in the array (our string), and then use an index to get a single character:

```javascript
[![] + []] // add the false string to an array
[![] + []][+[]] // get the first item of the array
[![] + []][+[]][+[]] // 'f' - get the first character of the string
```

You can then follow this process for the remaining characters and just increase the indexes as we did for incrementing the numbers. The easiest way of doing this is to label your expressions with comments as I’ve been doing and then combine them. So, we need the next character, which is at position one. If you go to the code snippet for one and copy it like below:

```javascript
++[+[]][+[]] // 1
```

Then get the false string from the other example:

```javascript
[![] + []][+[]] // "false" (string)
```

Then combine them together with the false string first and an accessor containing the number:

```javascript
[
![] + []
][+[]]
[
++[+[]][+[]]
] // 'a'
```

I’ve added spaces above for clarity. As you collect characters, it’s wise to save them in a text file with comments to show what they represent. This makes it easier to construct strings from them. Hopefully, by now, you’re pretty confident in creating these characters. Let’s continue and create the remaining characters for "false".

```javascript
[
![] + []
][+[]]
[
++[++[+[]][+[]]][+[]]
] // 'l'

[
![] + []
][+[]]
[
++[++[++[+[]][+[]]][+[]]][+[]]
] // 's'

[
![] + []
][+[]]
[
++[++[++[++[+[]][+[]]][+[]]][+[]]][+[]]
] // 'e'
```

As you can see above, only little modification is required when generating the "s" and "e" characters. In fact, we can reuse this whole process for generating the opposite of true, which is false. After all, this is a JavaScript hacking book, and we have to look for shortcuts. So, remember when we found out !\[] generates false? If we use the logical not operator again, it will convert it to true:

```javascript
!![] // true
```

We just replace the single exclamation mark in each code example we’ve previously generated with a double one. For example:

```javascript
[![] + []][+[]][+[]] // 'f' becomes
[!![] + []][+[]][+[]] // 't'
```

And so on:

```javascript
[
!![] + []
][+[]]
[
++[+[]][+[]]
] // 'r'

[
!![] + []
][+[]]
[
++[++[+[]][+[]]][+[]]
] // 'u'
```

We already have an “e”, so we don’t have to generate that again. You can see now how to generate characters quite easily. You might be thinking about how you can generate arbitrary JavaScript. First, you need to get access to a function, and to do that, you need to generate some characters that, when used as an accessor, get a function. Then you can use that function to get the constructor of it, which will be the Function constructor. Once you have access to the Function constructor, you can call it to generate arbitrary JavaScript. But let’s worry about that later. First, let’s get a function. Conveniently, there is a nice short function we can already access with the characters that we’ve generated. The `at` function allows you to get a single character of a string or an element of an array depending on which object you use it on. We are going to use that because it’s short in length. So, we first need a blank array:

```javascript
[]
```

Then we add an accessor:

```javascript
[] [
]
```

Then we add the string “a” and concatenate it with “t”:

```javascript
[] [
[
![] + []
][+[]]
+
[!![] + []][+[]]
] // "at" function
```

Once we have access to a function, we gain the ability to generate a lot more characters because a function can be converted to a string:

```javascript
[].at + '' // "function at() { [native code] }"
```

If we look at the characters we’ve previously generated, the only characters remaining to generate are “o”, “c”, and “n”. We can generate “n” using undefined, which we’ll do next. First, we create an empty array and attempt to access the first element, which is undefined:

```javascript
[][+[]] // undefined
```

Then we convert it to a string and access the second character, which is at position one:

```javascript
[[][+[]] + []][+[]][++[+[]][+[]]] // 'n'
```

Now we can generate the others to create the constructor property. To generate the missing characters, we can reuse the `at` function, convert it to a string, generate the required positions, and finally extract them.

First, create an empty array and access the first element:

```javascript
[][+[]

] // undefined
```

Then concatenate it with an empty string:

```javascript
[][+[]] + [] // "undefined"
```

Finally, extract the second character from the result:

```javascript
[[][+[]] + []][+[]][++[+[]][+[]]] // 'n'
```

Once you have all the characters, you can combine them:

```javascript
[][
[!![] + []][+[]]
+
[
![] + []
][+[]]
+
[
[][+[]] + []
][+[]][++[+[]][+[]]]
+
[
![] + []
][+[]]
+
[!![] + []][+[]]
+
[][+[]] + []
][+[]][++[++[++[++[+[]][+[]]][+[]]][+[]]][+[]]
```

You now have the constructor property, which means you can generate a reference to the Function constructor:

```javascript
[][
[
!![] + []
][+[]]
+
[
![] + []
][+[]]
+
[
[][+[]] + []
][+[]][++[+[]][+[]]]
+
[
![] + []
][+[]]
+
[!![] + []][+[]]
+
[][+[]] + []
][+[]][++[++[++[++[+[]][+[]]][+[]]][+[]]][+[]]
] [ [
![] + []
][+[]] ]
[
[
+!+[]
][+!+[]]
+
[++[+[]][+[]]] // 't'
+
[
!![] + []
][+[]][
++[+[]][+[]]
]
+
[![] + []][+[]]
+
[
[+[]][+[]]
] +
[!![] + []][+[]][+[]]
+
[
[+!+[]]
] +
[
[++[+[]][+[]]][+[]][+[]]
]
+
[
++[++[+[]][+[]]][+[]]
][+[]][+[]]
+
[++[++[+[]][+[]]][+[]]]
+
[[] + []][+[]][+!+[]]
][+[]][
[
+!+[]][+!+[]
] +
[++[+[]][+[]]][+[]][++[+[]][+[]]] // 'f'
][+[]][+!+[]]
```

Once you have a reference to the Function constructor, you can call it:

```javascript
[][
[!![] + []][+[]]
+
[
![] + []
][+[]]
+
[
[][+[]] + []
][+[]][++[+[]][+[]]]
+
[
![] + []
][+[]]
+
[!![] + []][+[]]
+
[][+[]] + []
][+[]][++[++[++[++[+[]][+[]]][+[]]][+[]]][+[]]
] [ [
![] + []
][+[]] ]
[
[
+!+[]
][+!+[]]
+
[++[+[]][+[]]] // 't'
+
[
!![] + []
][+[]][
++[+[]][+[]]
]
+
[![] + []][+[]]
+
[
[+[]][+[]]
] +
[!![] + []][+[]][+[]]
+
[
[+!+[]]
] +
[
[++[+[]][+[]]][+[]][+[]]
]
+
[
++[++[+[]][+[]]][+[]]
][+[]][+[]]
+
[++[++[+[]][+[]]][+[]]]
+
[[] + []][+[]][+!+[]]
][+[]][
[
+!+[]][+!+[]
] +
[++[+[]][+[]]][+[]][++[+[]][+[]]] // 'f'
][+[]][+!+[]]
```

Once you have access to the Function constructor, you can call it to generate arbitrary JavaScript. This allows you to execute any code you want, as long as you can construct the required characters. The process can be tedious, but it’s a great exercise in understanding the flexibility and power of JavaScript.

## Constructing Complex Scripts

💡 Today's Hacking Tip! 💡 New obfuscation technique in XSS using Non-Alphanumeric JavaScript

We will embed https://example.com into a JS Non-Alphanumeric code :&#x20;

```
var h = [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var t = [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var p = [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var s = [![] + []][+[]] + [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var colon = [![] + []][+[]] + [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var slash = [![] + []][+[]] + [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var e = [![] + []][+[]] + [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var x = [![] + []][+[]] + [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var a = [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var m = [![] + []][+[]] + [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var p = [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var l = [![] + []][+[]] + [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var e = [![] + []][+[]] + [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];

var url = h + t + t + p + s + colon + slash + slash + e + x + a + m + p + l + e + dot + c + o + m;

```

Construct and Execute the Fetch Script: We will create a fetch request to the generated URL and log the response to the console:&#x20;

```
var fetch = [!![] + []][+[]] + [![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]] + [!![] + []][+[]];
var console_log = c + o + n + s + o2 + l + e + '.' + l + o + g;

Function(fetch + '(' + url + ')' + '.then(function(response) { return response.text(); }).then(function(data) { ' + console_log + '(data); })')();
```

This script fetches data from "https://example.com" and logs the response text to the console using only non-alphanumeric characters.
