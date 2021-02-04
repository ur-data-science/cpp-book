---
title: Mathematical Functions, Characters, and Strings
author: Dr. Alireza Manashty
date: 2021-02-04
category: cpp
layout: post
---

# Mathematical Functions, Characters, and Strings

## 4.1 Introduction and Objectives

In this chapter you are going to learn about cmath library and various
mathematical functions that you could use, characters, strings, and the
functions that you can use to work with these two variable types.

## 4.2 Mathematical Functions

```cpp
#include <cmath>
```

-   **abs**: absolute value of a floating point value (|x|)

 *Parameters*-
    *arg* - Value of a floating-point or integral type

 *Return value*
     If successful, returns the absolute value of arg (|arg|). The value returned is exact and does not depend on any rounding modes. <https://en.cppreference.com/w/cpp/numeric/math/fabs

-   **log10**:
 computes common (base 10) logarithm ($log_{10}x$)

 *Parameters*
   arg - value of floating-point or Integral type

 *Return value*
- If no errors occur, the common (base-10) logarithm of arg  (l$log_{10}(arg)$
 or$lg(arg)$) is returned.
- If a domain error occurs, an implementation-defined value is returned (NaN where supported)
- If a pole error occurs, -HUGE_VAL, -HUGE_VALF, or -HUGE_VALL is returned.

> <https://en.cppreference.com/w/cpp/numeric/math/log10>

-   **log**:

 computes natural (base *e*) logarithm (ln(x))
 *Parameters*
      arg - value of floating-point or Integral type
 *Return value*
 
-   If no errors occur, the natural (base-e) logarithm of arg ($ln(arg)$ or $log_{e}(arg)$) is returned.
-   f a domain error occurs, an implementation-defined value is returned (NaN where supported)
-   f a pole error occurs, -HUGE_VAL, -HUGE_VALF, or -HUGE_VALL is returned.

> <https://en.cppreference.com/w/cpp/numeric/math/log>

-   **pow**
    raises a number to the given power ($x^{y}$)

**Parameters**

| parameters   | Descriptions
|------------  |--------------------------------------------------
| `base`       | base as a value of floating-point or integral type
| `exp`        | exponent as a value of floating-point or integral type
| `iexp`       | exponent as integer value

 **Return value**
  - If no errors occur, base raised to the power of exp (or iexp), is returned.
  - If a domain error occurs, an implementation-defined value is returned x(NaN where supported)
  - If a pole error or a range error due to overflow occurs, `±HUGE_VAL`, `±HUGE_VALF`, or ±HUGE_VALL is returned.
  - If a range error occurs due to underflow, the correct result (after rounding) is returned.
> <https://en.cppreference.com/w/cpp/numeric/math/pow>

-   **sqrt**
 computes square root ($sqrt{x}$)

 **Parameters**
- arg - Value of a floating-point or integral type

 **Return value**
  - If no errors occur, square root of arg ($sqrt{arg}$), is returned.
  - If a domain error occurs, an implementation-defined value is returned (NaN where supported)
  -  If a range error occurs due to underflow, the correct result (after rounding) is returned.
 <https://en.cppreference.com/w/cpp/numeric/math/sqrt

-   **cbrt**
computes cubic root ($sqrt{x}$)

 **Parameters**
 arg - value of a floating-point or Integral type

 **Return value**
 - If no errors occur, the cubic root of arg ($sqrt[3]{arg}$), is returned.
 - If a range error occurs due to underflow, the correct result (after rounding) is returned.

> <https://en.cppreference.com/w/cpp/numeric/math/cbrt>

> <http://www.cplusplus.com/reference/cmath/>


## 4.3 Character Data Type and Operations

-   `signed char` - type for *signed character* representation.

-   `unsigned char` - type for *unsigned character* representation. 
    Also used to inspect 
    [object representations](https://en.cppreference.com/w/cpp/language/object) 
    (raw memory).

-   `char` - type for character representation which can be most efficiently 
    processed on the target system 
    (has the same representation and alignment as either `signed char` or
    `unsigned char`, but is always a distinct type). 
    [Multibyte characters  strings](https://en.cppreference.com/w/cpp/string/multibyte) 
    use this type to represent code units. 
    The character types are large enough to represent any `UTF-8` eight-bit code unit (since C++14). 
    The signedness of char depends on the compiler and the target platform: 
    the defaults for ARM and PowerPC are typically unsigned, the defaults for `x86` and `x64` are typically signed.

-   `wchar_t` - type for wide character representation 
    (see [wide strings](https://en.cppreference.com/w/cpp/string/wide). 
    Required to be large enough to represent any supported character code 
    point (32 bits on systems that support Unicode. 
    A notable exception is Windows, where wchar_t is 16 bits and holds 
    `UTF-16` code units) It has the same size, signedness, and alignment as 
    one of the integer types, but is a distinct type.

|  Data Type | Since
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------
|  char16_t - type for UTF-16 character representation, required to be large enough to represent any UTF-16 code unit (16 bits). It has the same size, signedness, and alignment as [std::uint_least16_t](https://en.cppreference.com/w/cpp/types/integer), but is a distinct type.          |  (since C++11)         
|  char32_t - type for UTF-32 character representation, required to be large enough to represent any UTF-32 code unit (32 bits). It has the same size, signedness, and alignment as [std::uint_least32_t](https://en.cppreference.com/w/cpp/types/integer), but is a distinct type.          |       -
|  char8_t - type for UTF-8 character representation, required to be large enough to represent any UTF-8 code unit (8 bits). It has the same size, signedness, and alignment as unsigned char (and therefore, the same size and alignment as char and signed char), but is a distinct type.  |  (since C++20)

 - Besides the minimal bit counts, the C++ Standard guarantees that

```
1 == sizeof(char) <= sizeof(short) <= sizeof(int) <= sizeof(long) <= sizeof(long long).
```

**Note:** 
this allows the extreme case in which 
[bytes](https://en.wikipedia.org/wiki/Byte) 
are sized 64 bits, all types (including char) are 64 bits wide, 
and sizeof returns 1 for every type.

> <https://en.cppreference.com/w/cpp/language/types>

> <http://www.cs.uregina.ca/Links/class-info/110/unix/index.html>

> <http://www.cplusplus.com/doc/tutorial/variables/>

## 4.4 Character Functions

```cpp
<cctype (ctype.h)
```

These functions take the int equivalent of one character as parameter
and return an int that can either be another character or a value
representing a boolean value: an int value of 0 means false, and an int
value different from 0 represents true.

There are two sets of functions:

**1. Character classification functions**

They check whether the character passed as parameter belongs to a
certain category:

|  Category   |  Description
|----------   |--------------------------
|  isalnum    |  Check if character is alphanumeric (function )
|  isalpha    |  Check if character is alphabetic (function )
|  isblank    |  Check if character is blank (function )
|  iscntrl    |  Check if character is a control character (function )
|  isdigit    |  Check if character is decimal digit (function )
|  isgraph    |  Check if character has graphical representation (function )
|  islower    |  Check if character is lowercase letter (function )
|  isprint    |  Check if character is printable (function )
|  ispunct    |  Check if character is a punctuation character (function )
|  isspace    |  Check if character is a white-space (function )
|  isupper    |  Check if character is uppercase letter (function )
|  isxdigit   |  Check if character is hexadecimal digit (function )

**2. Character conversion functions**

Two functions that convert between letter cases:

  tolower   Convert uppercase letter to lowercase (function)
  --------- ---------------------------------------------------
  toupper   Convert lowercase letter to uppercase (function)

> <http://www.cplusplus.com/reference/cctype/>

## 4.5 The string Type

C++ has a string class. Some functions are defined in the class for strings to use. 
In C++ programming, you can declare string variables/objects. 
A string may be declared with or without an initial value.
If you do not indicate the initial value, the initial value is an empty string (zero length, no characters).

Here are some examples to help you understand C++ strings:

 ```cpp
//declare a string str1
string str1;

//A string variable/object may be initialized with
//a character string literal:
string str2 = "Hello there";
string str3("Goodbye"); // Alternate form

//A string variable/object may also be initialized with
//a string expression:
string str4 = str2;
string str5 = str2 + str3;

//A string variable/object may also be initialized with
//a substring of another string object:
string str6 = "ABCDEFGHIJKL";

// Initialize str7 as "CDEFG"
// Starts at character 2 ('C')
// with a length of 5
// (or the rest of the string, if shorter)
string str7(str6,2,5);
```

**The `length()` and `size()` Functions**

Both of these functions return the number of characters in the string. 
It returns a special type: size_type. It is an unsigned integer. 
We use the qualified `name string::size_type` because the definition of 
`size_type` is otherwise hidden inside the definition of the string type.

```cpp
string str8 = "Hello";
string::size_type len;

//Store returned values in a variable, then use them:
len = str8.length();
cout << len << endl; // prints 5
len = str8.size();
cout << len << endl; // also prints 5

// OR just use them directly:
cout << str8.length() << endl;
```
**The `find()` and `substr()` Functions**

The `find()` function searches the string it is called on, 
to find the first occurance of a particular substring.

- If the substring is found, `find()` returns the position of the first character. 
  If not, `find()` returns the special value s`tring::npos`.

- The `first argument` is the search substring. It is a string or string literal.
- The `second argument` is where to start searching. It is an integer greater than or equal to 0.
- If you leave it out, `find()` starts at 0.
 
 For example:

```cpp
string str16 = "abcdefghi";
string str17 = "def";

// Search from the beginning of str16
string::size_type pos = str16.find(str17);
cout << pos << endl; // prints 3

// Search from the beginning of str16
pos = str16.find(str17,0);
cout << pos << endl; // prints 3

// Search from the fifth position of str16
pos = str16.find(str17,5);
cout << pos << endl; // prints a REALLY BIG number!!
pos = str16.find("AB");

if(pos == string::npos)
{
    cout << "Not found." << endl;
    return 1;
}
```

- The `substr()` function cuts a substring out of a string. The `substr()` function always returns a substring of the string it is called on the first parameter is the start position of the substring the other parameter is is the length of the substring.
- If you leave it out, `substr()` returns everything from the start position to the end of the string.

For example:

```cpp
string str18 = "abcdefghi"
string str19 = str18.substr(5,2);
cout <<str19 <<endl; // prints "fg"
string str20 = str18.substr(5);
cout <<str20 <<endl; // prints "fghi"
```

**Operators**

A number of C++ operators also work with strings.

The assignment operator = may be used in several ways:

```cpp
//Assigning one string's value to another string
string string_one = "Hello";
string string_two;
string_two = string_one;
```
```cpp
//Assigning a single character (char) to a string
string string_four;
char ch = 'A';
string_four = ch;
string_four = 'Z';
```

The `plus` operator concatenates:

```cpp
// two strings
string str1 = "Hello ";
string str2 = "there";
string str3 = str1 + str2; // "Hello there"
```

```cpp
// a string and a character string literal
string str1 = "Hello ";
string str4 = str1 + "there";
```

```cpp
// a string and a single character
string str5 = "The End";
string str6 = str5 + '!';
```

The "+=" operator appends:
i.e: it combines the assignment and concatenation operations in the way
that you would expect.

The right-hand sice must be a string object, a string literal, or a
single character.

```cpp
string str1 = "Hello ";
str1 += "there";
```

> <https://www.tutorialspoint.com/cplusplus/cpp_strings.htm>

> <http://www.cs.uregina.ca/Links/class-info/110/fileio/index.html>

## 4.6 Formatting Console Output

There are two ways to get input into our programs. First, we use `istream`
variable cin together with the extraction operator  to get data from
the standard input device --- the keyboard. The other way is to get data
from a file to the program. We will talk about that next lab.

Here is the syntax template for an input statement

```cpp
cin >> Variable >> Variable >> ... ;
```

When you enter data at the keyboard, you must be sure that each value is
appropriate for the data type of the variable in the input statement. If
nothing can be read for a variable then input will fail and, unless you
take special action, nothing more can be read by your program. This will
cause unexpected behaviour.

The `>>` operator skips any leading white space characters when it is
looking for the next input value in the stream. Whitespace characters
are blanks and certain non-printable characters such as the character
that marks the end of a line (new line character). After skipping any
whitespace characters, `>>`  operator proceeds to extract the desired
data value from the input stream. If the data value is int or float,
input of the number stops at the first character that is inappropriate
for the data type, such as a whitespace character or letter. If the data
value is a char value, one printable character is input.

The get input function works a little differently. It inputs the next
character in the stream regardless of what it is, even if it is a
whitespace character or new line character.

Whether you use `get` or `>>` , when input is finished for one variable,
input continues to the next one until all input requests are satisfied.
If there is not enough input, the program will wait for the user to type
more and press enter. If there is too much input it will be remembered
until the next time input is needed and then it will be used.

Now look at the following character reading example. Compile and run the
two tests with the same set of the input data. e.g.
```
 a b c d
```
```
 a
 2
 b
 c
```
Examine the results carefully.

 ```cpp
 //This program demonstrates input with  and get for characters
 //and with  for other data types.
 #include <iostream
 #include <string
 using namespace std;

 int main ()
 {
 char char1;
 char char2;
 char char3;
 char char4;

 cout <<"******Extraction operator  test******"<<endl;
 cout <<"Input four characters. Press Return." <<endl;
 cin >>char1 >> char2 >> char3 >> char4;
 cout <<char1 <<char2 <<char3 <<char4 <<endl;

 cin.ignore(100,'\n');

 cout <<endl <<"******get() function test******"<<endl;
 cout <<"Input four characters. Press Return." <<endl;
 cin.get(char1);
 cin.get(char2);
 cin.get(char3);
 cin.get(char4);
 cout << char1 << char2 << char3 << char4 << endl;

 return 0;

 }
```
This next program demonstrates reading mixed datatypes with one cin.Try
the mixed type test with this input:

 ```
 3.1416Huh? What's going on?
```
```cpp
 //This program demonstrates input with  and get for characters
 //and with  for other data types.
 #include <iostream
 #include <string
 using namespace std;
 int main ()
 {
 int int1;
 float float1;
 string string1;
 cout <<"Mixed type test" <<endl;
 cin >> int1 >> float1 >> string1;
 cout <<string1 <<" " <<float1 <<" " <<int1 <<endl;
 cout <<endl <<"*****using getline() function below******" <<endl <<endl;

 getline(cin,string1);
 cout <<string1 <<endl;

 return 0;
 }
```
Notice the neat trick to get more than one word into a string? For a
string variable, say inputStr, the statement
```cpp
 cin >> inputStr;
```
skips leading whitespace and it stops as soon as it encounters a
whitespace character. The statement
```cpp
 getline(cin, inputStr);
```
does not skip the leading whitespace character(s). It stops when a new
line character 'n' is encountered. getline is a function from C++
standard library.

> <http://www.cs.uregina.ca/Links/class-info/110/strings/index_oldtext.html>

## 4.7 Simple File Input and Output

If you want to prepare input data ahead, you may store the data in a
file and direct the program to read its input from a file. If you want
to save output data in a file to use later, you may direct the program
to write to a file. To read and/or write to a file, do the following:

Request the preprocessor to include file `fstream` as well as `iostream`.
`fstream` contains the declarations for defining input and output streams
with files other than `cin` and `cout`.

Declare an input stream to be of type `ifstream` or an output stream to be
of type `ofstream`.

Prepare the stream for use by using the function named open provided in
file `fstream`. The parameter for the function open is the external name
of the file. The external name is the name under which the file is
stored on the disk.

Put the internal file name to the left of the insertion or extraction
operator.

Here is an example program that reads four floating point data values
from a file and writes to another file in the reverse order.

```cpp
// Program IODemo demonstrates how to use files

#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    cout << fixed;
    //sets all printout in decimal format with decimal points appearing
    
    float val1, val2, val3, val4; // declares 4 variables
    ifstream inData; // declares input stream
    ofstream outData; // declares output stream
    inData.open("inputfile.txt");

    // binds program variable inData to the input file "inputfile.txt"
    outData.open("outputfile.txt");

    // binds program variable outData to the output file
    "outputfile.txt"

    inData  val1  val2  val3  val4; // inputs 4 values
    outData << val4 << endl;
    outData << val3 << endl;
    outData << val2 << endl;
    outData << val1 << endl; // outputs 4 values

    inData.close();
    outData.close();
    return 0;
}
```

Each file in your program has both an internal name and an external
name. The internal name is what you call it in your program; the
external name is the name the operating system knows it by. Somehow,
these two names must be associated with one another. This association is
called binding and is done in function open. Notice that inData and
outData are identifiers in the program; `inputfile.txt` and
`outputfile.txt` are character strings. `inputfile.txt` is the name that
was used when the input data file was created; `outputfile.txt` is the
name of the file where the answers are stored.

You will need to use the pico or vi text editor to create the input data
file according the requirement of the data type and format in your
program. The input data file must exist and contain correct data.
Otherwise, the input will fail.

You can also create a data file by selecting "Add New Item" to a
project as a text file in the Visual C++.

For example, in the preceding IODemo program, the input file should look
like this:

```text
5.5
6.6
7.7
8.8
```

State of an I/O Stream

We know any of the following can cause an input stream to enter the fail state:

- Invalid input data
- An attempt to read beyond the end of a file
- An attempt to open a nonexistent file to input

C++ provides a way to test the state of a stream: The stream name used
in the expression returns true value if the state is ok and false value
if the state is in the fail state. Here is an example program that reads
four floating point data values from a file and write to another file in
the reverse order.

```cpp
// Program IODemo demonstrates how to use files

#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    cout << fixed;
    float val1, val2, val3, val4; // declares 4 variables
    ifstream inData; // declares input stream
    ofstream outData; // declares output stream

    // binds program variable inData to file "inputfile.txt"
    inData.open("inputfile.txt");

    //Testing the state of the stream
    //true means the last I/O operation on that stream succeeded
    //false means the last I/O operation on that stream failed
    if(!inData)
    {
        cout << "Can't open the input file successfuly." << endl;
        return 1;
    }

    // binds program variable outData to file "outputfile.txt"
    outData.open("outputfile.txt");

    //Testing the state of the stream
    if(!outData)
    {
        cout << "Can't open the output file successfuly." << endl;
        return 2;
    }

    inData >> val1 >> val2 >> val3 >> val4; // inputs 4 values
    outData << val4 << endl;
    outData << val3 << endl;
    outData << val2 << endl;
    outData << val1 << endl; // outputs 4 values
    
    inData.close();
    outData.close();
    return 0;
}
```
***Note*** that `inData` and `outData` are two variables in the program;
`inputfile.txt` and `outputfile.txt` are character strings.
`inputfile.txt` is the name of the input data file that we have created;
`outputfile.txt` is the name of the output data file where the answers are
stored.

If the input file `inputfile.txt` cannot be found, 1 is returned to the
operating system. If the output file `outputfile.txt` cannot be opened or
created, 2 is returned to the operating system. If there is no input and
output error, 0 is returned to the operating system. Notice that the
main is exited as soon as a value is returned. Therefore, Returning 0
value means normal completion of a program; returning any other value
signals an error. When you write your own program, you may choose the
value to return to indicate different error conditions.

You can use pico or vi text editor to create the input data file
according to the requirement of the data type and format in your
program. Input data file must exist and contain correct data. Otherwise,
you will get input failure.

For example, in the preceding IODemo program, the input file should look
like this:

```text
5.5
6.6
7.7
8.8
```

You may run the program and and test the state of the I/O stream.

> <http://www.cs.uregina.ca/Links/class-info/110/fileio/index.html>

> <http://www.cplusplus.com/doc/tutorial/files/>

## 4.8 Chapter Summary

All in all, now we know how to use char and string data type and 
use pre-built mathematical, string, and character functions. 
Also, we know how to read input information from a file and write 
the output in an output file as well._
