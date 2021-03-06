---
title: "Arrays"
teaching: 30
exercises: 0
questions:
- "How does C++ represent multiple values of the same type?"
objectives:
- "Learn how to declare and use arrays in C++."
- "Learn how to pass arrays as arguments to functions."
keypoints:
- "Arrays provide a convenient way of storing many values of the same type."
- "Arrays are defined by a name and elements are accessed using an index."
- "C++ supports multi-dimensional arrays."
- "Arrays can only be passed by reference as parameters to functions."
---
An array is a sequence of elements of the same type. The elements of an array are placed in contiguous memory locations so that they 
can be individually referenced by adding an index to a memory address. An array is named using a unique identifier. Arrays provide
a convenient way of storing multiple values without having to declare a separate variable for each value.

For example, five values of type `int` can be declared as an array without having to declare five different variables 
each with its own identifier. Instead, using an array the five `int` values are stored in contiguous memory locations, and all 
five can be accessed using just a single identifier and an associated index.

In the diagram below, `my_array` represents an array containing five integer values of type `int`:

<img src="{{ site.github.url }}/fig/11-arrays-repr-01.png"/>
 
Each block represents an element of the array, which in this case are values of type `int`. These elements are numbered from 0 to 4, 
with 0 being the first and 4 the last. *In C++, the element of an array are always numbered starting from 0.*
The name `my_array` refers to the memory address of the first element of the array. Elements of the array are accessed by specifying
the index of the required element.

Like a regular variable, an array must be declared before it is used. A typical declaration for an array in C++ is:

~~~
type name [elements];
~~~
{: .code}

For this declaration, `type` is a valid type (such as `int`, `float`, etc.), `name` is a valid identifier, and `elements` 
specifies the length of the array in terms of the number of elements.

To declare the `my_array` array from above, we would use the following:

~~~
int my_array[5];
~~~
{: .code}

NOTE: The number of elements specified must be a constant expression, since arrays are blocks of static memory whose size must be determined 
at compile time.

### Initializing arrays

By default, regular arrays of local scope (for example, those declared within a function) are left uninitialized. This means that 
an array's elements are indeterminate at the point the array is declared. The elements in an array can be explicitly initialized, however, 
by enclosing those initial values in braces. 

For example:

~~~
int my_array[5] = { 16, 2, 77, 40, 12071 }; 
~~~
{: .code}

This statement declares an array that can be represented like this:

<img src="{{ site.github.url }}/fig/11-arrays-repr-02.png"/>
 
The number of values between braces must not be greater than the number of elements in the array. However, it can be less, in which case
the remaining elements are set to their default values (which for fundamental types, means they are set to zero). 

For example:

~~~
int my_array[5] = { 10, 20, 30 }; 
~~~
{: .code}

Will create an array like this:

<img src="{{ site.github.url }}/fig/11-arrays-repr-03.png"/>

The initializer can even have no values, just the braces:

~~~
int my_array[5] = { }; 
~~~
{: .code}

This creates an array of five int values, each initialized with a value of zero:

<img src="{{ site.github.url }}/fig/11-arrays-repr-04.png"/>

When initializing values of an array in this way, there is no need to specify the size of the array, since C++ is able to deduce
this from the number of elements being initialized. 

For example:

~~~
int my_array[] = { 16, 2, 77, 40, 12071 };
~~~
{: .code}

After this declaration, array `my_array` would contain 5 elements, and each element would be initialized with the corresponding value.

This array initialization syntax is common to both C and C++. However, C++ also provides a universal initialization syntax that can be used
for any data types, including arrays. This syntax is almost the same, there is just no equals sin before the first curly brace. 

Both of the following statements are equivalent:

~~~
int my_array[] = { 10, 20, 30 };
int my_array[] { 10, 20, 30 }; 
~~~
{: .code}

Arrays declared with global scope, and those declared directly in a namespace (outside any function), are always initialized. If no explicit 
initializer is  specified, all the elements are default-initialized (with zeroes, for fundamental types).

### Accessing the values of an array

The values of any of the elements in an array can be accessed just like the value of a regular variable of the same type. The syntax is:

~~~
name[index]
~~~
{: .code}

The following diagram shows how to access each element of the `my_array` array, either to reference the value of the element, or to store a new value at
that location:

<img src="{{ site.github.url }}/fig/11-arrays-access.png"/>
 
For example, the following statement stores the value 75 in the third element of `my_array`:

~~~
my_array[2] = 75;
~~~
{: .code}

The following statement copies the value of the third element of `my_array` to a variable called `x`:

~~~
x = my_array[2];
~~~
{: .code}

The expression `my_array[2]` is itself a variable of type `int`.

In C++, it is possible to exceed the valid range of indices for an array. The compiler will typically try to detect this situation and flag it as
a warning to the user, but it is not always possible to determine this at compile-time. Instead, this may cause an error to occur at runtime,
since accessing out-of-range elements can return invalid values, or overwrite important data in the program. The programmer should be very
careful to ensure this situation does not occur.

It is important to note the two different uses of brackets with arrays. One is to specify the size of an array when it is declared, and 
the other is to specify the index of an element to be accessed.

~~~
int my_array[5];         // declaration of a new array
my_array[2] = 75;        // access to an element of the array.  
~~~
{: .code}

This example shows some other valid operations with arrays:

~~~
my_array[0] = a;
my_array[a] = 75;
b = my_array[a+2];
my_array[my_array[a]] = my_array[2] + 5;
~~~
{: .code}

Here is a slightly more complex example:

~~~
// arrays example
#include <iostream>
using namespace std;

int my_array[] = {16, 2, 77, 40, 12071};
int n, result = 0;

int main()
{
  for (n = 0 ; n < 5 ; ++n )
  {
    result += my_array[n];
  }
  cout << result << endl;
  return 0;
}
~~~
{: .code}

This program generates the output:

~~~
12206
~~~
{: .output}

### Multi-dimensional arrays

Multi-dimensional arrays in C++ are defined by specifying more than one dimension. A C++ array with two dimensions can be considered 
as a two-dimensional array comprising elements of the same uniform data type.

<img src="{{ site.github.url }}/fig/11-arrays-multi-01.png"/>

Here, `my_array` represents a two-dimensional array of 3 rows and 5 columns of type `int`. The C++ syntax for this is:

~~~
int my_array[3][5];
~~~
{: .code}

To reference a specific element, for example, the element at the intersecton of the second row and fourth column, the expression would be 
(remember that array indices always begin with zero):

~~~
my_array[1][3]
~~~
{: .code}

<img src="{{ site.github.url }}/fig/11-arrays-multi-02.png"/>

Multi-dimensional arrays are not limited to two dimensions, but can be declared with any number of dimensions. Be aware that
the amount of memory needed for the array can increase substantially with each added dimension. 

For example:

~~~
char century [100][365][24][60][60];
~~~
{: .code}

This declares a five-dimensional array with one element for each second in a century. This amounts to more than 3 billion characters, so this 
declaration would consume more than 3 gigabytes of memory!

Multi-dimensional arrays are just an abstraction for programmers. They are stored in the same way as single dimensional arrays, except that
the compiler remembers the size of each dimension and uses this to calculate the location of the element.

The following two pieces of code produce the exactly the same result, but one uses a two-dimensional array while the other uses a simple array: 

<table border="1">
<tr><th>multi-dimensional array</th><th>pseudo multi-dimensional array</th></tr>
<tr><td><pre><code>
const int WIDTH = 5;
const int HEIGHT = 3;

int my_array[WIDTH][HEIGHT];
int n, m;

int main()
{
  for (int n = 0; n < HEIGHT; n++)
    for (int m = 0; m < WIDTH; m++)
      my_array[n][m] = (n+1) * (m+1);
}
</code></pre></td><td><pre><code>
const int WIDTH = 5;
const int HEIGHT = 3;

int my_array[HEIGHT * WIDTH];


int main()
{
  for (int n = 0; n < HEIGHT; n++)
    for (int m = 0; m < WIDTH; m++)
      my_array[n * WIDTH + m] = (n+1) * (m+1);
}
</code></pre></td></tr>
</table>

The memory contents after running either of these programs will be the same, and will consist of:

<img src="{{ site.github.url }}/fig/11-arrays-multi-03.png"/>

### Advanced Topics

### Arrays as function parameters

At some point, we may need to pass an array to a function. In C++, it is not possible to pass the entire block of memory 
represented by an array to a function directly as an argument, but it can be passed instead by its address. In practice, this has 
almost the same effect, and it is a much faster and more efficient operation.

To accept an array as parameter for a function, the parameters can be declared as the array type, but omitting the 
actual size of the array. For example:

~~~
void procedure(int arr[])
~~~
{: .code}

This function accepts a parameter of type "array of int". An array can be passed to this function as follows:

~~~
int myarray[40];

procedure(myarray);
~~~
{: .code}

Here you have a complete example: 

~~~
// arrays as parameters
#include <iostream>
using namespace std;

void printarray(int arr[], int length) {
  for (int n = 0; n < length; ++n)
    cout << arr[n] << ' ';
  cout << endl;
}

int main ()
{
  int firstarray[] = {5, 10, 15};
  int secondarray[] = {2, 4, 6, 8, 10};
  printarray(firstarray,3);
  printarray(secondarray,5);
}
~~~
{: .code}

The output from this program is:

~~~
5 10 15
2 4 6 8 10
~~~
{: .output}

In the code above, the first parameter (`int arr[]`) accepts any array whose elements are of type `int` of any length. 
For that reason, it is often necessary to provide a second parameter that tells the function the length of the array that 
is passed to it. In this case the length is used to determine how many loop iterations are required to display all the
array values.

In a function declaration, it is also possible to include multi-dimensional arrays. For multi-demensional array paramemters, the
first dimension is always left empty. 

For example, a function with a 3-dimensional array as argument could be: 

~~~
void procedure(int myarray[][3][4])
~~~
{: .code}

Notice that the first set of brackets is left empty, while the following ones specify sizes for their respective dimensions. This is 
necessary in order for the compiler to be able to determine the depth of each additional dimension.

In a way, passing an array as argument always loses a dimension. The reason is that the array is actully being passed using a *pointer*. This is a 
common source of errors for novice programmers. Pointers are explained in greater detail in a subsequent lesson.

### Library arrays

The arrays we've discussed so far are built-in arrays. These are inherited from the C language. They are a great feature, but 
by restricting its copy and easily decay into pointers, they probably suffer from an excess of optimization.

To overcome some of these issues with language built-in arrays, C++ provides an alternative array type as a standard container. It is a type 
template (a class template, in fact) defined in header `<array>`.

Containers are a library feature that falls out of the scope of this tutorial, and thus the class will not be explained in detail here. Suffice 
it to say that they operate in a similar way to built-in arrays, except that they allow being copied (an actually expensive operation that 
copies the entire block of memory, and thus to use with care) and decay into pointers only when explicitly told to do so (by means of its 
member data).

Just as an example, these are two versions of the same example using the language built-in array described in this chapter, and the 
container in the library:

<table border="1">
<tr><th>built-in array</th><th>library array</th></tr>
<tr><td><pre><code>
#include &lt;iostream&gt;

using namespace std;

int main()
{
  int myarray[3] = {10,20,30};

  for (int i = 0; i < 3; ++i)
    ++myarray[i];

  for (int elem : myarray)
    cout << elem << endl;
}
</code></pre></td><td><pre><code>
#include &lt;iostream&gt;>
#include &lt;array&gt;
using namespace std;

int main()
{
  array&lt;int,3&gt; myarray {10,20,30};

  for (int i = 0; i < myarray.size(); ++i)
    ++myarray[i];

  for (int elem : myarray)
    cout << elem << endl;
}
</code></pre></td></tr>
</table>

As you can see, both kinds of arrays use the same syntax to access its elements: `myarray[i]`. Other than that, the main differences are how the 
arrays are declared, and the inclusion of an additional header for the library array. Notice also how it is easy to access the size 
of the library array.
