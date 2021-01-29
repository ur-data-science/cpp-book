# Functions

## 6.1 Introduction and Objectives

Functions allow to structure programs in segments of code to perform
individual tasks.

In C++, a function is a group of **statements** that is given a name, and
which can be called from some point of the program

> <http://www.cplusplus.com/doc/tutorial/functions/>

## 6.2 Defining and Calling a Function

The most common syntax to define a function is:

```cpp
type name (parameter1, parameter2, ...) { statements }
```

Where:

-   type is the type of the value returned by the function.
-   name is the identifier by which the function can be called.
-   parameters (as many as needed): Each parameter consists of a type
    followed by an identifier, with each parameter being separated from the
    next by a comma. Each parameter looks very much like a regular variable
    declaration (for example: `int x`), and in fact acts within the function
    as a regular variable which is local to the function. The purpose of
    parameters is to allow passing arguments to the function from the
    location where it is called from.
-   statements is the function's body. It is a block of statements
    surrounded by braces `{}` that specify what the function actually does.


Let's have a look at an example:

```cpp
//  function example
 

#include <iostream>
                       
using namespace std;

int addition(int a, int b)
{
    int r;
    r = a+b;
    return r;
}

int main()
{
    int z;
    z = addition(5, 3);
    cout << "The result is " << z;
}
```

Output:

```text
The result is 8
```

This program is divided in two functions: addition and main. Remember
that no matter the order in which they are defined, a C++ program always
starts by calling main. In fact, main is the only function called
automatically, and the code in any other function is only executed 
**if its function is called from main** (directly or indirectly).

In the example above, main begins by declaring the variable `z` of
type int, and right after that, it performs the first function call: it
calls addition. The call to a function follows a structure very similar
to its declaration. In the example above, the call to addition can be
compared to its definition just a few lines earlier:

![alt text](../images/chapter_06/Picture1.png)

The parameters in the function declaration have a clear correspondence
to the arguments passed in the function call. The call passes two
values, `5` and `3`, to the function; these correspond to the
parameters `a` and `b`, declared for function addition.

At the point at which the function is called from within main, the
control is passed to function addition: here, execution of main is
stopped, and will only resume once the addition function ends. At the
moment of the function call, the value of both arguments (5 and 3) are
copied to the local variables int a and int b within the function.

Then, inside addition, another local variable is declared (`int r`), and
by means of the expression `r=a+b`, the result of `a` plus `b` is assigned
to `r`; which, for this case, where a is `5` and b is `3`, means that `8` is
assigned to `r`.

The final statement within the function:

```cpp
return r;
```

Ends function addition, and returns the control back to the point where
the function was called; in this case: to function main. At this precise
moment, the program resumes its course on main returning exactly at the
same point at which it was interrupted by the call to addition. But
additionally, because addition has a return type, the call is evaluated
as having a value, and this value is the value specified in the return
statement that ended addition: in this particular case, the value of the
local variable `r`, which at the moment of the return statement had a
value of `8`.

![alt text](../images/chapter_06/Picture2.png)

Therefore, the call to addition is an expression with the value returned
by the function, and in this case, that value, `8`, is assigned to `z`. It
is as if the entire function call (`addition(5, 3)`) was replaced by the
value it returns(i.e., `8`).

Then main simply prints this value by calling:

```cpp
cout << "The result is " << z;
```

A function can actually be called multiple times within a program, and
its argument is naturally not limited just to literals:

```cpp
// function example


#include <iostream>

using namespace std;

int subtraction(int a, int b)
{
    int r;
    r = a-b;
    return r;
}

int main()
{
    int x=5, y=3, z;
    
    z = subtraction(7, 2);

    cout << "The first result is" << z << '\n';
    cout << "The second result is" << subtraction(7, 2) << '\n';
    cout << "The third result is" << subtraction(x, y) << '\n';

    z = 4 + subtraction(x, y);

    cout << "The fourth result is" << z << '\n';
}                                                       
```

Output:

```text
The first result is 5
The second result is 5
The third result is 2
The fourth result is 6
```

Similar to the addition function in the previous example, this example
defines a subtract function, that simply returns the difference between
its two parameters. This time, main calls this function several times,
demonstrating more possible ways in which a function can be called.

Let's examine each of these calls, bearing in mind that each function
call is itself an expression that is evaluated as the value it returns.
Again, you can think of it as if the function call was itself replaced
by the returned value:

```cpp
z = subtraction(7, 2);
cout << "The first result is " << z;
```

If we replace the function call by the value it returns (i.e., `5`), we
would have:

```cpp
z = 5;
cout << "The first result is " << z;
```

With the same procedure, we could interpret:

```cpp
cout << "The second result is " << subtraction (7, 2);
```

as:

```cpp
cout << "The second result is " << 5;
```

since `5` is the value returned by `subtraction(7, 2)`.

In the case of:

```cpp
cout << "The third result is " << subtraction (x, y);
```

The arguments passed to subtraction are variables instead of literals.
That is also valid, and works fine. The function is called with the
values `x` and `y` have at the moment of the call: `5` and `3` respectively,
returning `2` as result.

The fourth call is again similar:

```cpp
z = 4 + subtraction (x, y);
```

The only addition being that now the function call is also an operand of
an addition operation. Again, the result is the same as if the function
call was replaced by its result: `6`. Note, that thanks to the commutative
property of additions, the above can also be written as:

```cpp
z = subtraction (x, y) + 4;
```

With exactly the same result. Note also that the semicolon does not
necessarily go after the function call, but, as always, at the end of
the whole statement. Again, the logic behind may be easily seen again by
replacing the function calls by their returned value:

```cpp
z = 4 + 2;
```
> same as `z = 4 + subtraction (x, y);`

```cpp
z = 2 + 4;
```
> same as `z = subtraction (x, y) + 4;`


## 6.3 void Functions

The syntax shown above for functions:

```cpp
type name (argument1, argument2 ...) { statements }
```

Requires the declaration to begin with a type. This is the type of the
value returned by the function. But what if the function does not need
to return a value? In this case, the type to be used is void, which is a
special type to represent the absence of value. For example, a function
that simply prints a message may not need to return any value:

```cpp
//  void function example


#include <iostream>

using namespace std;

void printmessage()
{
    cout << "I'm a function!";
}

int main()
{
    printmessage();
}                                                      
```

Output:

```text
I'm a function!
```

void can also be used in the function's parameter list to explicitly
specify that the function takes no actual parameters when called. For
example, `printmessage` could have been declared as:

```cpp
void printmessage(void)
{
    cout << "I'm a function!";
}
```

In C++, an empty parameter list can be used instead of void with same
meaning, but the use of void in the argument list was popularized by the
C language, where this is a requirement.

Something that in no case is optional are the parentheses that follow
the function name, neither in its declaration nor when calling it. And
even when the function takes no parameters, at least an empty pair of
parentheses shall always be appended to the function name. See
how `printmessage` was called in an earlier example:

```cpp
printmessage();
```

The parentheses are what differentiate functions from other kinds of
declarations or statements. The following would not call the function:

```cpp
printmessage;
```
> <http://www.cs.uregina.ca/Links/class-info/110/functions/index-val-008_ggg.html>


## 6.4 Passing Arguments by Value

In the functions seen earlier, arguments have always been passed *by value*. 
This means that, when calling a function, what is passed to the
function are the values of these arguments on the moment of the call,
which are copied into the variables represented by the function parameters. 
For example, take:

```cpp
int x=5, y=3, z;
z = addition(x, y);
```

In this case, function addition is passed `5` and `3`, which are copies of
the values of `x` and `y`, respectively. These values (`5` and `3`) are used to
initialize the variables set as parameters in the function's
definition, but any modification of these variables within the function
has no effect on the values of the variables `x` and `y` outside it, because
`x` and `y` were themselves not passed to the function on the call, but only
copies of their values at that moment.

![](../images/chapter_06/Picture3.png)

In certain cases, though, it may be useful to access an external
variable from within a function. To do that, arguments can be passed *by reference*, 
instead of *by value*. For example, the function duplicate in this code duplicates 
the value of its three arguments, causing the variables used as arguments to actually be
modified by the call:

```cpp
// passing parameters by reference


#include <iostream>

using namespace std;

void duplicate(int& a, int& b, int& c)
{
    a *= 2;
    b *= 2;
    c *= 2;
}

int main()
{
    int x=1, y=3, z=7;
    duplicate(x, y, z);
    cout << "x=" << x << ", y=" << y << ", z=" << z;
    return 0;
}                                                    
```
Output:
```text
x=2, y=6, z=14
```
> <http://www.cs.uregina.ca/Links/class-info/110/functions/index-val-008_ggg.html>


## 6.5 Modularizing Code

We have been building exceedingly small programs. When a program is
small enough, we can keep all the details of the program in our heads at
once. Real application programs are 100 to 10000 times larger than any
program you have likely written (or maybe even worked on); they are
simply too large and complex to hold all their details in our heads.
They are also written by multiple authors. To build large software
systems requires techniques we have not talked about so far.

One key solution to managing complexity of large software is *modular programming*: 
the code is composed of many different code modules that
are developed separately. This allows different developers to take on
discrete pieces of the system and design and implement them without
having to understand all the rest. But to build large programs out of
modules effectively, we need to be able to write modules that we can
convince ourselves are correct *in isolation* from the rest of the
program. Rather than have to think about every other part of the program
when developing a code module, we need to be able to use *local reasoning*: 
that is, reasoning about just the module and the contract it
needs to satisfy with respect to the rest of the program. If everyone
has done their job, separately developed code modules can be plugged
together to form a working program without every developer needing to
understand everything done by every other developer in the team. This is
the key idea of modular programming.

> <https://www.cs.cornell.edu/courses/cs3110/2019sp/textbook/modules/modular_programming.html>

## 6.6 Overloading Functions

In C++, two different functions can have the same name if their
parameters are different; either because they have a different number of
parameters, or because any of their parameters are of a different type.
For example:

```cpp
//  overloading functions


#include <iostream>

using namespace std;

int operate (int a, int b)
{
    return(a*b);
}

double operate (double a, double b)
{
    return(a/b);
}

int main()
{
    int x=5, y=2;
    double n=5.0, m=2.0;
    
    cout << operate(x, y) << '\n';
    cout << operate(n, m) << '\n';

    return 0;
}
```

Output:

```text
10
2.5
```

In this example, there are two functions called operate, but one of them
has two parameters of type int, while the other has them of type double.
The compiler knows which one to call in each case by examining the types
passed as arguments when the function is called. If it is called with
two int arguments, it calls to the function that has two int parameters,
and if it is called with two doubles, it calls the one with
two doubles.

In this example, both functions have quite different behaviors,
the int version multiplies its arguments, while the double version
divides them. This is generally not a good idea. Two functions with the
same name are generally expected to have -at least- a similar behavior,
but this example demonstrates that is entirely possible for them not to.
Two overloaded functions (i.e., **two functions with the same name**) have
entirely different definitions; they are, for all purposes, different
functions, that only happen to have the same name.

Note that a function cannot be overloaded only by its return type. At
least one of its parameters must have a different type.


### 6.7 Function templates

Overloaded functions may have the same definition. For example:

```cpp
// overloaded functions


#include <iostream>

using namespace std;

int sum(int a, int b)
{
    return a+b;
}

double sum(double a, double b)
{
    return a+b;
}

int main()
{
    cout << sum(10, 20) << '\n';
    cout << sum(1.0, 1.5) << '\n';

    return 0;
}
```

Output:

```text
30
2.5
```

Here, sum is overloaded with different parameter types, but with the
exact same body.

The function sum could be overloaded for a lot of types, and it could
make sense for all of them to have the same body. For cases such as
this, C++ has the ability to define functions with generic types, known
as *function templates*. Defining a function template follows the same
syntax as a regular function, except that it is preceded by
the template keyword and a series of template parameters enclosed in
angle-brackets `<>`:

```cpp
template <template-parameters> function-declaration
```

The template parameters are a series of parameters separated by commas.
These parameters can be generic template types by specifying either
the class or typename keyword followed by an identifier. This identifier
can then be used in the function declaration as if it was a regular
type. For example, a generic sum function could be defined as:

```cpp
template <class SomeType>

SomeType sum(SomeType a, SomeType b)
{
    return a+b;
}
```

It makes no difference whether the generic type is specified with
keyword class or keyword typename in the template argument list (they
are 100% synonyms in template declarations).

In the code above, declaring SomeType (a generic type within the
template parameters enclosed in angle-brackets) allows SomeType to be
used anywhere in the function definition, just as any other type; it can
be used as the type for parameters, as return type, or to declare new
variables of this type. In all cases, it represents a generic type that
will be determined on the moment the template is instantiated.

Instantiating a template is applying the template to create a function
using particular types or values for its template parameters. This is
done by calling the *function template*, with the same syntax as calling
a regular function, but specifying the template arguments enclosed in
angle brackets:

```cpp
name <template-arguments> (function-arguments)
```

For example, the sum function template defined above can be called with:

```cpp
x = sum<int>(10, 20);
```

The `function sum<int>` is just one of the possible instantiations of
function template sum. In this case, by using int as template argument
in the call, the compiler automatically instantiates a version
of sum where each occurrence of SomeType is replaced by int, as if it
was defined as:

```cpp
int sum (int a, int b)
{
    return a+b;
}
```

Let's see an actual example:

```cpp
//  function template


#include <iostream>

using namespace std;

template <class T> T sum(T a, T b)
{
    T result;
    result = a + b;
    
    return result;
}

int main()
{
    int i=5, j=6, k;
    double f=2.0, g=0.5, h;

    k = sum<int>(i, j);
    h = sum<double>(f, g);
    
    cout << k << '\n';
    cout << h << '\n';

    return 0;
}
```

Output:

```text
11
2.5
```

In this case, we have used T as the template parameter name, instead
of SomeType. It makes no difference, and T is actually a quite common
template parameter name for generic types.

In the example above, we used the function template sum twice. The first
time with arguments of type int, and the second one with arguments of
type double. The compiler has instantiated and then called each time the
appropriate version of the function.

Note also how T is also used to declare a local variable of that
(generic) type within sum:

```cpp
T result;
```

Therefore, result will be a variable of the same type as the
parameters a and b, and as the type returned by the function.
In this specific case where the generic type T is used as a parameter
for sum, the compiler is even able to deduce the data type automatically
without having to explicitly specify it within angle brackets.
Therefore, instead of explicitly specifying the template arguments with:

```cpp
k = sum<int>(i, j);
h = sum<double>(f, g);
```

It is possible to instead simply write:

```cpp
k = sum(i, j);
h = sum(f, g);
```

without the type enclosed in angle brackets. Naturally, for that, the
type shall be unambiguous. If sum is called with arguments of different
types, the compiler may not be able to deduce the type
of `T` automatically.

Templates are a powerful and versatile feature. They can have multiple
template parameters, and the function can still use regular **non-templated** types. 
For example:

```cpp
//  function templates


#include <iostream>
using namespace std;

template <class T, class U> bool are_equal(T a, U b)
{
    return (a==b);
}

int main()
{
    if(are_equal(10, 10.0))
        cout << "x and y are equal\n";
    else
        cout << "x and y are not equal\n";

    return 0;
}
```

Output:

```text
x and y are equal
```

Note that this example uses automatic template parameter deduction in
the call to `are_equal`:

```cpp
are_equal(10, 10.0)
```

Is equivalent to:

```cpp
are_equal<int, double>(10, 10.0)
```

There is no ambiguity possible because numerical literals are always of
a specific type: Unless otherwise specified with a suffix, integer
literals always produce values of type int, and floating-point literals
always produce values of type double. Therefore `10` has always
type int and `10.0` has always type double.

### 6.8 Non-type template arguments

The template parameters can not only include types introduced
by class or typename, but can also include expressions of a particular
type:


```cpp
//  template arguments


#include <iostream>

using namespace std;

template <class T, int N> T fixed_multiply(T val)
{
    return val * N;
}

int main() 
{
    cout << fixed_multiply<int, 2>(10) << '\n';
    cout << fixed_multiply<int, 3>(10) << '\n';
}                                                        
```

Output:

```text
20
30
```

The second argument of the fixed_multiply function template is of
type int. It just looks like a regular function parameter, and can
actually be used just like one.

But there exists a major difference: the value of template parameters is
determined on compile-time to generate a different instantiation of the
function fixed_multiply, and thus the value of that argument is never
passed during runtime: The two calls
to fixed_multiply in main essentially call two versions of the function:
one that always multiplies by two, and one that always multiplies by
three. For that same reason, the second template argument needs to be a
constant expression (it cannot be passed a variable).

> <http://www.cplusplus.com/doc/tutorial/functions2/>

## 6.9 Function Declarations, Prototypes, Implementation, Definition

Many people, when learning C++, seem to have some confusion about the
distinction between and purpose of declarations and definitions.
Especially concerning functions or classes. To understand why all this
seemingly pedantic and repetitive stuff is necessary, let's review the
build process.

![](../images/chapter_06/Picture4.png)

First, each .cpp file is compiled independently. During this process any
`#include` directives will first insert the included file into the `.cpp`.
Compilation then processes the `.cpp` from top to bottom, generating
machine language code and outputting this into an `.obj` file. The thing
to keep in mind for purposes of this discussion is that it is a single
pass process from top to bottom, and that it is completely unaware of
anything in other `.cpp` files. Nor is the compiler even aware of anything
in the current `.cpp` file at any point beyond the point at which it is
processing. The code generated by the compiler does not fully resolve
memory addressing and function calls. That's the job of the linker. When
the compiler encounters a function call in a `.cpp` file, it usually has
no idea what the function does, or how it does it. All the compiler need
to know is what parameters are passed and what type the return value is.
The `.obj` code for the function call can be generated, and the linker
will figure out exactly where to make the jump later.

Now keeping all this in mind we can discuss the real topic.

**DECLARATIONS:** A declaration introduces a name into a scope.
Generally speaking, a scope is either an entire `.cpp` file or anything in
code delimited by `{}`, be it a function, a loop within a function, or
even an arbitrarily placed block of `{}` within a function. A name
introduced, is visible within the scope from the point at which it is
declared to the end of that scope. A declarations merely tells the
compiler how to use something, it does not actually create anything.

```cpp
extern int y;
```
> declares `y`, but does not define it. `y` is defined elsewhere,
> but the program can now use it since it knows what it is (an integer)                                              

**PROTOTYPES:** A prototype is just another name for a **declaration** of a function.

```cpp
double someFunction( double, int );
```

**DEFINITIONS:** A definition fully specifies an entity. Definitions are
where the actual creation of the entity in memory takes place. All
definitions are also declarations, but not all declarations are
definitions.

```cpp
Int x;
```
> declares and defines `x`. it is a definition because it creates the variable allocating memory

**IMPLEMENTATIONS:** An implementation is another name for a **definition** of a function. 
That is, the implementation is the actual code of the function itself.

```cpp
double someFunction( double x, int y )
{
    return x * y;
}
```

Any entity can be declared multiple times, but can only be defined once.

### Why all this matters to you

```cpp
int main()
{
    double a = 3.5;
    int b = 2;
    double c;

    c = someFunction(a, b);
}

double someFunction(double x, int y)
{
    return x * y;
}                                                          
```

Recall that compilation is a single pass top-down process. Because of
this, the above code can not work because the compiler gets to the 
`c = someFunction( a, b );` line and doesn't know how to handle
`someFunction()`. The solution is to have `someFunction()` declared before
this.

```cpp
double someFunction(double, int);

int main()
{
    double a = 3.5;
    int b = 2;
    double c;

    c = someFunction(a, b);
}

double someFunction(double x, int y)
{
    return x * y;
}                                                          
```

```cpp
double someFunction(double x, int y)
{
    return x * y;
}

int main()
{
    double a = 3.5;
    int b = 2;
    double c;

    c = someFunction(a, b);
}                                                          
```

Since a definition is also a declaration, either of the above approaches
works. The first uses a prototype, while the second just moved the
definition of `someFunction()` ahead of the call to it in `main()`. As a
general rule, using prototypes is the preferred method as it allows code
to be organized better (you don't have to start at the bottom and work
up as you read it) and prevents errors being introduced if code is
reorganized. Also, consider a set of recursive functions in which each
calls the other.

```cpp
funcA()
{
    if( condition )
        funcB();
    return;
}

funcB()
{
    if( condition )
        funcC();
    return;
}

funcC()
{
    if( condition )
        funcA();
    return;
}
```

This may sound bizarre to new students, but it is rather common in
certain types of algorithms like sorting and grammar parsing. The thing
to note is that there is no way to organize these functions without
having at least one prototype somewhere. So do yourself a favor and get
into the habit of using prototypes.

### A note about `.h` and `.cpp` organization

All of the above relates directly to how you should organize your code
into header files and source files. Most students learning C++ won't be
writing programs large enough to require multiple source files for the
first month or so of their study. But when they do, I've seen a lot of
them get confused about what should be put in which file. The rule of
thumb is this: Header files should contain **declarations**, sourch
files should contain **definitions**. The reason for this should be
fairly clear now. An entity can be declared multiple times, but only
defined once. If a header file contains definitions, you can end up with
the same entity being defined more than once. This will likely cause
problems in the linking process when the linker tries to resolve
external addressing and finds multiple entities with the same name.

> <http://www.cplusplus.com/articles/yAqpX9L8/>

## 6.8 Default Arguments

In C++, functions can also have optional parameters, for which no
arguments are required in the call, in such a way that, for example, a
function with three parameters may be called with only two. For this,
the function shall include a default value for its last parameter, which
is used by the function when called with fewer arguments. For example:

```cpp
//  default values in functions


#include <iostream>

using namespace std;

int divide(int a, int b=2)
{
    int r;
    r = a/b;
    return (r);
}

int main()
{
    cout << divide(12) << '\n';
    cout << divide(20, 4) << '\n';

    return 0;
}
```

Output:

```text
6
5
```

In this example, there are two calls to function divide. In the first
one:

```cpp
divide(12)
```

The call only passes one argument to the function, even though the
function has two parameters. In this case, the function assumes the
second parameter to be `2` (notice the function definition, which declares
its second parameter as `int b=2`). Therefore, the result is `6`.

In the second call:

```cpp
divide(20, 4)
```

The call passes two arguments to the function. Therefore, the default
value for `b` (`int b=2`) is ignored, and b takes the value passed as
argument, that is `4`, yielding a result of `5`.

## 6.9 Inline Functions

In C, we have used Macro function an optimized technique used by
compiler to reduce the execution time etc. So Question comes in mind
that what's there in C++ for that and in what all better ways? Inline
function is introduced which is an optimization technique used by the
compilers especially to reduce the execution time. We will cover "what,
why, when & how" of inline functions.


**What is inline function :**

The inline functions are a C++ enhancement feature to increase the
execution time of a program. Functions can be instructed to compiler to
make them inline so that compiler can replace those function definition
wherever those are being called. Compiler replaces the definition of
inline functions at compile time instead of referring function
definition at runtime.
NOTE- This is just a suggestion to compiler to make the function inline,
if function is big (in term of executable instruction etc) then,
compiler can ignore the "inline" request and treat the function as
normal function.


**How to make function inline:**

To make any function as inline, start its definitions with the keyword "inline".

Example

```cpp
Class A
{
    Public:
        inline int add(int a, int b)
        {
            return(a + b);
        };
}

Class A
{
    Public:
        int add(int a, int b);
};

inline int A::add(int a, int b)
{
    return(a + b);
}
```

**Why to use**

In many places we create the functions for small work/functionality
which contain simple and less number of executable instruction.
Imagine their calling overhead each time they are being called by
callers.
When a normal function call instruction is encountered, the program
stores the memory address of the instructions immediately following
the function call statement, loads the function being called into the
memory, copies argument values, jumps to the memory location of the
called function, executes the function codes, stores the return value
of the function, and then jumps back to the address of the instruction
that was saved just before executing the called function. Too much run
time overhead.
The C++ inline function provides an alternative. With inline keyword,
the compiler replaces the function call statement with the function
code itself (process called expansion) and then compiles the entire
code. Thus, with inline functions, the compiler does not have to jump
to another location to execute the function, and then jump back as the
code of the called function is already available to the calling
program.
With below pros, cons and performance analysis, you will be able to
understand the "why" for inline keyword

**Pros**:

1. It speeds up your program by avoiding function calling overhead.
2. It save overhead of variables push/pop on the stack, when function
calling happens.
3. It save overhead of return call from a function.
4. It increases locality of reference by utilizing instruction cache.
5. By marking it as inline, you can put a function definition in a
header file (i.e. it can be included in multiple compilation unit,
without the linker complaining)

**Cons**

1. It increases the executable size due to code expansion.
2. C++ inlining is resolved at compile time. Which means if you change
the code of the inline function, you will need to recompile all the
code using it to make sure it will be updated\
3. When used in a header, it makes your header file larger with
information which users do not care.
4. As mentioned above it increases the executable size, which may
cause thrashing in memory. More number of page fault bringing down
your program performance.
5. Sometimes not useful for example in embedded system where large
executable size is not preferred at all due to memory constraints.

**When to use**

Function can be made as inline as per programmer need. Some useful
recommendation are mentioned below:

1. Use inline function when performance is needed.
2. Use inline function over macros.
3. Prefer to use inline keyword outside the class with the function 
definition to hide implementation details.

**Key Points**

1. It's just a suggestion not compulsion. Compiler may or may not
inline the functions you marked as inline. It may also decide to
inline functions not marked as inline at compilation or linking time.

2. Inline works like a copy/paste controlled by the compiler, which is
quite different from a pre-processor macro: The macro will be forcibly
inlined, will pollute all the namespaces and code, won't be easy to
debug.

3. All the member function declared and defined within class are
Inline by default. So no need to define explicitly.

4. Virtual methods are not supposed to be inlinable. Still, sometimes,
when the compiler can know for sure the type of the object 
(i.e. the object was declared and constructed inside the same function body),
even a virtual function will be inlined because the compiler knows
exactly the type of the object.

5. Template methods/functions are not always inlined 
(their presence in an header will not make them automatically inline).

6. Most of the compiler would do in-lining for recursive functions but
some compiler provides #pragmas - microsoft c++ compiler - inline_recursion(on) 
and once can also control its limit with inline_depth. 
In gcc, you can also pass this in from the command-line with.-max-inline-insns-recursive.

> <http://www.cplusplus.com/articles/2LywvCM9/>


## 6.10 Local, Global, and Static Local Variables

In this section, we will learn about storage classes in C++.

We initial chapters we saw the declaration of variables, each of those
variables have storage class and type defined explicitly but sometimes
we do not have to explicitly mention the storage class for global and
local variables. Depending on the place they are declared, scope (life)
of the variable is determined. We will see each storage class in detail.

LOCAL VARIABLE:

The variable declared inside the function (inside block of a function)
is called local variable.

The scope of this variable is only inside the function. We cannot access
this variable outside the function definition. The memory allocated to
this variable will be free after the function exit.

Example:
```cpp
#include <iostream>

using namespace std;

void testingvariable();

int main()
{
    // local variable to main() function
    int x = 5;
    testingvariable();
    
    // illegal: var1 not declared inside main()
    y = 9;
}

void testingvariable()
{
    // local variable to testingvariable()
    int y;
    y = 6;

    // illegal: var not declared inside testingvariable()
    cout << x;
}
```

The local variable `x` cannot be used inside `testingvariable()` and local
variable `y` cannot be used inside `main()` function.

GLOBAL VARIABLE:

The variable declared outside all functions is termed as global
variable. The scope of the global variable is throughout the program.
The memory allotted to this variable is cleared once the program
execution complete. We can use this variable any where inside the
program and change its value.

Example:

```cpp
#include <iostream>

using namespace std;

// Global variable declaration
int g = 12;

void testingvariable();

int main()
{
    ++g;

    // Output will be 13 at this point of the program
    cout << g << endl;
    testingvariable();
    
    return 0;
}

void testingvariable()
{
    ++g;

    // Output will be 14 here
    cout << g;
}
```

Output:

```text
13
14
```

Here g can be accessed and updated in both `main()` and `testingvariable()`
functions

STATIC VARIABLE:

The Local variable that is declared with the keyword static is called
STATIC variable. The difference between local variable and static
variable is the life of the variable. In local variable the life of the
variable is till the function exit, but static variable life is till the
program ends but can only be used inside the function. To be more
specific, the memory allotted to the static variable is not cleared
immediately after function exit, but it will be cleared after program
exits.

Example:

```cpp
#include <iostream>

using namespace std;

void testingvariable()
{
    // x is a static variable
    static int x = 0;
    ++x;
    cout << x << endl;
}

int main()
{
    testingvariable();
    testingvariable();

    return 0;
}
```

Output:

```text
1
2
```

In this program, `x` is a static variable inside the `testingvariable`
function which is also a local variable but when the function exits for
the first time the value of the variable is stored in the memory and
when the function is called again it wont take the initialization value
`0` again. It will take the value stored in the memory and prints the
output as `2`.

## Passing Arguments by Reference

To gain access to its arguments, the function declares its parameters
as *references*. In C++, references are indicated with an ampersand (`&`)
following the parameter type, as in the parameters taken by duplicate in
the example above.

When a variable is passed *by reference*, what is passed is no longer a
copy, but the variable itself, the variable identified by the function
parameter, becomes somehow associated with the argument passed to the
function, and any modification on their corresponding local variables
within the function are reflected in the variables passed as arguments
in the call.

![](media/image7.png)

in fact, `a`, `b`, and `c` become aliases of the arguments passed on the
function call (`x`, `y`, and `z`) and any change on a within the function is
actually modifying variable `x` outside the function. Any change
on `b` modifies `y`, and any change on `c` modifies `z`. That is why when, in
the example, function duplicate modifies the values of variables `a`, `b`,
and `c`, the values of `x`, `y`, and `z` are affected.

If instead of defining duplicate as:

```cpp
void duplicate (int& a, int& b, int& c)
```

Was it to be defined without the ampersand signs as:

```cpp
void duplicate (int a, int b, int c)
```

The variables would not be passed *by reference*, but *by value*,
creating instead copies of their values. In this case, the output of the
program would have been the values of `x`, `y`, and `z` without being modified
(i.e., `1`, `3`, and `7`).

> <http://www.cs.uregina.ca/Links/class-info/110/functions/index-ref-008_ggg.html>

## 6.11 Constant Reference Parameters

References used as function parameters can also be const. This allows us
to access the argument without making a copy of it, while guaranteeing
that the function will not change the value being referenced.

```cpp
// ref is a const reference to the argument passed in, not a copy 

void changeN(const int& ref)
{
    ref = 6; // not allowed, ref is const
}
```

References to const values are particularly useful as function
parameters because of their versatility. A const reference parameter
allows you to pass in a non-const l-value argument, a const l-value
argument, a literal, or the result of an expression:

```cpp
#include <iostream>

void printIt(const int& x)
{
    std::cout << x;
}

int main()
{
    int a{ 1 };
    printIt(a); // non-const l-value

    const int b{ 2 };
    printIt(b); // const l-value
    printIt(3); // literal r-value
    printIt(2+b); // expression r-value

    return 0;
}
```

The above prints
```text
1234
```

To avoid making unnecessary, potentially expensive copies, variables
that are not pointers or fundamental data types (`int`, `double`, etc...)
should be generally passed by (`const`) reference. Fundamental data types
should be passed by value, unless the function needs to change them.
There are a few exceptions to this rule, namely types that are so small
that it's faster for the CPU to copy them than having to perform an
extra indirection for a reference.

> <https://www.learncpp.com/cpp-tutorial/6-11a-references-and-const/>


## 6.12 Case Study: Converting Hexadecimals to Decimals

Given with a hexadecimal number as an input, the task is to convert the
given hexadecimal number into a decimal number.

Hexadecimal number in computers is represented with base 16 and decimal
number is represented with base 10 and represented with values `0` - `9`
whereas hexadecimal number have digits starting from `0` -- `15` in which `10`
is represented as `A`, `11` as `B`, `12` as `C`, `13` as `D`, `14` as `E` and `15` as `F`.

To convert a hexadecimal number into a decimal number follow these steps

-   We will extract digits starting from right to left through a
    remainder and then multiply it with the power starting from `0` and
    will be increased by `1` till the (number of digits) -- `1`

-   Since we need to do conversions from `hexdecimal` to binary the base
    of power will be `16` as octal have base `16`.

-   Multiply the digits of given inputs with base and power and store
    the results

-   Add all the multiplied values to obtain the final result which will
    be a decimal number.

Given below is the pictorial representation of converting a hexadecimal
number into a decimal number.

![](../images/chapter_06/Picture5.png)

## Example

Input:
> `A(10)` will be converted to a decimal number by: `10 X 16^2 = 2560`

> `C(12)` will be converted to a decimal number by: `12 X 16^1 = 192`

> `D(13)` will be converted to a decimal number by: `13 X 16^0 = 13`

Output:
```text
total = 13 + 192 + 2560 = 2765
```

## Algorithm

**Start**

Step 1-> declare function to convert hexadecimal to decimal
```cpp
   int convert(char num[])

      Set int len = strlen(num)

      Set int base = 1

      Set int temp = 0

      Loop For int i=len-1 and i>=0 and i---

         IF (num[i]>='0' && num[i]<='9')

            Set temp += (num[i] - 48)*base

            Set base = base * 16

         End

         Else If (num[i]>='A' && num[i]<='F')

            Set temp += (num[i] - 55)*base

            Set base = base*16

         End

         return temp
```
step 2-> In `main()`
```cpp
   declare char num[] = "3F456A"

   Call convert(num)
```
Stop

## Example

[Live Demo](http://tpcg.io/Tpe8cP)
```cpp
#include <iostream>
#include <string.h>

using namespace std;

//convert hexadecimal to decimal

int convert(char num[])
{
    int len = strlen(num);
    int base = 1;
    int temp = 0;

    for(int i=len-1; i>=0; i--)
    {
        if(num[i]>='0' && num[i]<='9')
        {
            temp += (num[i] - 48)*base;
            base = base * 16;
        }
        else if(num[i]>='A' && num[i]<='F')
        {
            temp += (num[i] - 55)*base;
            base = base*16;
        }
    }
    return temp;
}

int main()
{
    char num[] = "3F456A";

    cout << num << " after converting to deciaml becomes :" << convert(num) << endl;

    return 0;
}
```

Output:

IF WE RUN THE ABOVE CODE IT WILL GENERATE FOLLOWING OUTPUT
```
3F456A after converting to deciaml becomes : 4146538
```
> <https://www.tutorialspoint.com/cplusplus-program-for-hexadecimal-to-decimal>


## 6.13 Function Abstraction and Stepwise Refinement

Function Abstraction is a technique used in object-oriented programming
where the function implemented provides only the high-level overview by
hiding the unnecessary details. You will see about this topic in the
advanced learning of C++ journey.

**Stepwise refinement** is the idea that software is developed by moving through 
the levels of abstraction, beginning at higher levels and, incrementally refining 
the software through each level of abstraction, providing more detail at each
increment. At higher levels, the software is merely its design models;
at lower levels there will be some code; at the lowest level, 
the software has been completely developed.

At the early steps of the refinement process the software engineer does
not necessarily know how the software will perform what it needs to do.
This is determined at each successive refinement step, as the design and
the software are elaborated upon.

Refinement be the compliment of abstraction. Abstraction is concerned
with hiding lower levels of detail; it moves from lower to higher
levels. Refinement is the movement from higher levels of detail to lower
levels. Both concepts are necessary in developing software.

> <https://www.cs.uct.ac.za/mit_notes/software/htmls/ch07s09.html>

## 6.14 Chapter Summary

This chapter helps you in writing the modular programming using the
functions where all the necessary topics are covered to declare, define
and call the function inside the program. In the advanced topics you
will learn how to call the functions from the different programs or
files. Pass by value and pass by reference are used to pass the
parameters to the function. We have also seen the storage classes of a
variable and how local, global and static variables scope affects the
values in a program. We will see how we can write a program where we
have multiple values to operate.
