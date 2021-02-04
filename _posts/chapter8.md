---
title: Advance Topics
author: Dr. Alireza Manashty
date: 2021-02-04
category: cpp
layout: post
---

# Advance Topics

## 8.1 Introduction and Objectives
From chapter 1-7, you have learned the basics of the programming which will give you basic intuition on how programming logics are written using various concepts. In this chapter, you will learn some advanced topics like 2D arrays, object oriented programming concepts etc. This is to get you an understanding of real world problems we solve using programming. So, Lets start with 2D arrays.

> <http://www.cplusplus.com/articles/NAUq5Di1/>

## 8.2 Declaring Two-Dimensional Arrays

**Vector based multi-dimensional arrays**- Vectors are a STL container
that allow you to store pretty much anything in them. When used
correctly they can be very powerful containers.
They provide an added benefit that they will automatically remove the
memory they use when they go out of scope. This means that objects
stored within a vector do not need to be de-allocated (but pointers to
objects do).
You can also do some interesting things with dynamic multi-dimensional
arrays with vectors. For example, if you only allocate the first
dimension, then use the `.push_back()` to add records to the 2nd dimension
it's no longer a grid, but an array with a dynamically sized 2nd
dimension (much like a street of buildings each with a different amount
of floors). This functionality can be achieved using pointers, but is
much harder to do.

A simple 2D Array with vectors:

```cpp
#include <vector>
using std::vector;

#define HEIGHT 5
#define WIDTH 3

int main()
{
    vector<vector<double> > array2D;

    // Set up sizes. (HEIGHT x WIDTH)
    array2D.resize(HEIGHT);
    for (int i = 0; i < HEIGHT; ++i)
        array2D<i>.resize(WIDTH);

    // Put some values in
    array2D[1][2] = 6.0;
    array2D[3][1] = 5.5;
    return 0;
}
```

**Pointer based multi-dimensional arrays** Pointer based
multi-dimensional arrays provide you with a more raw access to the
objects. The benefits can be added speed and you can apply custom
optimizations to them.

Note: There are ways you can optimize this by combining the 2 dimensions
into a single dimension `(HEIGHTxWIDTH)`. I leave the discussion of this
out, as it's a more advanced topic for people already familiar with
this topic.

A simple 2D Array:

```cpp
#define HEIGHT 5
#define WIDTH 3   

int main()
{
    double **p2DArray;
    // Allocate memory
    p2DArray = new double*[HEIGHT];
    for (int i = 0; i < HEIGHT; ++i)
    {
        p2DArray<i> = new double[WIDTH];
    }
    // Assign values
    p2DArray[0][0] = 3.6;
    p2DArray[1][2] = 4.0;
    // De-Allocate memory to prevent memory leak
    for (int i = 0; i < HEIGHT; ++i)
    {
        delete [] p2DArray<i>;
    }
    delete [] p2DArray;
    return 0;
}
```

## **8.3 Processing Two-Dimensional Arrays**

## **8.4 Passing Two-Dimensional Arrays to Functions**

You can pass them by pointer.

e.g

```cpp
void doSomethingWith2D(double **Array); or
voud doSomethingWith2D(vector<vector<double> > &Array);
```

## **8.5 Multidimensional Arrays**

A 3D Array with vectors.

```cpp
#include <vector>
using std::vector;

#define HEIGHT 5
#define WIDTH 3
#define DEPTH 7

int main()
{
    vector<vector<vector<double> > > array3D;                                                 
    // Set up sizes. (HEIGHT x WIDTH)
    array3D.resize(HEIGHT);
    for (int i = 0; i < HEIGHT; ++i)
    {
        array3D<i>.resize(WIDTH);

        for (int j = 0; j < WIDTH; ++j)
        {
            array3D<i>[j].resize(DEPTH);
        }
    }  // Put some values in
    array3D[1][2][5] = 6.0;
    array3D[3][1][4] = 5.5;
    return 0;
}
```

A 3D Array with pointer:

```cpp
#define HEIGHT 5
#define WIDTH 3
#define DEPTH 7

int main()
{
    double ***p2DArray;                           
    // Allocate memory
    p2DArray = new double**[HEIGHT];
                                                                              
    for (int i = 0; i < HEIGHT; ++i)
    {
        p2DArray<i> = new double*[WIDTH];
        for (int j = 0; j < WIDTH; ++j)
            p2DArray<i>[j] = new double[DEPTH];
    }

    // Assign values
    p2DArray[0][0][0] =3.6;
    p2DArray[1][2][4] =4.0;
                                                             
    // De-Allocate memory to prevent memory leak
    for (int i = 0; i < HEIGHT; ++i)
    {
        for (int j = 0; j < WIDTH;++j)
        {
            delete [] p2DArray<i>[j];
        }                                                         
        delete [] p2DArray<i>;
    }
    delete [] p2DArray;
    return 0;
}
```

## **8.6 Defining Classes for Objects**

*Classes* are an expanded concept of *data structures*: like data
structures, they can contain data members, but they can also contain
functions as members.

An *object* is an instantiation of a class. In terms of variables, a
class would be the type, and an object would be the variable.

Classes are defined using either keyword `class` or keyword `struct`, with
the following syntax:

```cpp
class class_name
{
    access_specifier_1:member1;            
                     
    access_specifier_2:member2;            
                   
    ...

} object_names;     
```

Where `class_name` is a valid identifier for the class, `object_names` is an
optional list of names for objects of this class. The body of the
declaration can contain *members*, which can either be data or function
declarations, and optionally *access specifiers*.

Classes have the same format as plain *data structures*, except that
they can also include functions and have these new things called *access
specifiers*. An *access specifier* is one of the following three
keywords: `private`, `public` or `protected`. These specifiers modify the
access rights for the members that follow them:

-   `private` members of a class are accessible only from within other
    members of the same class (or from their *"friends"*).

-   `protected` members are accessible from other members of the same
    class (or from their *"friends"*), but also from members of their
    derived classes.

-   Finally, `public` members are accessible from anywhere where the
    object is visible.

By default, all members of a class declared with the `class` keyword have
private access for all its members. Therefore, any member that is
declared before any other *access specifier* has private access
automatically. For example:

```cpp
class Rectangle
{
    int width, height;

    public:
        void set_values (int,int);
        int area (void);
} rect;                       
```

Declares a class (i.e., a type) called `Rectangle` and an object (i.e., a
variable) of this class, called `rect`. This class contains four members:
two data members of type *int* (member `width` and member `height`)
with *private access* (because private is the default access level) and
two member functions with *public access*: the
functions *set_values* and *area*, of which for now we have only included
their declaration, but not their definition.

Notice the difference between the *class name* and the *object name*: In
the previous example, `Rectangle` was the *class name* (i.e., the type),
whereas `rect` was an object of type Rectangle. It is the same
relationship *int* and a have in the following declaration:

```cpp
int a;
```

where *int* is the type name (the class) and *a* is the variable name (the
object).

After the declarations of *Rectangle* and *rect*, any of the public members
of object *rect* can be accessed as if they were normal functions or
normal variables, by simply inserting a `dot(.)` between *object
name* and *member name*. This follows the same syntax as accessing the
members of plain data structures. For example:

```cpp
rect.set_values(3,4);
myarea = rect.area();     
```

The only members of `rect` that cannot be accessed from outside the class
are `width` and `height`, since they have private access and they can only
be referred to from within other members of that same class.

Here is the complete example of class Rectangle:

```cpp
// classes example


#include <iostream>

using namespace std;

class Rectangle
{
    int width, height;                                       
                                                           
    public:
        void set_values (int, int);
        int area()
        {
            return width*height;
        }
};

void  Rectangle::set_values (int x, int y)
{
    width = x;
    height = y;
}

int main()
{
    Rectangle rect;
    rect.set_values(3, 4);
    cout << "area: " << rect.area();
    return 0;                                                  
}
```

Output: 

```text
area: 12 
```
This example reintroduces the *scope operator* (::, two colons), seen in
earlier chapters in relation to namespaces. Here it is used in the
definition of function ```set_values``` to define a member of a class outside
the class itself.

Notice that the definition of the member function area has been included
directly within the definition of class Rectangle given its extreme
simplicity. Conversely, set_values it is merely declared with its
prototype within the class, but its definition is outside it. In this
outside definition, the operator of scope (::) is used to specify that
the function being defined is a member of the class Rectangle and not a
regular non-member function.

The scope operator (::) specifies the class to which the member being
defined belongs, granting exactly the same scope properties as if this
function definition was directly included within the class definition.
For example, the function set_values in the previous example has access
to the variables width and height, which are private members of
class Rectangle, and thus only accessible from other members of the
class, such as this.

The only difference between defining a member function completely within
the class definition or to just include its declaration in the function
and define it later outside the class, is that in the first case the
function is automatically considered an *inline* member function by the
compiler, while in the second it is a normal (not-inline) class member
function. This causes no differences in behavior, but only on possible
compiler optimizations.

Members width and height have private access (remember that if nothing
else is specified, all members of a class defined with
keyword class have private access). By declaring them private, access
from outside the class is not allowed. This makes sense, since we have
already defined a member function to set values for those members within
the object: the member function set_values. Therefore, the rest of the
program does not need to have direct access to them. Perhaps in a so
simple example as this, it is difficult to see how restricting access to
these variables may be useful, but in greater projects it may be very
important that values cannot be modified in an unexpected way
(unexpected from the point of view of the object).

The most important property of a class is that it is a type, and as
such, we can declare multiple objects of it. For example, following with
the previous example of class Rectangle, we could have declared the
object `rectb` in addition to object `rect`:

```cpp
// example: one class, two objects


#include<iostream>                                         

using namespace std;                                                 

class Rectangle
{
    int width,height;                                              

    public:
        void set_values(int,int);                                           
        int area ()
        {
            return width*height;
        }                                              
};

void Rectangle::set_values(int x, int y)
{
    width = x;
    height = y;
}

int main()
{
    Rectangle rect, rectb;                                               
    rect.set_values (3,4);                                               
    rectb.set_values (5,6);                                               
    
    cout << "rect area: " << rect.area() << endl;
    cout << "rectb area: " << rectb.area()
    return 0;                                                                                               
}
```

Output:

```text                                                
rect area: 12
rectb area: 30
```
In this particular case, the class (type of the objects) is Rectangle,
of which there are two instances (i.e., objects): rect and rectb. Each
one of them has its own member variables and member functions.

Notice that the call to `rect.area()` does not give the same result as the
call to `rectb.area()`. This is because each object of class Rectangle has
its own variables width and height, as they -in some way- have also
their own function members set_value and area that operate on the
object's own member variables.

Classes allow programming using object-oriented paradigms: Data and
functions are both members of the object, reducing the need to pass and
carry handlers or other state variables as arguments to functions,
because they are part of the object whose member is called. Notice that
no arguments were passed on the calls to `rect.area` or `rectb.area`. Those
member functions directly used the data members of their respective
objects `rect` and `rectb`.

> <http://www.cplusplus.com/doc/tutorial/classes/>

## **8.7 Constructing and Using Objects**

### **8.7.1 Constructors**

What would happen in the previous example if we called the member
function area before having called set_values? An undetermined result,
since the members width and height had never been assigned a value.

In order to avoid that, a class can include a special function called
its *constructor*, which is automatically called whenever a new object
of this class is created, allowing the class to initialize member
variables or allocate storage.

This constructor function is declared just like a regular member
function, but with a name that matches the class name and without any
return type; not even void.

The Rectangle class above can easily be improved by implementing a
constructor:

```cpp
// example: class constructor


#include <iostream>

using namespace std;

class Rectangle
{
    int width, height;
    
    public:
        Rectangle (int,int);
        int area () {return (width*height);}
};

Rectangle::Rectangle (int a, int b) {
  width = a;
  height = b;
}

int main () {
  Rectangle rect (3,4);
  Rectangle rectb (5,6);
  cout << "rect area: " << rect.area() << endl;
  cout << "rectb area: " << rectb.area() << endl;
  return 0;
}
```

Output:
                                   
```text
rect area: 12
rectb area: 30  
```

The results of this example are identical to those of the previous
example. But now, class Rectangle has no member function set_values, and
has instead a constructor that performs a similar action: it initializes
the values of width and height with the arguments passed to it.

Notice how these arguments are passed to the constructor at the moment
at which the objects of this class are created:

```cpp
Rectangle rect (3,4);
Rectangle rectb (5,6);    
```

Constructors cannot be called explicitly as if they were regular member
functions. They are only executed once, when a new object of that class
is created.

Notice how neither the constructor prototype declaration (within the
class) nor the latter constructor definition, have return values; not
even void: Constructors never return values, they simply initialize the
object.

### **8.7.2 Overloading constructors**

Like any other function, a constructor can also be overloaded with
different versions taking different parameters: with a different number
of parameters and/or parameters of different types. The compiler will
automatically call the one whose parameters match the arguments:

```cpp
// overloading class constructors


#include <iostream>

using namespace std;

class Rectangle
{
    int width, height;

    public:
        Rectangle ();
        Rectangle (int,int);
        int area (void) {return (width*height);}
};

Rectangle::Rectangle()
{
    width = 5;
    height = 5;
}

Rectangle::Rectangle(int a, int b)
{
    width = a;
    height = b;
}

int main()
{
    Rectangle rect (3,4);
    Rectangle rectb;
    cout << "rect area: " << rect.area() << endl;
    cout << "rectb area: " << rectb.area() << endl;
    return 0;
}
```

Output:

```text
rect area: 12
rectb area: 25  
```

In the above example, two objects of class Rectangle are
constructed: rect and rectb. rect is constructed with two arguments,
like in the example before.

But this example also introduces a special kind constructor:
the *default constructor*. The `default constructor` is the constructor
that takes no parameters, and it is special because it is called when an
object is declared but is not initialized with any arguments. In the
example above, the *default constructor* is called for *rectb*. Note
how *rectb* is not even constructed with an empty set of parentheses - in
fact, empty parentheses cannot be used to call the default constructor:

```cpp
Rectangle rectb;   // ok, default constructor called
Rectangle rectc(); // oops, default constructor NOT called   
```

This is because the empty set of parentheses would make of `rectc` a
function declaration instead of an object declaration: It would be a
function that takes no arguments and returns a value of type Rectangle.

### **8.7.3 Uniform initialization**

The way of calling constructors by enclosing their arguments in
parentheses, as shown above, is known as `functional form`. But
constructors can also be called with other syntaxes:

First, constructors with a single parameter can be called using the
variable initialization syntax (an equal sign followed by the
argument):

```cpp
class_name object_name = initialization_value;
```

More recently, C++ introduced the possibility of constructors to be
called using *uniform initialization*, which essentially is the same as
the functional form, but using braces (`{}`) instead of parentheses (`()`):

```cpp
class_name object_name { value, value, value, ... }
```

Optionally, this last syntax can include an equal sign before the
braces.

Here is an example with four ways to construct objects of a class whose
constructor takes a single parameter:

```cpp
// classes and uniform initialization


#include <iostream>

using namespace std;

class Circle 
{
    double radius;

    public:
        Circle(double r) { radius = r; }
        double circum() {return 2*radius*3.14159265;}
};

int main()
{
    Circle foo (10.0);   // functional form
    Circle bar = 20.0;   // assignment init.
    Circle baz {30.0};   // uniform init.
    Circle qux = {40.0}; // POD-like

    cout << "foo's circumference: " << foo.circum() << '\n';
    return 0;
}
```

output:

```text
foo's circumference: 62.8319
```

An advantage of uniform initialization over functional form is that,
unlike parentheses, braces cannot be confused with function
declarations, and thus can be used to explicitly call default
constructors:

```cpp
Rectangle rectb; // default constructor called 3
Rectangle rectc(); // function declaration (default constructor called)
Rectangle rectd{}; // default constructor called             
```

The choice of syntax to call constructors is largely a matter of style.
Most existing code currently uses functional form, and some newer style
guides suggest to choose uniform initialization over the others, even
though it also has its potential pitfalls for its preference
of [initializer_list](http://www.cplusplus.com/initializer_list) as its
type.

### **8.7.4 Member initialization in constructors**

When a constructor is used to initialize other members, these other
members can be initialized directly, without resorting to statements in
its body. This is done by inserting, before the constructor's body, a
`colon (:)` and a list of initializations for class members. For example,
consider a class with the following declaration:

```cpp
class Rectangle
{
    int width, height;

    public:
        Rectangle(int,int);                                                        
        
        int area() 
        {
            return width*height;
        }                                          
};                                    
```

The constructor for this class could be defined, as usual, as:

```cpp
Rectangle::Rectangle (int x, int y) { width=x; height=y; }
```

But it could also be defined using *member initialization* as:

```cpp
Rectangle::Rectangle (int x, int y) : width(x) { height=y; }
```

Or even:

```cpp
Rectangle::Rectangle (int x, int y) : width(x), height(y) { }
```

Note how in this last case, the constructor does nothing else than
initialize its members, hence it has an empty function body.

For members of fundamental types, it makes no difference which of the
ways above the constructor is defined, because they are not initialized
by default, but for member objects (those whose type is a class), if
they are not initialized after the colon, they are default-constructed.

Default-constructing all members of a class may or may always not be
convenient: in some cases, this is a waste (when the member is then
reinitialized otherwise in the constructor), but in some other cases,
default-construction is not even possible (when the class does not have
a default constructor). In these cases, members shall be initialized in
the member initialization list. For example:

```cpp
// member initialization


#include <iostream>

using namespace std;

class Circle {
    double radius;
  public:
    Circle(double r) : radius(r) { }
    double area() {return radius*radius*3.14159265;}
};

class Cylinder {
    Circle base;
    double height;
  public:
    Cylinder(double r, double h) : base (r), height(h) {}
    double volume() {return base.area() * height;}
};

int main()
{
  Cylinder foo (10,20);

  cout << "foo's volume: " << foo.volume() << '\n';
  return 0;
}```

output:

```text 
foo's volume: 6283.19
```

In this example, class `Cylinder` has a member object whose type is
another class (base's type is *Circle*). Because objects of
class Circle can only be constructed with a parameter, Cylinder's
constructor needs to call *base's* constructor, and the only way to do
this is in the *member initializer list*.

These initializations can also use uniform initializer syntax, using
braces `{}` instead of parentheses `()`:

```cpp
Cylinder::Cylinder (double r, double h) : base{r}, height{h} { }
```

### **8.7.5 Pointers to classes**

Objects can also be pointed to by pointers: Once declared, a class
becomes a valid type, so it can be used as the type pointed to by a
pointer. For example:

```cpp
Rectangle * prect;   
```

is a pointer to an object of class `Rectangle`.

Similarly as with plain data structures, the members of an object can be
accessed directly from a pointer by using the arrow `operator (->)`. Here
is an example with some possible combinations:

```cpp
// pointer to classes example


#include <iostream>

using namespace std;

class Rectangle {
  int width, height;
public:
  Rectangle(int x, int y) : width(x), height(y) {}
  int area(void) { return width * height; }
};


int main() {
  Rectangle obj (3, 4);
  Rectangle * foo, * bar, * baz;
  foo = &obj;
  bar = new Rectangle (5, 6);
  baz = new Rectangle[2] { {2,5}, {3,6} };
  cout << "obj's area: " << obj.area() << '\n';
  cout << "*foo's area: " << foo->area() << '\n';
  cout << "*bar's area: " << bar->area() << '\n';
  cout << "baz[0]'s area:" << baz[0].area() << '\n';
  cout << "baz[1]'s area:" << baz[1].area() << '\n';       
  delete bar;
  delete[] baz;
  return 0;
}
```

This example makes use of several operators to operate on objects and
pointers (operators *, &, ., ->, []). They can be interpreted as:
<dl>
 <style type="text/css">
	table.tableizer-table {
		font-size: 12px;
		border: 1px solid #CCC; 
		font-family: Arial, Helvetica, sans-serif;
	} 
	.tableizer-table td {
		padding: 4px;
		margin: 3px;
		border: 1px solid #CCC;
	}
	.tableizer-table th {
		background-color: #104E8B; 
		color: #FFF;
		font-weight: bold;
	}
</style>
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th>expression</th><th>        can be read as</th></tr></thead><tbody>
 <tr><td>*x</td><td>pointed to by x</td></tr>
 <tr><td>&x</td><td>address of x</td></tr>
 <tr><td>x.y</td><td>member y of object x</td></tr>
 <tr><td>x->y</td><td>member y of object pointed to by x</td></tr>
 <tr><td>(*x).y</td><td>member y of object pointed to by x (equivalent to the previous one)</td></tr>
 <tr><td>x[0]</td><td>first object pointed to by x</td></tr>
 <tr><td>x[1]</td><td>second object pointed to by x</td></tr>
 <tr><td>x[n]</td><td>(n+1)th object pointed to by x</td></tr>
</tbody></table>
</dl>

Most of these expressions have been introduced in earlier chapters. Most
notably, the chapter about arrays introduced the offset operator (`[]`)
and the chapter about plain data structures introduced the arrow
operator (`->`).

## **8.8 Inline Functions in Classes**

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
To make any function as inline, start its definitions with the keyword
"inline".

Example:
```cpp
Class A
{
 Public:
    inline int add(int a, int b)
    {
       return (a + b);
    };
}

Class A
{
 Public:
    int add(int a, int b);
};

inline int A::add(int a, int b)
{
   return (a + b);
}
                            

```
**Why to use --**
In many places we create the functions for small work/functionality
which contain simple and less number of executable instruction. Imagine
their calling overhead each time they are being called by callers.
When a normal function call instruction is encountered, the program
stores the memory address of the instructions immediately following the
function call statement, loads the function being called into the
memory, copies argument values, jumps to the memory location of the
called function, executes the function codes, stores the return value of
the function, and then jumps back to the address of the instruction that
was saved just before executing the called function. Too much run time
overhead.
The C++ inline function provides an alternative. With inline keyword,
the compiler replaces the function call statement with the function code
itself (process called expansion) and then compiles the entire code.
Thus, with inline functions, the compiler does not have to jump to
another location to execute the function, and then jump back as the code
of the called function is already available to the calling program.
With below pros, cons and performance analysis, you will be able to
understand the "why" for inline keyword
**Pros** :-
1. It speeds up your program by avoiding function calling overhead.
2. It save overhead of variables push/pop on the stack, when function
calling happens.
3. It save overhead of return call from a function.
4. It increases locality of reference by utilizing instruction cache.
5. By marking it as inline, you can put a function definition in a
header file (i.e. it can be included in multiple compilation unit,
without the linker complaining)

**Cons**:-
1. It increases the executable size due to code expansion.
2. C++ inlining is resolved at compile time. Which means if you change
the code of the inlined function, you would need to recompile all the
code using it to make sure it will be updated
3. When used in a header, it makes your header file larger with
information which users don't care.
4. As mentioned above it increases the executable size, which may cause
thrashing in memory. More number of page fault bringing down your
program performance.
5. Sometimes not useful for example in embedded system where large
executable size is not preferred at all due to memory constraints.

**When to use -**
Function can be made as inline as per programmer need. Some useful
recommendation are mentioned below-
1. Use inline function when performance is needed.
2. Use inline function over macros.
3. Prefer to use inline keyword outside the class with the function
definition to hide implementation details.

**Key Points -**
1. It's just a suggestion not compulsion. Compiler may or may not inline
the functions you marked as inline. It may also decide to inline
functions not marked as inline at compilation or linking time.
2. Inline works like a copy/paste controlled by the compiler, which is
quite different from a pre-processor macro: The macro will be forcibly
inlined, will pollute all the namespaces and code, won't be easy to
debug.
3. All the member function declared and defined within class are Inline
by default. So no need to define explicitly.
4. Virtual methods are not supposed to be inlinable. Still, sometimes,
when the compiler can know for sure the type of the object (i.e. the
object was declared and constructed inside the same function body), even
a virtual function will be inlined because the compiler knows exactly
the type of the object.
5. Template methods/functions are not always inlined (their presence in
an header will not make them automatically inline).
6. Most of the compiler would do in-lining for recursive functions but
some compiler provides #pragmas-
microsoft c++ compiler - inline_recursion(on) and once can also control
its limit with inline_depth.
In gcc, you can also pass this in from the command-line with
--max-inline-insns-recursive

> <https://www.cplusplus.com/articles/2LywvCM9/>

## **8.9 Data Field Encapsulation**

Data Encapsulation is one of the object-oriented concept that binds
together the data and functions that manipulate the data, and that keeps
both safe from outside interference and misuse. Data encapsulation led
to the important OOP concept of **data hiding**.

Encapsulation can be achieved using the user defined types called
classes. Each member or a function can be private or public or protected
depending on the usage. Every member is a private by default.

Members that are private can only be accessed inside the class. Public
members can be accessed anywhere in the program or outside the program.

## **8.10 Chapter Summary**
This chapter provides you the basic understanding of object oriented programming and the N-d arrays. You will learn about these topics in depth when you take the advanced courses in C++. Now you have completed with the basics of programming and the outline of the advanced topics which is the start to your programming career. Keep coding!!!