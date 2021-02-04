---
title: Single-Dimensional Arrays and C-Strings
author: Dr. Alireza Manashty
date: 2021-02-04
category: cpp
layout: post
---

# Single-Dimensional Arrays and C-Strings

## 7.1 Introduction and Objectives

> <http://www.cplusplus.com/doc/tutorial/arrays/>

## 7.2 Array Basics

A **one-dimensional array** is a structured collection of components (often
called array elements) that can be accessed individually by specifying
the **position** of a component with a single index value.

Here is the syntax template of a one-dimensional array declaration:
```cpp
DataType ArrayName [ConstIntExpression];
```

In the syntax template, **DataType** describes what is stored in each
component of the array. Array components may be of any type, but for now
we limit our discussion to simple data types (e.g. integral and floating
types). **ConstIntExpression** indicates the size of the array declared.
That is, it specifies the number of array components in the array. It
must have a value **greater than 0**. If the value is `n`, the range of the
index values is `0` to `n-1`. 
For example, the declaration`int number[50];` creates the number array which has 50 components, 
each capable of holding one int value. In other words, the number array 
has a total of `50` components, all of type `int`.

**Fundamental Operations on a One-dimensional Array:**
Now let's look at how to access individual components of an array. 
The syntax template for accessing an array component is:

```cpp
ArrayName[ IndexExpression ]
```

The index expression must result in an integer value. It can be of type
`char`, `short`, `int`, `long`, or `bool` value because these are all *integral*
types. The simplest form of index expression is a constant. For example:

> `number[0]` specifies the 1st component of the number array
>
> `number[1]` specifies the 2nd component of the number array
>
> `number[2]` specifies the 3rd component of the number array
>
> `number[3]` specifies the 4th component of the number array
>
> `number[4]` specifies the 5th component of the number array
>
> .
>
> .
>
> .
>
> `number[48]` specifies the 2nd last component of the number array
>
> `number[49]` specifies the last component of the number array

To store values in the number array, we can do the following:

```cpp
for (int i=0; i<50; i++)
{
    number[i]=i; //store a number in each array element

    cout << "number[" << i << "] = " << number[i] <<
    endl;
}
```

Each array element can be treated as a simple variable. Here, an integer
value is assigned to each array element, which has been declared to hold
data type int.

To use the values stored in the number array, we can treat each array
element as a simple variable of data type `int`. For example:

```cpp
for (int i=0; i<50; i++)
{
    number[i]=2*number[i]; //double the value in each array element
    //and store it in the array element
    cout << "number[" << i << "] = " << number[i] << endl;
}
```

For the number array, the valid index range is from `0` to `49`. If the
`IndexExpression` results in a value less than `0` or greater than the
`array_size` minus `1`, then the index is considered to be **out-of-bounds**.
For instance, `number[50]` is trying to access a memory location outside
of the number array.

**Array Initialization in its Declaration**

A variable can be initialized in its declaration. For example:

```cpp
int value = 25;
```

The value `25` is called an *initializer*. Similarly, an array can be
initialized in its declaration. A list of initial values for array
elements can be specified. They are **separated with commas** and 
**enclosed within braces**. For example:

```cpp
int age[5] = {23, 56, 87, 92, 38};
```

In this declaration, `age[0]` is initialized to `23`, `age[1]` is
initialized to `56`, and so on. There must be **at least one** initial value
between braces. If too many initial values are specified, a syntax error
will occur. If the number of initial values is less than the array size,
the remaining array elements will be initialized to **zero**.

In C++, the array size can be omitted when it is initialized in the
declaration. For example:

```cpp
int age[] = {23, 56, 87, 92, 38, 12, 15, 6, 3};
```

The compiler determines the size of the age array according to how many
initial values are listed. Here, the size of the age array is `9`.

**Example:** 
This program adds two integer arrays and displays the arrays.

```cpp
// Program Arraypractice.cpp will add two arrays and store the sum
// in the third array. Print them all out to the screen.


#include <iostream>

using namespace std;

int main ()
{
    const int MAX_ARRAY = 5;
    int a[MAX_ARRAY];
    int b[MAX_ARRAY];
    int c[MAX_ARRAY];
    int index;

    // Ask users to enter values for array a[].
    for(index = 0; index < MAX_ARRAY; index++)
    {
        cout << "Please input a number for the array element: ";
        cin >> a[index];
    }

    // Ask users to enters value for array b[].
    for(index = 0; index < MAX_ARRAY; index++)
    {
        cout << "Please input a number for the array element: ";
       cin >> b[index];
    }

    // Store the sum of array a[] and array b[] to array c[].
    for(index = 0; index < MAX_ARRAY; index++)
    {
        c[index] = a[index] + b[index];
    }

    // Add code to print out each of the arrays
    for (index = 0; index < MAX_ARRAY; index++)
    {
        cout << "array a is " << a[index] << endl;
        cout << "array b is " << b[index] << endl;
        cout << "array c is " << c[index] << endl;
        cout << endl;
    }
    
    return 0;
}
```

> <http://www.cs.uregina.ca/Links/class-info/110/arrays/oneD_array_ggg.html>

`std::array` is a container that encapsulates **fixed size arrays**.

The struct combines the performance and accessibility of a C-style array
with the benefits of a standard container, such as knowing its own size,
supporting assignment, random access iterators, etc.

std::array satisfies the requirements of Container and
ReversibleContainer except that default-constructed array is not empty
and that the complexity of swapping is linear, satisfies the
requirements of ContiguousContainer, (since C++17) and partially
satisfies the requirements of SequenceContainer.

There is a special case for a zero-length array (`N == 0`). In that case,
`array.begin() == array.end()`, which is some unique value. The effect of
calling `front()` or `back()` on a **zero-sized array** is undefined.

An array can also be used as a tuple of `N` elements of the same type.

>  <https://en.cppreference.com/w/cpp/container/array>

## 7.3 Passing Arrays to Functions

Before we get into passing arrays, let's review the format for using
functions.

```cpp
#include <iostream>
using namespace std;
// function prototypes go here
// e.g. int getMax( int [], int );
int main()
{
  // variables declared here
  // function calls interspersed with other code
  // e.g. max = getMax(array, 10);
  return 0;
}
// end main

// Function header
// function_return_type function_name(*parameter_list*)
// e.g. int getMax(int ary[], int len)
{
  // code for function
  // e.g. max = ary[i];
} // end function
```

Now, let's take a closer look at how those arrays are passed. In C++,
arrays are **not** passed by value to functions, they are **passed by reference**. 
Because of this, you do not have to use the & reference
character. You simply pass the base address of an array to a function.
To do this, just supply the name of the array.

For example, suppose you had made the following declarations:

```cpp
const int size=10;
int ary[size];
```

Further suppose you wanted to pass this array to a function
called `getMax` which expected the array reference as a parameter. 
The call to that function would be:

```cpp
getMax(ary, size);
```

Notice that only the array name `ary` appears in the parameter list; it is
not followed by any subscripts at all.

**Example:**
This program adds two integer arrays and displays the arrays.

```cpp
// Program Arraypractice.cpp will add two arrays and store the sum
// in the third array. Print them all out to the screen.

#include <iostream>

using namespace std;

void add_arrays(int [], int [], int [], int);

int main ()
{
    const int MAX_ARRAY = 5;
    int a[MAX_ARRAY];
    int b[MAX_ARRAY];
    int c[MAX_ARRAY];
    int index;
    
    // Ask users to enter values for array a[].
    cout << "Please input 5 values for a array." << endl;
    for (index = 0; index < MAX_ARRAY; index++)
    {
       cout << index+1 << ": ";
       cin >>a[index];
    }
    
    // Ask users to enters value for array b[].
    
    cout << "Please input 5 values for b array." << endl;;
    
    for (index = 0; index < MAX_ARRAY; index++)
    {
        cout << index+1 << ": ";
        cin >>b[index];
    }
    
    // Store the sum of array a[] and array b[] to array c[].
    // for (index = 0; index < MAX_ARRAY; index++)
    // {
    //     c[index] = a[index]+ b[index];
    // }
    
    // call for the function add_arrays() to add two arrays
    add_arrays( a, b, c, MAX_ARRAY);
    
    //To separate the output from other stuff
    cout << endl;
    
    // Add code to print out each of the arrays
    for (index = 0; index < MAX_ARRAY; index++)
    {
        cout << "a[" << index << "] = " << a[index] << endl;
        cout << "b[" << index << "] = " << b[index] << endl;
        cout << "c[" << index << "] = " << c[index] << endl;
        cout << endl;
    }
    return 0;
}
// a function adds two arrays

void add_arrays(int x[], int y[], int z[], int len)
{
    for ( int i = 0; i < len; i++)
    {
        z[i] = x[i] + y[i];
    }
    return;
}
```

> <http://www.cs.uregina.ca/Links/class-info/110/arrays/oneD_array_ggg.html>

## 7.4 Preventing Changes of Array Arguments in Functions

As we learned in the last section, there is no way to pass an array by
value and not by reference. So, how we can prevent possible changes of
array arguments? One way to do so is passing the array as a **constant** to
the function.

For instance, if we have:

```cpp
#include <iostream>

using namespace std;

void changeArray(const int array[]);

int main()
{
    int myArray[] = { 1, 2, 3, 4 };
    changeArray(myArray);
    return 0;
}

void changeArray(const int array[])
{
    array[0] += 2; // Compile Error!
}
```

We will get a *compile error* because the program is trying to change a
constant value which is impossible.

## Returning Arrays from Functions

You may try to return an array in you function. For example, you would
write:

```cpp
float[] calculateAreas(int x, int y)
```

However, it is not a valid statement in C++.

## 7.5 Searching Arrays

**Linear search (`O(n)`)**:
One of the approaches to search an array is **Linear Search**. In this
approach you need to loop through the array and compare each element of
the array to the value that you are looking for. This could be done by
using count controlled while loop or for loop.

For instance, if we have an array of characters and we are looking for
the index of character `E` in the array, one of the possible solutions
would be:

```cpp
#include <iostream>

using namespace std;

int main()
{
    char myArray[] = { 'A', 'b', 'E', 'e', 'c' };
    int index;
    for (int i = 0; i < 5; i++)
    {
        if (myArray[i] == 'E')
        {
            index = i;
            break;
        }
    }
    cout << "The index of letter 'E' is " << index << endl;

    return 0;
}
```

**Binary search (`O(logn)`)**:
Another possible approach is **Binary Search** which requires the array
to be sorted.

Let us assume that we are looking for number `19` (X) in the following
array:

  --- --- --- --- ---- ---- ---- ---- ----
  1   4   6   9   12   15   19   20   22
  --- --- --- --- ---- ---- ---- ---- ----

In binary search, after sorting the array, using sort algorithms, the
value that you are looking for `X` will be compared to the **middle value**
of the array. For example, at this stage `19` will be compared with `12`.

  --- --- --- --- ---- ---- ---- ---- ----
  1   4   6   9   12   15   19   20   22
  --- --- --- --- ---- ---- ---- ---- ----

-   If `X` < middle value, it means that the value is in the **first half**
    of the array.

  --- --- --- --- ---- ---- ---- ---- ----
  1   4   6   9   12   15   19   20   22
  --- --- --- --- ---- ---- ---- ---- ----

-   If `X` > middle value, it means that the value is in the **second half**
    of the array.

  --- --- --- --- ---- ---- ---- ---- ----
  1   4   6   9   12   15   19   20   22
  --- --- --- --- ---- ---- ---- ---- ----

-   If `X` = middle value, we already found the index.

  --- --- --- --- ---- ---- ---- ---- ----
  1   4   6   9   12   15   19   20   22
  --- --- --- --- ---- ---- ---- ---- ----

In our example `19` > `12` so we need to search the second half of the
array.

  ---- ---- ---- ----
  15   19   20   22
  ---- ---- ---- ----

Like before, we find the middle value:

  ---- ---- ---- ----
  15   19   20   22
  ---- ---- ---- ----

And compare the middle value with `X` which means `19` = `19`. So we found the
index of `19` in the array.

## 7.6 Sorting Arrays

There are several various ways to sort an array. You could use sorting
algorithms like *insertion sort*, *bubble sort*, *quick sort*. Also, there is
a simple way to sort an array using `sort()` function which is available
in `C++11` and higher compilers.

The corresponding library to `sort()` function is `algorithm`. So, you
would have `#include <algorithm>` at the top of your code.

**About The Function**
So let's go dig into these and figure out what each does and why it does
it.

Found in ~ `#include <algorithm>`

**Parameter 1** `myvector.begin()` ~ The first parameter is where you will be
putting a iterator(Pointer) to the **first** element in the range that you
want to sort. The sort will **include** the element that the iterator points
to.

**Parameter 2** `myvector.end()` ~ The second parameter is almost like the
first but instead of putting a iterator to the first element to sort you
will be putting a iterator to the **last** element. One very important
difference is that the search **won't include** the element that this
iterator points to. It is **[First,Last)** meaning it includes the first
parameter in the sort but it doesn't include the second parameter in the
sort.

**Parameter 3** `myCompFunction() Optional` ~ I will only give a brief
description here, because I will be explaining this parameter in more
detail later. The third parameter is used to define how you do the
search. For example if you have a struct that has 3 different variables
in it, how does the function know which one to sort? Or how does it know
how it should sort it? This is what this parameter is for. I will
explain this more in a bit.

**Function Return** ~ This function doesn't return anything because it
alters the container directly through iterators(Pointers).

Array Example:

```cpp
// sort() Example using arrays.                                                                              
// By Zereo 04/22/13                                   
                 
                                          
#include <iostream>                                 
#include <algorithm>                                
                                                           
using namespace std;                                   
                                                          
const int SIZE = 7;                                    
                                                          
int main()                                                                                                 
{                                                      
                                                          
    int intArray[SIZE] = {5, 3, 32, -1, 1, 104, 53};     
                                                            
    //Now we call the sort function                        
    sort(intArray, intArray + SIZE);                       
                                                            
    cout << "Sorted Array looks like this." << endl;                                                          
    for (size_t i = 0; i != SIZE; ++i)                                                                            
        cout << intArray[i] << " ";                    
                                                              
    return 0;                                                                                                          
}                                                      
```

>  <https://www.cplusplus.com/articles/NhA0RXSz/>

## 7.7 C-String

`const char* c_str() const`. Get *C string* equivalent.

Returns a *pointer* to an array that contains a *null-terminated* sequence
of characters (i.e., a C-string) representing the current value of the
string object.

This array includes the same sequence of characters that make up the
value of the string object plus an additional terminating **null-character**
(`0`) at the end. The pointer returned may be invalidated by further calls to other member
functions that modify the object.

**Parameters**: None
**Return value**: A pointer to the c-string representation of the string
object's value.

Example:

```cpp
// strings and c-strings                                      
                                                                  
#include <iostream>
#include <cstring>
#include <string>

int main ()
{
    std::string str ("Please split this sentence into tokens");
    char * cstr = new char [str.length()+1];
    std::strcpy (cstr, str.c_str());

    // cstr now contains a c-string copy of str
    char * p = std::strtok (cstr," ");

    while(p!=0)
    {
        std::cout << p << '\n';
        p = std::strtok(NULL," ");
    }
    delete[] cstr;
    return 0;
}
```

Output:

```text
Please   
split    
this     
sentence 
into     
tokens  
```

> <http://www.cplusplus.com/reference/string/string/c_str/>

## 7.8 Converting Numbers to Strings

Returns a [string](http://www.cplusplus.com/string) with the
representation of val.

The format used is the same
that [printf](http://www.cplusplus.com/printf) would print for the
corresponding type:


| **type of val**      | **`printf` equivalent**  | **description**
|----------------------|------------------------|-----------------------------
| int                  | `%d`                   | Decimal-base representation of *val*. <br> The representations of negative values are preceded with a minus sign (`-`).
| long                 | `%ld`                  |
| long long            | `%lld`                 |
| unsigned             | `%u`                   | Decimal-base representation of *val*.
| unsigned long        | `%lu`                  |
| unsigned long long   | `%llu`                 | 
| float                | `%f`                   | As many digits are written as needed to represent the integral part, followed by the decimal-point character and six decimal digits. <br> inf (or infinity) is used to represent *infinity*. <br> nan (followed by an optional sequence of characters) to represent NaNs (**Not-a-Number**). <br> The representations of negative values are preceded with a minus sign (-). 
| double               | `%f`                   |
| long double          | `%Lf`                  | 

Parameters

Val => Numerical value.

Return Value => A [string](http://www.cplusplus.com/string) object
containing the representation of val as a sequence of characters.

> <http://www.cplusplus.com/reference/string/to_string/>

## 7.9 Chapter Summary
All in all, in this chapter we learned about arrays. 
At this point we know how declare an array, 
how to pass it to a function, how to sort it, 
and how to search for something in an array.
