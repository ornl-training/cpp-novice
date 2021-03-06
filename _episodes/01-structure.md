---
title: "Structure of a Program"
teaching: 15
exercises: 5
questions:
- "What are the basic elements of a C++ program?"
- "How do I use comments in C++?"
- "What are namespaces?"
objectives:
- "Learn the basic structure of a C++ program."
keypoints:
- "C++ formatting is very flexible, whitespace generally doesn't matter."
- "C++ has two styles of comments, for single lines, and for multi-lines."
- "Libraries generally exist in a separate namespace."
---

Let's start with the simple "Hello World" program, and look at it in more detail:

~~~
1 // My first Hello World program
2 #include <iostream>
3
4 int main() 
5 {
6   std::cout << "Hello World!" << std::endl;
7   return 0;
8 }
~~~
{: .code}

Let's examine this program line by line:

Line 1: `// My first Hello World program`
: Two slash signs indicate that the rest of the line is a comment inserted by the programmer but which has no effect on the behavior of the 
program. Programmers use them to include short explanations or observations concerning the code or program. In this case, it is a brief 
introductory description of the program.

Line 2: `#include <iostream>`
: Lines beginning with a hash sign `#` are directives read and interpreted by what is known as the preprocessor. They are special lines 
interpreted before the compilation of the program itself begins. In this case, the directive `#include <iostream>`, instructs the preprocessor 
to include a section of standard C++ code, known as *header iostream*, that allows to perform standard input and output operations, such as 
writing the output of this program (Hello World) to the screen.

Line 3: A blank line.
: Blank lines have no effect on a program. They simply improve readability of the code.

Line 4: `int main ()`
: This line initiates the declaration of a function. Essentially, a function is a group of code statements which are given a name: in this case, 
this gives the name "main" to the group of code statements that follow. Functions will be discussed in detail in a later chapter, but 
essentially, their definition is introduced with a succession of a type `int`, a name `main` and a pair of parentheses `()`, optionally 
including parameters.
The function named `main` is a special function in all C++ programs; it is the first function called when the program is started. The execution 
of all C++ programs begins with the `main` function, regardless of where the function is actually located within the code.

Lines 5 and 7: `{` and `}`
: The open brace `{` at line 5 indicates the beginning of `main`'s function definition, and the closing brace `}` at line 7, indicates its end. 
Everything between these braces is the function's body that defines what happens when main is called. All functions use braces to indicate 
the beginning and end of their definitions.

Line 6: `std::cout << "Hello World!" << std::endl;`
: This line is a C++ statement. A statement is an expression that can actually produce some effect. It is the meat of a program, specifying its 
actual behavior. Statements are executed in the same order that they appear within a function's body.
This statement has the following parts: First, `std"::cout`, which identifies the standard character output device (usually, this is the computer screen). 
Second, the insertion operator `<<`, which indicates 
that what follows is inserted into `std::cout`. Next, a sentence within quotes `"Hello world!"`, is the content inserted into the standard output,
and this is followed by another insertion operation. Finally, `std::endl` specifies the "end of line" so that any additional output will be on
subsequent lines. Notice that the statement ends with a semicolon `;`. This character marks the end of the statement, just as the period ends a sentence in 
English. All C++ statements must end with a semicolon character. One of the most common syntax errors in C++ is forgetting to end a 
statement with a semicolon.

Line 7: `return 0;`
: The `main` function is just like any other function. Since it was declared to return a value of type `int`, we should do that. This statement
says that the function should always return the value 0.

You may have noticed that not all the lines of this program perform actions when the code is executed. There is a line containing a comment 
(beginning with `//`). There is a line with a directive for the preprocessor (beginning with `#`). There is a line that defines a function 
(in this case, the `main` function). And, finally, a line with a statements ending with a semicolon (the insertion into `cout`), which was within 
the block delimited by the braces ( `{ }` ) of the main function. 

The program has been structured into separate lines and properly indented, in order to make it easier to understand for the humans reading it. 
Unlike languages such as Python, C++ does not have strict rules on indentation or on how to split instructions in different lines. For example, 
instead of:

~~~
int main() 
{
  std::cout << "Hello World!" << std::endl;
  return 0;
}
~~~
{: .code}

We could have written the whole function on one line:

~~~
int main() { std::cout << "Hello World!" << std::endl; return 0; }
~~~
{: .code}

This would have had exactly the same meaning as the preceding code.

In C++, the separation between statements is specified with an ending semicolon `;`, with the separation into different lines not mattering 
at all for this purpose. Many statements can be written in a single line, or each statement can be in its own line. The division of 
code in different lines serves only to make it more legible and schematic for the humans that may read it, but has no effect on the 
actual behavior of the program.

Preprocessor directives (those that begin by `#`) are not covered by this general rule since they are not statements. They are lines read and 
processed by the preprocessor before proper compilation begins. Preprocessor directives must be specified in their own line and, 
because they are not statements, do not have to end with a semicolon.

### Comments

As noted above, comments do not affect the operation of the program; however, they provide an important tool to document directly within the 
source code what the program does and how it operates.

C++ supports two ways of commenting code:

~~~
// line comment
/* block 
comment */ 
~~~
{: .code}

The first type is known as line comment, and it discards everything from the pair of slash signs`//` to the end of the same line. The second type
is known as block comment, and it discards everything between the `/*` characters and the first appearance of the `*/` characters, with the 
possibility of including multiple lines.

Let's use this to improve our second program: 

~~~
/* My second program in C++
   with more comments */

#include <iostream>

int main()
{
  std::cout << "Hello World! ";     // prints "Hello World!" with no "new line"
  std::cout << "I'm a C++ program" << std::endl ; // prints "I'm a C++ program" on the same line
  return 0;
}
~~~

While adding the comments, we also took the opportunity to show you how `std::endl` can be used to control
where the output is printed.

### Using Namespaces

If you have seen C++ code before, you may have seen `cout` being used instead of `std::cout`. These both refer to the same
object.

The name `cout` is part of the standard C++ library. Everything within this library are declared in a *namespace*,
which in this case is called `std`. 

In order to refer to the elements in the `std` namespace a program has to either *qualify* each use with `std::`, or introduce visibility 
of its components. The most typical way to introduce visibility of these components is via a `using` declaration:

~~~
using namespace std;
~~~
{: .code}

The above declaration enables all elements in the `std` namespace to be accessed in an *unqualified* manner (without the `std::` prefix).

With this in mind, the last example can be rewritten as follows:

~~~
/* My second program in C++
   with more comments */

#include <iostream>
using namespace std;

int main()
{
  cout << "Hello World! ";     // prints "Hello World!" with no "new line"
  cout << "I'm a C++ program" << endl ; // prints "I'm a C++ program" on the same line
  return 0;
}
~~~
{: .code}

Both ways of accessing the elements of the `std` namespace are valid in C++ and produce the exactly same behavior. For simplicity, and 
to improve readability, the examples in these lessons will usually use the unqualified method.

Namespaces are explained in more detail in a later chapter.

>## Challenge
> Often you will see statements that include the sequence "`\n`" at the end of a string, rather than using "`<< std::endl`" as shown below.
>
> ~~~
> std::cout << "Hello World!\n";
> ~~~
> {: .code}
>
> Both of these sequences refer to "end of line" or inserting a new line at the end of the string. However there is a
> subtle difference: `endl` also flushes the stream, which forces any output to be displayed. In most cases, they can be
> used interchangeably.
>
> Compile and run the program above to see the output it generates. Now modify the program to use 
> "`\n`" instead of "`endl`". Re-compile and re-run it to verify that it generates the same output.
>
{: .challenge}
