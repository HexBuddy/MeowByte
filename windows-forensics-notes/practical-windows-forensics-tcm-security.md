---
description: Course Notes
---

# Practical Windows Forensics - TCM Security

{% hint style="info" %}
**Lab Setup That I Used for Notes Can Be Found Here** [**here**](https://bluecapesecurity.com/build-your-forensic-workstation)
{% endhint %}

## Your First C Program

In the previous tutorial you learned how to [install C](https://www.programiz.com/c-programming/getting-started) on your computer. Now, let's write a simple C program.

The following program displays `Hello, World!` on the screen.

```
#include <stdio.h>

int main() {

    printf("Hello, World!");

    return 0;
}
```

**Output**

```
Hello World!
```

**Note:** A `Hello World!` program includes the basic syntax of a programming language and helps beginners understand the structure before getting started. That's why it is a common practice to introduce a new language using a `Hello World!` program.

It's okay if you don’t understand how the program works right now. We will learn about it in upcoming tutorials. For now, just write the exact program and run it.

***

### Working of C Program <a href="#working-of-c-program" id="working-of-c-program"></a>

Congratulations on writing your first C program.Now, let's see how the program works.

```
#include <stdio.h>

int main() {

    printf("Hello, World!");

    return 0;
}
```

Notice the following line of code:

```
printf("Hello, World!");
```

Here, `printf` statement prints the text `Hello, World!` to the screen.

Remember these important things about `printf`:

* Everything you want to print should be kept inside parentheses `()`.
* The text to be printed is enclosed within double quotes `""`.
* Each `printf` statement ends with a semicolon `;`.

Not following the above rules will result in errors and your code will not run successfully.

***

### Basic Structure of a C Program <a href="#basic-structure" id="basic-structure"></a>

As we have seen from the last example, a C program requires a lot of lines even for a simple program.

For now, just remember that every C program we will write will follow this structure:

```
#include <stdio.h> 

int main() {

  // your code

  return 0;
}
```

And, we will write out code inside curly braces `{}`.

Next, we will be learning about [C comments](https://www.programiz.com/c-programming/comments).
