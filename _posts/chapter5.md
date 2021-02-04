---
title: Loops
author: Dr. Alireza Manashty
date: 2021-02-04
category: cpp
layout: post
---

# Loops

## 5.1 Introduction and Objectives

When the program needs to be executed multiple times on a sequence of
inputs or validate them using the condition statements then it is not a
productive way of writing the same program with the similar conditions
repetitively. So, Loops repeat a statement a certain number of times, or
while a condition is fulfilled. They are introduced by the
keywords while, do, and for.

> <http://www.cplusplus.com/doc/tutorial/control/>

## 5.2 The while Loop

The simplest kind of loop is the while-loop. Its syntax is:

```cpp
while (expression) statement
```

The while-loop simply repeats statement while expression is true. If,
after any execution of statement, expression is no longer true, the loop
ends, and the program continues right after the loop.

For example, let's have a look at a countdown using a while-loop:

```cpp
//  [url](http://www.cplusplus.com/doc/tutorial/control/) 


#include <iostream>
                                                   
using namespace std;                                        
                                                      
int main ()                                                                                                   
{                                                       
    int n = 10;                                                                                                    
    while (n>0) {                                        
      cout << n << ", ";                                                 
      --n;                                                                                                           
    }
    cout << "liftoff!\n";                                        
}
```

Output:

```text
10, 9, 8, 7, 6, 5, 4, 3, 2, 1, liftoff!
```

The first statement in main sets `n` to a value of 10. This is the first
number in the countdown. Then the while-loop begins: if this value
fulfills the condition `n>0` (that n is greater than zero), then the
block that follows the condition is executed, and repeated for as long
as the condition (`n>0`) remains being true.

The whole process of the previous program can be interpreted according
to the following script (beginning in main):

1.  `n` is assigned a value

2.  The while condition is checked (`n>0`). At this point there are two
    possibilities:

    -   condition is true: the statement is executed 
        (to step 3)

    -   condition is false: ignore statement and continue after it 
        (to step 5)

3.  Execute statement:

    `cout << n << ", ";` 
    
    `--n;`

    (prints the value of `n` and decreases `n` by `1`)

4.  End of block. Return automatically to step 2.

5.  Continue the program right after the block:
    print `liftoff!` and end the program.

A thing to consider with while-loops is that the loop should end at some
point, and thus the statement shall alter values checked in the
condition in some way, so as to force it to become false at some point.
Otherwise, the loop will continue looping forever. In this case, the
loop includes `--n`, that decreases the value of the variable that is
being evaluated in the condition (`n`) by one - this will eventually make
the condition (`n>0`) false after a certain number of loop iterations. To
be more specific, after `10` iterations, `n` becomes `0`, making the condition
no longer true, and ending the while-loop.

Note that the complexity of this loop is trivial for a computer, and so
the whole countdown is performed instantly, without any practical delay
between elements of the count
(if interested, see [sleep_for](http://www.cplusplus.com/sleep_for) 
for a countdown example with delays).

> <http://www.cs.uregina.ca/Links/class-info/110/loops/index.html>

> <https://www.tutorialspoint.com/cplusplus/cpp_while_loop.htm>

## 5.3 Loop Design Strategies

Initial days of programming makes it difficult to understand the working
of the loops and while to implement you may make some errors. So, here
are 3 steps to follow when writing the loop.

◦ Identify the statements that need to be repeated in a program.

`Statement1`, `statement2`, ...

◦ Place these statements in a loop (Infinite loop) as below:
```
while True:
{
    All Statements
}
```
◦ Code the **loop-continuation-condition** and include appropriate
**statements to control the loop**.

```cpp
while loop-continuation-condition:
{
    Statements
    Additional statements for controlling the loop
}
```


## 5.4 Controlling a Loop with User Confirmation

We can write a program using a loop that executes the next iteration
only if it gets some input from the user which controls the flow the
program. The user input can be defined whether to execute the next
iteration or to come out of the loop and terminate that block of code.

```cpp
continueLoop = 'Y'
while continueLoop == 'Y':
{
    # Execute the loop body once ...
    # Prompt the user for confirmation

    continueLoop = input("Enter Y to continue and N to quit: ")
}
```

Controlling a value with a sentinel value can also be a good idea. A
sentinel value is a special value that is used to terminate the loop
when reading a user input. This special value signifies the end of the
input. If a loop that uses sentinel value is called Sentinel value
controlled loop.

E.g. Tell the user to input any positive integer values. And inform the
user that giving a negative integer `-1` will terminate the loop. So, `-1`
is the sentinel value in this program.

## 5.5 Input and Output Redirections and Read All Data from a File

TODO

## 5.6 The do-while Loop

A very similar loop is the do-while loop, whose syntax is:

```cpp
do statement while (condition);
```

It behaves like a while-loop, except that condition is evaluated after
the execution of statement instead of before, guaranteeing at least one
execution of statement, even if condition is never fulfilled. For
example, the following example program echoes any text the user
introduces until the user enters goodbye:

```cpp
*/
    echo machine
    Enter text: hello You entered: hello Enter text: goodbye You entered: goodbye
*/

#include <iostream>
#include <string>                                            

using namespace std;
                                         
int main()
{
    string str;                                                                    
    do {                                                                    
        cout << "Enter text: ";
        getline(cin,str);
        cout << "You entered: " << str << '\n';
    } while (str != "goodbye");
}
```
> The do-while loop is usually preferred over a while-loop when
> the statement needs to be executed at least once, such as when the
> condition that is checked to end of the loop is determined within the
> loop statement itself. In the previous example, the user input within
> the block is what will determine if the loop ends. And thus, even if
> the user wants to end the loop as soon as possible by
> entering goodbye, the block in the loop needs to be executed at least
> once to prompt for input, and the condition can, in fact, only be
> determined after it is executed.

> <http://www.cs.uregina.ca/Links/class-info/110/loops/write-p1.html>

## 5.7 The for Loop

The for loop is designed to iterate a number of times. Its syntax is:

```cpp
for (initialization; condition; increase) statement;
```

Like the while-loop, this loop repeats statement while condition is
true. But, in addition, the for loop provides specific locations to
contain an initialization and an increase expression, executed before
the loop begins the first time, and after each iteration, respectively.
Therefore, it is especially useful to use counter variables
as condition.

It works in the following way:

1.  initialization is executed. Generally, this declares a counter
    variable, and sets it to some initial value. This is executed a
    single time, at the beginning of the loop.

2.  condition is checked. If it is true, the loop continues; otherwise,
    the loop ends, and statement is skipped, going directly to step 5.

3.  statement is executed. As usual, it can be either a single statement
    or a block enclosed in curly braces `{ }`.

4.  increase is executed, and the loop gets back to step 2.

5.  the loop ends: execution continues by the next statement after it.

Here is the countdown example using a for loop:

```cpp
// countdown using a for loop


#include <iostream>

using namespace std;

int main ()
{
    for ( int n=10 ; n>0 ; n-- )                                       
    {
        cout << n << ", ";                                         
    }                                    
    cout << "liftoff!\n";                                        
}
```

Ooutput:

```text
10, 9, 8, 7, 6, 5, 4, 3, 2, 1, liftoff!
```

The three fields in a for-loop are optional. They can be left empty, but
in all cases the semicolon signs between them are required. For
example, `for (;n<10;)` is a loop
without *initialization* or *increase* (equivalent to a while-loop);
and `for (;n<10;++n)` is a loop with *increase*, but
no *initialization* (maybe because the variable was already initialized
before the loop). A loop with no *condition* is equivalent to a loop
with true as condition (i.e., an infinite loop).

Because each of the fields is executed in a particular time in the life
cycle of a loop, it may be useful to execute more than a single
expression as any of *initialization*, *condition*, or *statement*.
Unfortunately, these are not statements, but rather, simple expressions,
and thus cannot be replaced by a block. As expressions, they can,
however, make use of the comma operator (`,`): This operator is an
expression separator, and can separate multiple expressions where only
one is generally expected. For example, using it, it would be possible
for a for loop to handle two counter variables, initializing and
increasing both:

```cpp
for ( n=0, i=100 ; n!=i ; ++n, --i )    
{
    // whatever here...
}                                          
```

This loop will execute 50 times if neither `n` or `i` are modified within
the loop:

![alt-image](../images/chapter_05/Picture1.png)

`n` starts with a value of `0`, and `i` with `100`, the condition is `n!=i` 
(i.e., that `n` is not equal to `i`). 

Because `n` is increased by one, and `i` decreased by one on each iteration, 
the loop's condition will become false after the 50th iteration, when both `n` and `i` are equal to
`50`.

#### Range-based for loop

The for-loop has another syntax, which is used exclusively with ranges:
```cpp
for ( declaration : range ) statement;
```
This kind of for loop iterates over all the elements in range,
where declaration declares some variable able to take the value of an
element in this range. Ranges are sequences of elements, including
arrays, containers, and any other type supporting the
functions begin and end; Most of these types have not yet been
introduced in this tutorial, but we are already acquainted with at least
one kind of range: strings, which are sequences of characters.

An example of range-based for loop using strings:

```cpp
*/ 
    range-based for loop   
    [H][e][l][l][o][!]
*/

#include <iostream>                                          
#include <string>*                                             

using namespace std;

int main()
{
    string str{"Hello!"};

    for (char c : str)
    {
        cout << "[" << c << "]";                              
    }                                                       
                                                              
    cout << '\n';
}
```

Note how what precedes the colon (`:`) in the for loop is the declaration
of a char variable (the elements in a string are of type char). We then
use this variable, `c`, in the statement block to represent the value of
each of the elements in the range.

This loop is automatic and does not require the explicit declaration of
any counter variable.

Range based loops usually also make use of type deduction for the type
of the elements with auto. Typically, the range-based loop above can
also be written as:

```cpp
for (auto c : str) cout << "[" << c << "]";
```

Here, the type of c is automatically deduced as the type of the elements
in str.

> <http://www.cs.uregina.ca/Links/class-info/110/loops/write-p1.html>

## 5.8 Which Loop to Use?

Now we know there are 3 different looping techniques, but which one to
use where?

There are no strict rules that says you need to use them for specific
purpose. All of them are used to iterate you through the whole block of
statements until the end condition is met and loop is terminated. But
here are some rules that you can follow to make the program efficient

Use For loop when you know the number of iterations. E.g. iterate
through an array of size `N`.

Use While loop when you do not know how many iterations it will take to
satisfy the condition(make sure you give a valid terminating condition
otherwise program will go into infinite loop and program stops with out
of memory error)

Situations where you can use while loop are reading an input file into a
variable, when you are taking input from user and when the increment
value is not standard.

And when you want to execute the block of statements at least once
without considering the satisfying condition then you can go with Do-
while loop

## 5.9 Nested Loops

The body of a loop can contain any type of statement including another
loop such as a While loop, a Do-while loop, or a For loop. A loop inside
another loop is called a nested loop.

The following program counts the number of characters on each line in a
file. We know that the I/O manipulator `endl` forces the next character
sent to the output stream to begin a new line. How can we recognize a
new line in the input stream? A new line begins following the symbol
`\n`. We must be sure to use function get defined in `iostream`, not
the extraction operator, to input each character.
```
/* 
    Program LineCt counts the number of characters per line
    and the number of lines in a file.
    
    Assumption: There is a '\n' before the EOF.
*/

#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    int lineNo;
    char character;
    int number;

    ifstream inData; //declares input stream

    // bind the input stream name *inData* to the file "Input.txt"
    inData.open("Input.txt");

    if (!inData)
    {
        cout << "Can't open the input file successfully." << endl;
        return 1;
    }

    lineNo = 0;
    
    //Use get function to read data from file "Input.txt"
    inData.get(character);

    //while the input stream is not in the fail state
    //e.g. while not EOF, go into the loop
    while (inData)
    {
        lineNo++;
        number = 0;

        //while not "end of line", go into the loop
        while (character != '\n')
        {
            number++;
            inData.get(character);
        }
        cout << "Line " << lineNo << " contains " << number << " characters." << endl;
    
    inData.get(character);
    }

    inData.close();
    return 0;
}
```
> <http://www.cs.uregina.ca/Links/class-info/110/loops/index.html>


## 5.10 Minimizing Numeric Errors

Using floating-point numbers in the loop-continuation condition may
cause numeric errors.

• Numerical errors involving floating-point numbers are inevitable.

• This section provides an example showing you how to minimize such
errors.

The following program sums a series that starts with `0.01` and ends with
`1.0`. The numbers in the series will increment by `0.01`, as follows: 
`0.01 + 0.02 + 0.03` and so on.

LISTING 5.7 Sum.cpp
```cpp
//Initialize sum

#include <iostream>

Using namespace std;

int main()
{
    Float sum = 0;
    # Add 0.01, 0.02, \..., 0.99, 1 to sum
    float i = 0.01;
    
    while( i <= 1.0)
    { 
        sum += i;
        i = i + 0.01;
    }

    //Display result
    cout << "The sum is" << sum;
}
```
Output: `The sum is 49.50000000000003`

Here the Actual output should be 50.5, but when the iteration ends the
value of i is slightly greater than 1 but not exactly one (1.01) so the
loop terminates and gives a slight error in output. Basically, the
floating points are represented by approximation. So, we should avoid
floating points in iterating the loops.

## 5.11 Jump Statements (Keywords break and continue)

Jump statements allow altering the flow of a program by performing jumps
to specific locations.

#### The break statement

break leaves a loop, even if the condition for its end is not fulfilled.
It can be used to end an infinite loop, or to force it to end before its
natural end. For example, let's stop the countdown before its natural
end:

```cpp
*/
    break loop example
    10, 9, 8, 7, 6, 5, 4, 3, countdown aborted!
    [url](http://www.cplusplus.com/doc/tutorial/control/)
 
#include <iostream>

using namespace std;

int main ()
{
    for (int n=10; n>0; n--)
    {   
        cout << n << ", ";
        if (n==3)
        {
            cout << "countdown aborted!";
            break;
        }                                                       
    }
}                                                       
```

#### The continue statement

The continue statement causes the program to skip the rest of the loop
in the current iteration, as if the end of the statement block had been
reached, causing it to jump to the start of the following iteration. For
example, let's skip number 5 in our countdown:

```cpp
*/ 
    continue loop example
    10, 9, 8, 7, 6, 4, 3, 2, 1, liftoff!
    [url](http://www.cplusplus.com/doc/tutorial/control/)
*/

#include <iostream>

using namespace std;

int main ()
{
    for (int n=10; n>0; n--)
    {
        if (n==5) continue;
        cout << n << ", ";
    }
    
    cout << "liftoff!\n";
}                                                       
```

#### The goto statement

goto allows to make an absolute jump to another point in the program.
This unconditional jump ignores nesting levels, and does not cause any
automatic stack unwinding. Therefore, it is a feature to use with care,
and preferably within the same block of statements, especially in the
presence of local variables.

The destination point is identified by a *label*, which is then used as
an argument for the goto statement. A *label* is made of a valid
identifier followed by a colon (`:`).

goto is generally deemed a low-level feature, with no particular use
cases in modern higher-level programming paradigms generally used with
C++. But, just as an example, here is a version of our countdown loop
using goto:
```cpp
// goto loop example  10, 9, 8, 7, 6, 5, 4, 3, 2, 1, liftoff!

#include <iostream>

using namespace std;

int main()
{
    int n=10;
    
    mylabel:
        cout << n << ", ";
        n--;
        if(n>0) goto mylabel;
    
    cout << "liftoff!\n";
```
> <https://www.w3schools.com/cpp/cpp_break.asp> (optional)

## 5.12 Chapter Summary

In this chapter, you have learned how to use loops, jump statements and
where to use the loops with the error making possibilities and solutions
for them.
