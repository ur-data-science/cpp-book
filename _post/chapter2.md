---
title: Elementary Programming
author: Dr. Alireza Manashty
date: 2021-02-04
category: cpp
layout: post
---

# Elementary Programming

## 2.1 Introduction and Objectives

Let us start our journey in programming with learning some basic concepts. We are going to learn about simple input/output, identifiers, variables, and expressions in this chapter. These are some important tools that will help us to communicate information between a user and our code. We will learn how to get information from the user, how to save that information, how to do some calculation using that information, and eventually, how to let the user know about the result of the calculation. 

## 2.2 Writing a Simple Program

Let's examine the following C++ program.

```cpp
// Author: Ada Lovelace
// Purpose: Demonstrate Basic I/O operation by inputting a number and outputting the number just entered.

#include <iostream>
using namespace std;

int main()
{                                                            
    int number;
    cout << "Please enter a number.";
    cin >> number;
    cout << "You entered: " << number << endl;
    return 0;
}
```

Try it yourself:

<iframe 
    height="500px" 
    width="100%" 
    src="https://repl.it/@Baranerf/Ch21?lite=true" 
    scrolling="no" 
    frameborder="no" 
    allowtransparency="true" 
    allowfullscreen="true" 
    sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals">
</iframe>
<br>


-   The first 6 lines of code is a comment block that gives a brief introduction to the
    C++ program.

-   By convention, every single C++ program should have this kind of
    comment block at the beginning of the program.

-   Usually, a comment that carries over several lines begins with `*`
    and ends with `*`

-   A comment on just one line - or part of the line - begins with `//`

-   Typically, you will see an inline comment at the beginning or end of
    a processing block such as `//` end of program.

-   The next two lines tell the compiler to add **console** input and output
    (`iostream`) features to the program and to make them easier to use by
    adding their namespace into our program. You will probably use these
    in every program this semester.

-   Line 8 is what's known as a **preprocessor command**. The pound (`#`)
    sign followed by `include {:.cpp}` begins every preprocessor command.

-   Any *built-in* or *user-defined* header files you wish to use in your
    program must follow this same syntax.


> **NOTE**: 
>
> Built-in header files are enclosed inside the `<` and `>`
> marks. Header files you create and bring in to the program are enclosed
> in `""` quotation marks.

-   `int main() {:.cpp}` is the executable part of our program. The
    function name is `main`, and it returns a value that is of type
    integer. The function has no parameters, as indicated by the empty
    parentheses.

-   The parentheses `{ }` mark the **beginning** and **end**
    of a group of C++ statements. In this case, they enclose our `main`
    function.

-   `int number;` sets `number` as a variable of type *integer*.

-   `cout` is the command to print text or data **on the screen**.
    Anything that is enclosed in **quotation marks** is to be printed.

-   `cin` - command that receives data from the end user.

-   The `<iostream> {:.cpp}` file exists in every C++ program, and it is
    this file which allows us to use `cout` and cin.

-   The second `cout` line prints out `"You entered: [number]"`. 
    So, if I entered 5, the output would be: `You entered: 5`

-   This kind of way to get data into the program is called a 
    **user interactive input**, and it makes the program become 
    an interactive program.

-   `endl` is *manipulator* to indicate the **end of the line**. It tells the
    cursor to stop printing on the current line, and begin on the next
    line.

-   `return 0; {:.cpp}` - This line is there, since the return value in
    our main program was designated as an integer. Just prevents the
    compiler from reporting a syntax error.

-   `// end program` - a single line comment.

## 2.3 Reading Input from the Keyboard

Imagine we want to write a program to calculate the area of a
rectangle with length of `x` and width of `y`. The first step to calculate
the area is to get the length and width from input. Reading input will
enables you to interact with the user and get the necessary information
for you program.

Here is the table of C++ **basic Input/Output** (I/O) symbols:


| **Symbol**     | **Name**            | **Description**
|------------    |------------         |------------------
| `cout`         | A special variable  | used along with the insertion operator “<<” to write out the values of variables and expressions to the standard output device such as screen.
| `<<`           | Insertion operator  | takes two operands. Its left-hand operand is a stream expression. Its right-hand operand is an expression which could be as simple as a literal string. It can be used several times in a single output statement. 
| `cin`          | A special variable  | used along with the extraction operator “>>” to input values from the standard input device such as keyboard to a variable.                                                                                        
| `>>`           | Extraction operator | takes two operands. Its left-hand operand is a stream expression. Its right-hand operand is a variable into which we store the input data. It can be used several times in a single input statement.               


For instance, for getting `x`{:.cpp} (length) and `y`{:.cpp} (width) from input we could
say:
```cpp
cin >> x;
cin >> y;
```

Also, we could get `x` and `y`in one line:

```cpp
cin >> x >> y;
```



## 2.4 Identifiers

There are two main parts in a C++ program:

1. Instructions to the C++ **preprocessor** and **compiler**.

2. Instructions that describe the processing to be done.

Before we can describe these instructions, we must have a way of naming
things so that we can tell the compiler about them and describe what we
want to do with them. We name things (data types, data objects, and
actions) by giving them an *identifier*.

**Rules of identifiers**:

-   An identifier is made up of **letters**, **numbers**, and **underscore** ( \_ ).

-   An identifier must begin with a letter or an underscore.

-   An identifier should not be a *reserved word*.

For instance, length and \_width1 are legal identifiers, while 1length
and width-4 are not legal.

> **NOTE**: 
> 
> 1. Reserved words are certain words which have predefined meanings within the C++
>    language. Examples of reserved words:
>    `int`, `namespace`, `using`, `include`, `cin`, `cout`, `and`, `return`, etc. 
>    You **cannot** use them as your user defined identifier such as variable names.
>
> 2. C++ is case sensitive. It means length, Length, and LEngTh are all different.


**camelCase**:
Camel case is a naming convention in which the first letter of each word
is uppercase except for the first word. The rest of the letters are
lower case. For example, `payRate`, `camelCase`, and `numberOfYears` are `camelCase`.

![CamelCase](../images/chapter_02/330px-CamelCase_new.svg.png)


## 2.5 Variables

Variables are named memory locations that have a type, such as an
integer or character, and consequently, a size, which is inherited from
their **type**. Since variables are types, they have a set of operations
that can be used to change or manipulate them.

Each variable in your program must be **declared** and **initialized**. There
are two ways in which we can do this.
One is we can declare our variables
first, like this:

```cpp
char letter;
int x;
long student_id;
float payRate;
double pi;
bool valid;
```

Then initialize them later in the program as a separate statement.

```cpp
letter = 'A';
x = 7;
student_id = 200201202;
payRate = 12.85;
pi = 3.1415926536;
valid = true;
```

The other way is to initialize them at the same time as they are
declared (in one statement).

```cpp
char letter = 'A';
int x = 7;
long student_id = 200201202;
double pi = 3.1415926536;
float payRate = 12.85;
bool valid = true;
```

However, a variable can be used only **after its value is set**.


## 2.6 Assignment Statements and Assignment Expressions

You need to know the definition of an **arithmetic expression** and the
**precedence** of the operators.

**Arithmetic Expressions**:
Variables and constants of integral and floating point types can be
combined into expressions using arithmetic operators.


## 2.7 Named Constants

We can also declare our initialized variable as a *constant*, by adding
the type qualifier `const` before the definition. The general format for a
const declaration is shown below:

`const type variable-name = any value you like`

Inside of a program, you will see constants written like this:

```cpp
const float payRate = 12.85;
const double pi = 3.1415926536;
```



## 2.8 Numeric Data Types and Operations

A *data type* is a set of values and a set of operations on these values.
In the preceding program, we used the data type `int` which is an
identifier for the integer data type.

We used data type `int` in four ways in the preceding program. `int`
precedes `main`, the name of the main function in the program to indicate
that the function returns the value of type `int`. At the end an `int`
literal (zero) is returned as the result of the main function `main`. Also, in the middle of the program a variable number is declared to have the data type `int`. In addition, an integer number was read from the keyboard and stored in the
storage of variable number.

The following are some fundamental/simple data types:


 Integral Types                                             
------------------------------------------------------------
 `short`           `int`              `long`           `char `         
 `unsigned short`  `unsigned int`       `unsigned long`  `unsigned char` 


 Floating Types                             
--------------------------------------------
 `float`           `double `    `long double`      


The arithmetic operators are listed in the following table:                                                 

| Operator     | Description                                                                     
|-----------   |----------------
| `+`          | **Unary plus** needs one operand.                                                   
| `-`          | **Unary minus** needs one operand.                                                  
| `+`          | **Addition** needs two operands.                                                    
| `-`          | **Subtraction** needs two operands.                                                 
| `\`          | **Multiplication** needs two operands.                                              
| `/`          | **Division** needs two operands. <br>Floating point operands &rightarrow; floating point result <br> Integer operands &rightarrow; integer quotient <br>  Mixed operands &rightarrow; floating point result                                              
| `%`          | **Modulus**  <br> Remainder from integer division <br>   Operands must be integral                                                                    
| `++`         | **Increment by one** <br> Can be prefix or postfix <br> As postfix has highest precedence                                                          
| `--`         | **Decrement by one** <br> Can be prefix or postfix <br> As postfix has highest precedence                                                          




## 2.9 Evaluating Expressions and Operator Precedence

The precedence rules of arithmetic apply to arithmetic expressions in a
program. That is, the order of execution of an expression that contains
more than one operation is determined by the precedence rules of
arithmetic. These rules state that parentheses have the highest
precedence, multiplication, division, and modulus have the next highest
precedence, and addition and subtraction have the lowest. The Postfix
increment and decrement operators have the highest precedence over any
of the arithmetic operators.

Look at the following example, and decide what is written by each of the
output statements.

```cpp
// The program demonstrates the precedence of the operators.


#include <iostream>
using namespace std;

int main ()
{
    cout << 4 + 3 * 5 << endl;
    cout << (4 + 3) * 5 << endl;
    cout << 4 * 5 % 3 + 2 << endl;
    cout << (4 * (5 % 3) + 2) << endl;
    return 0;
}
```

Output:

```text
19
35
4
10
```

Try it yourself:


<iframe 
    height="400px" 
    width="100%" 
    src="https://repl.it/@Baranerf/Ch22?lite=true" 
    scrolling="no" 
    frameborder="no" 
    allowtransparency="true" 
    allowfullscreen="true" 
    sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals">
</iframe>
<br>


| **Precedence** | **Operator**          | **Description**                                            | **Associativity** 
|----------------|-----------------------|------------------------------------------------------------|-------------------
|     1          | `::`                  |  Scope resolution                                          |  Left-to-right 
|     2          | `a++`, `a--`          |  Suffix/postfix increment and decrement                    |                                   
|     3          | `++a`, `--a`          |  Prefix increment and decrement                            |  Right-to-left 
|                | `+a`, `-a`            |  Unary plus and minus                                      |                               
|                | `*a`                  |  Indirection (dereference)                                 |                  
|                | `&a`                  |  Address-of                                                |                  
|     4          | `.*`, `->*`           |  Pointer-to-member                                         |  Left-to-right 
|     5          | `a*b`, `a/b`, `a%b`   |  Multiplication, division, and remainder                   |                  
|     6          | `a+b`, `a-b`          |  Addition and subtraction                                  |                  
|     7          | `<<`, `>>`            |  Bitwise left shift and right shift                        |                  
|     8          | `<=>`                 |  Three-way comparison operator (since C++20)               |                  
|     9          | `<`, `<=`             |  For relational operators < and ≤ respectively             |                  
|                | `>`, `>=`             |  For relational operators > and ≥ respectively             |                  
|     10         | `==`, `!=`            |  For relational operators = and ≠ respectively             |                  
|     11         | `&`                   |  Bitwise AND                                               |                  
|     12         | `^`                   |  Bitwise XOR (exclusive or)                                |                  
|     13         | `\`                   |  Bitwise OR (inclusive or)                                 |                  
|     14         | `&&`                  |  Logical AND                                               |                  
|     15         | `^`                   |  Logical OR                                                |                  
|     16         | `a?b:c`               |  Ternary conditional[note 2]                               |  Right-to-left             
|                | `=`                   |  Direct assignment (provided by default for C++ classes)   |                  
|                | `+=`, `-=`            |  Compound assignment by sum and difference                 |                  
|                | `*=`, `/=`, `%=`      |  Compound assignment by product, quotient, and remainder   |                      
|     17         | `,`                   |  Comma                                                     |  Left-to-right 


## 2.10 Augmented Assignment Operators

Assignment operators **modify** the value of the object.

| Operator name                    | Syntax     | Over​load​able  |
|----------------                  |--------    |-------------- |
| simple assignment                | `a = b`    | Yes           |
| addition assignment              | `a += b`   | Yes           |
| subtraction assignment           | `a -= b`   | Yes           |
| multiplication assignment        | `a *= b`   | Yes           |
| division assignment              | `a /= b`   | Yes           |
| modulo assignment                | `a %= b`   | Yes           |
| bitwise AND assignment           | `a &= b`   | Yes           |   
| bitwise OR assignment            | `a \= b`   | Yes           |
| bitwise XOR assignment           | `a ^= b`   | Yes           |
| bitwise left shift assignment    | `a <<= b`  | Yes           | 
| bitwise right shift assignment   | `a >>= b`  | Yes           |


> Examples are **Inside class definition** and **Outside class definition** respectively.
<!---
> **NOTE**: 
>
> All built-in assignment operators return *this, and most user-defined overloads also return *this 
> so that the user-defined operators can be used in the same manner as the built-ins. 
> However, in a user-defined operator overload, any type can be used as return type (including void).
> `T2` can be any type including `T`.
--->

### Explanation

**copy assignment** operator replaces the contents of the object a with a
copy of the contents of `b` (`b` is not modified). For class types, this is
a special member function, described in copy assignment operator.

**move assignment** operator replaces the contents of the object a with the
contents of b, avoiding copying if possible (b may be modified). For
class types, this is a special member function, described in move
assignment operator. (since C++11)

For non-class types, copy and move assignment are indistinguishable and
are referred to as **direct assignment**.

**compound assignment** operators replace the contents of the object a with
the result of a binary operation between the previous value of a and the
value of b.

<!---
Builtin direct assignment

The direct assignment expressions have the form

```cpp
lhs = rhs (1)

lhs = {} (2) (since C++11)

lhs = { rhs } (3) (since C++11)
```

For the built-in operator, lhs may have any non-const scalar type and
rhs must be implicitly convertible to the type of lhs.

The direct assignment operator expects a modifiable lvalue as its left
operand and an rvalue expression or a braced-init-list (since C++11) as
its right operand, and returns an lvalue identifying the left operand
after modification.

For non-class types, the right operand is first implicitly converted to
the cv-unqualified type of the left operand, and then its value is
copied into the object identified by left operand.

When the left operand has reference type, the assignment operator
modifies the referred-to object.

If the left and the right operands identify overlapping objects, the
behavior is undefined (unless the overlap is exact and the type is the
same)

If the right operand is a braced-init-list

if the expression `E1` has scalar type,

the expression `E1 = {}` is equivalent to `E1 = T{}`, where `T` is the type of
`E1`.

the expression `E1 = {E2}` is equivalent to `E1 = T{E2}`, where `T` is the
type of `E1`.

if the expression `E1` has class type, the syntax `E1 = {args...}`
generates a call to the assignment operator with the braced-init-list as
the argument, which then selects the appropriate assignment operator
following the rules of overload resolution. Note that, if a non-template
assignment operator from some non-class type is available, it is
preferred over the copy/move assignment in `E1 = {}` because `{}` to
non-class is an identity conversion, which outranks the user-defined
conversion from `{}` to a `class` type. (since C++11)

Using an lvalue of volatile-qualified non-class type as left operand of
built-in direct assignment operator is deprecated, unless the assignment
expression appears in an unevaluated context or is a discarded-value
expression. (since C++20)

In overload resolution against user-defined operators, for every type `T`,
the following function signatures participate in overload resolution:

```cpp
T*& operator=(T*&, T*);

T*volatile & operator=(T*volatile &, T*);
```

For every enumeration or pointer to member type `T`, optionally
volatile-qualified, the following function signature participates in
overload resolution:

```cpp
T& operator=(T&, T );
```

For every pair `A1` and `A2`, where `A1` is an arithmetic type (optionally
volatile-qualified) and `A2` is a promoted arithmetic type, the following
function signature participates in overload resolution:

```cpp
A1& operator=(A1&, A2);
```

```cpp
#include <iostream>

using namespace std;

int main()
{
    int n = 0; // not an assignment
    n = 1; // direct assignment
    cout<< n << ' ';
    n = {}; // zero-initialization, then assignment
    cout<< n <<' ';
    n = 'a';       // integral promotion, then assignment
    cout<< n << ' ';
    n = {'b'}; // explicit cast, then assignment
    cout<< n << ' ';
    n = 1.0; // floating-point conversion, then assignment
    cout<< n << ' ';
    // n = {1.0}; // compiler error (narrowing conversion)
    int& r = n; // not an assignment
    int* p;
    r = 2; // assignment through reference
    cout << n <<'\n';
    p = &n; // direct assignment
    p = nullptr; // null-pointer conversion, then assignment
    struct {int a; string s;} obj;
    obj = {1, "abc"}; // assignment from a braced-init-list
    cout<< obj.a << ' ' << obj.s <<'\n';
}
```

Output:

```text
1 0 97 98 1 2
1 abc
```

Try it yourself:

<iframe 
    height="700px" 
    width="700px" 
    src="https://repl.it/@DataScienceLab/2-10#main.cpp?lite=true" 
    scrolling="yes" 
    frameborder="no" 
    allowtransparency="true" 
    allowfullscreen="true" 
    sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin">
</iframe>
<br>
--->

## 2.11 Increment and Decrement Operators

Increment/decrement operators increment or decrement the value of the object.

| **Operator name**   | Syntax     | Over​load​able|                           
|-------------------  |---------   |-------------|
| pre-increment       | `++a`      | Yes         |     
| pre-decrement       | `--a`      | Yes         |
| post-increment      | `a++`      | Yes         |
| post-decrement      | `a--`      | Yes         |


### **Explanation**
Pre-increment and pre-decrement operators increments or decrements the
value of the object and returns a reference to the result.

Post-increment and post-decrement creates a copy of the object,
increments or decrements the value of the object and returns the copy
from before the increment or decrement.

Built-in prefix operators

The prefix increment and decrement expressions have the form

`++ expr`: prefix increment (pre-increment)

`-- expr`: prefix decrement (pre-decrement)


The operand ``expr`` of a built-in prefix increment or decrement operator
must be a modifiable (non-const) value of non-boolean (since C++17)
arithmetic type or pointer to completely-defined object type. For
non-boolean operands, the expression `++x` is exactly equivalent to `x += 1`, 
and the expression. `-x` is exactly equivalent to `x -= 1`, that is, the
prefix increment or decrement is an lvalue expression that identifies
the modified operand. All arithmetic conversion rules and pointer
arithmetic rules defined for arithmetic operators apply and determine
the implicit conversion (if any) applied to the operand as well as the
return type of the expression.

```cpp
#include <iostream>

using namespace std;

int main()
{
    int n1 = 1;
    int n2 = ++n1;
    int n3 = ++ ++n1;
    int n4 = n1++;
    // int n5 = n1++ ++; // error
    // int n6 = n1 + ++n1; // undefined behavior
    cout << "n1 = " << n1 << '\n' << "n2 = " << n2 << '\n' << "n3 = " << n3 << '\n' << "n4 = " << n4 << '\n';
}
```

Output:

```text
n1 = 5
n2 = 2
n3 = 4
n4 = 4
```

Try it Yourself:

<iframe 
    height="400px"
    width="100%" 
    src="https://repl.it/@Baranerf/Ch23?lite=true" 
    scrolling="no" 
    frameborder="no" 
    allowtransparency="true" 
    allowfullscreen="true" 
    sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals">
</iframe>
<br>



## 2.12 Numeric Type Conversions

If an integral and a floating point variable or constant are mixed in an
operation, the integral value is changed *temporarily* to its equivalent
floating point representation before the operation is executed. This
automatic conversion of an integral value to a floating point value is
called **type coercion**. Type coercion also occurs when a floating point
value is assigned to an integral variable. Coercion from an integer to a
floating point is exact. However, when a floating point value is coerced
into an integral value, the fractional part is **truncated**.

Type changes can be made explicit by placing the value to be changed in
parentheses and placing the name of the new type before it. This is
called *type casting* or *type conversion*. For example, `intValue = 10.66;` and `intValue = int(10.66);` produce the same result `10`.

In summary, we have *explicit* and *implicit* data type conversion.

- **Type coercion** The **implicit** (automatic) conversion of a value from one data type to another.

- **Type casting** The **explicit** conversion of a value from one data type to another; also called *type conversion*.



Conversion function is declared like a non-static member function or
member function template with no parameters, no explicit return type,
and with the name of the form:


> operator conversion-type-id **(1)**

> explicit operator conversion-type-id **(2)** (since C++11)

> explicit ( expression ) operator conversion-type-id **(3)** (since C++20)


1. Declares a user-defined conversion function that participates in **all implicit and explicit** conversions.

2. Declares a user-defined conversion function that participates in **direct-initialization and explicit** conversions only.

3. Declares a user-defined conversion function that is **conditionally explicit**.

<!---
*conversion-type-id* is a *type-id* except that function and array operators
`[]` or `()` are **not allowed** in its declarator (thus conversion to types
such as pointer to array requires a type alias/typedef or an identity
template). Regardless of typedef, conversion-type-id cannot
represent an array  a function ortype.


Although the return type is not allowed in the declaration of a
user-defined conversion function, the decl-specifier-seq of the
declaration grammar may be present and may include any specifier other
than type-specifier or the keyword static, In particular, besides
explicit, the specifiers inline, virtual, constexpr (since C++11),
const eval (since C++20), and friend are also allowed 
(note that friend requires a qualified name: `friend A::operator B();`).

When such member function is declared in class `X`, it performs conversion
from `X` to conversion-type-id:


```cpp
struct X {
    // implicit conversion
    operator int() const { return 7; }
 
    // explicit conversion
    explicit operator int*() const { return nullptr; }
 
    // Error: array operator not allowed in conversion-type-id
    // operator int(*)[3]() const { return nullptr; }
    using arr_t = int[3];
    operator arr_t*() const { return nullptr; } // OK if done through typedef
    // operator arr_t () const; // Error: conversion to array not allowed in any case
};
 
int main()
{
    X x;
 
    int n = static_cast<int>(x);   // OK: sets n to 7
    int m = x;                     // OK: sets m to 7
 
    int* p = static_cast<int*>(x);  // OK: sets p to null
//  int* q = x; // Error: no implicit conversion
 
    int (*pa)[3] = x;  // OK
}
```

**Explanation**
User-defined conversion function is invoked on the second stage of the
implicit conversion, which consists of zero or one converting
constructor or zero or one user-defined conversion function.

If both conversion functions and converting constructors can be used to
perform some user-defined conversion, the conversion functions and
constructors are both considered by overload resolution in
copy-initialization and reference-initialization contexts, but only the
constructors are considered in direct-initialization contexts.

```cpp
struct To {
    To() = default;
    
    To(const struct From&) {} // converting constructor
};

struct From {
    operator To() const {return To();} // conversion function
};

int main()
{
    From f;
    To t1(f); // direct-initialization: calls the constructor

    /*
        note, if converting constructor is not available, implicit copy constructor
        will be selected, and conversion function will be called to prepare its argument
    */

    To t2 = f; // copy-initialization: ambiguous

    // note, if conversion function is from a non-const type, e.g.

    // From::operator To();, it will be selected instead of the ctor in this case)

    To t3 = static_cast<To>(f); // direct-initialization: calls the constructor

    const To& r = f; // reference-initialization: ambiguous
}
```

Conversion function to its own (possibly cv-qualified) class (or to a
reference to it), to the base of its own class (or to a reference to
it), and to the type void can be defined, but can not be executed as
part of the conversion sequence, except, in some cases, through virtual
dispatch:

```cpp
struct D;

struct B {
    virtual operator D() = 0;
};

struct D : B
{
    operator D() override { return D(); }
};

int main()
{
    D obj;
    D obj2 = obj; // does not call D::operator D()
    B& br = obj;
    D obj3 = br; // calls D::operator D() through virtual dispatch
}
```

It can also be called using member function call syntax:

```cpp
struct B {};

struct X : B {
    operator B&() { return *this; };
};

int main()
{
    X x;
    B& b1 = x; // does not call X::operatorB&()
    B& b2 = static_cast<B&>(x); // does not call X::operatorB&
    B& b3 = x.operator B&(); // calls X::operatorB&
}
```
--->
## 2.13 Software Development Process

In software engineering, a software development process is the process
of dividing software development work into distinct phases to **improve
design**, **product management**, and **project management**. It is also known as
a **software development life cycle** (SDLC). The methodology may include
the pre-definition of specific deliverables and artifacts that are
created and completed by a project team to develop or maintain an
application.

Most modern development processes can be vaguely described as agile.
Other methodologies include waterfall, prototyping, iterative and
incremental development, spiral development, rapid application
development, and extreme programming.

A life-cycle "model" is sometimes considered a more general term for a
category of methodologies and a software development "process" a more
specific term to refer to a specific process chosen by a specific
organization.[citation needed] For example, there are many specific
software development processes that fit the spiral life-cycle model. The
field is often considered a subset of the systems development life
cycle.


## 2.14 Common Errors

-   **TypeError**: Type conversion

-   **ValueError**: Trying to change the value of a constant variable

-   **LogicalError**: Lack of using parentheses and getting the wrong Boolean expression

-   **SyntaxError**: Forgetting `;` at the end of the lines that is needed

-   **VariableError**: Inappropriate variable initialization


## 2.15 Chapter Summary

All in all, now we know how a simple C++ program looks like. Also, we
know how to declare variables, get them from user, and how to write
expressions using them and operators.

<hr>

## References
- <http://www.cs.uregina.ca>
- <https://en.wikipedia.org/wiki/Camel_case>
- <http://www.cplusplus.com/doc/tutorial/constants/>
- <https://en.cppreference.com/w/cpp/language/operator_precedence>
- <https://en.cppreference.com/w/cpp/language/cast_operator>
- <https://en.cppreference.com/w/cpp/language/operator_incdec>
- <http://www.cplusplus.com/doc/tutorial/operators/>
- <https://en.wikipedia.org/wiki/Software_development_process>
