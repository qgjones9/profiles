# Table of Contents

<!-- vscode-markdown-toc -->
* 1. [Control Flow](#ControlFlow)
	* 1.1. [If statements](#Ifstatements)
	* 1.2. [Nesting if Statements](#NestingifStatements)
	* 1.3. [Loops](#Loops)
	* 1.4. [While loop syntax](#Whileloopsyntax)
	* 1.5. [For Loops](#ForLoops)
	* 1.6. [Index-Based For Loops](#Index-BasedForLoops)
	* 1.7. [Break and Continue Statements](#BreakandContinueStatements)
* 2. [Functions](#Functions)
	* 2.1. [Return Statement](#ReturnStatement)
	* 2.2. [Information Passing](#InformationPassing)
	* 2.3. [Mutable Parameters](#MutableParameters)
	* 2.4. [Default Parameter Values](#DefaultParameterValues)
	* 2.5. [Keyword Parameters](#KeywordParameters)
* 3. [Console input and output](#Consoleinputandoutput)
	* 3.1. [files](#files)
* 4. [Exception Handling](#ExceptionHandling)
	* 4.1. [Common Exception Types](#CommonExceptionTypes)
	* 4.2. [Raising an Exception](#RaisinganException)
	* 4.3. [Catching an Exception](#CatchinganException)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

##  1. <a name='ControlFlow'></a>Control Flow  
colon character delimits beginning of a block of code that acts as a body for a control structure.  
A body starts on on an indented new line following the colon. 
Python relies on the indentation level to designate the extent of that block of code, or any nested blocks of code within. 

###  1.1. <a name='Ifstatements'></a>If statements
- Also known as if statements
- Execute a chosen block of code based on run-time evaluation of one or more Boolean expressions.

```bash
if first condition: 
    first body
elif second condition: 
    second body
elif third condition: 
    third body
else:
    fourth body
```

What data type does each condition evaluates to?
- Each condition is a Boolean expression

What is contained in the body of a conditional construct?
- Each body contains one or more commands that are to be executed conditionally. 

>  What is the execution process of the conditional construct's body?  
- If the first condition succeeds then the first body will be executed; 
- no other conditions or bodies are evaluated.
- If the first condition fails
- then the process continues in similar manner with the evaluation of the second condition. 
- The execution of this overall construct will cause precisely one of the bodies to be executed.

How many elif clauses can there be? 
There may be any number of elif clauses (including zero)

Do i have to have a final else clause?
- the final else clause is optional. 
As described on page 7, nonboolean types may be evaluated as Booleans with intuitive meanings. 
For example, if response is a string that was entered by a user, and we want to condition a behavior on this being a nonempty string, we may write
```python
# shorthand
response = str(input())
if response:
    pass
    
# longhand
if response != '':
    pass
```
>Another example
```python
class UserResponse:

    def __init__(self):
        pass

    def user_name(self):
        user_input = input()
        if user_input:
            print('your name is {}'.format(user_input))
        elif user_input == '':
            print('what is your name damnit')

# instantiate the class and watch the wizardry
q = UserResponse()
q.user_name()

```
###  1.2. <a name='NestingifStatements'></a>Nesting if Statements

How does python execute handle nested conditional constructs?
- We may nest one control structure within another relying on indentation to make clear the extent of the various bodies.
```python
class DoorMan:
    """ Use the DoorMan to get through the building """

    def __init__(self, name, state=False):
        """ instantiate DoorMan """
        self.name = name
        self.state = state

    def set_state(self, state=False):
        """ state of the door must be a boolean """
        self.state = state

    def door_is_closed(self):
        if self.state:
            print('doors open')
        else:
            print('doors closed')

    def door_is_locked(self):
        if self.state:
            print('door is locked')
        else:
            print('door is not locked')

    def unlock_door(self):
        if self.state:
            print('unlocking door')
        else:
            print('door is unlocked')

    def open_door(self):
        if self.state:
            print('opening door')
        else:
            print('door is already open so no need to open it')

    def advance(self):
        if self.state:
            print('advancing')
        else:
            print('cant advance')


# run my program
if __name__ == '__main__':
    q = DoorMan('quincy')
    q.set_state(False)
    if q.door_is_closed():
        if q.door_is_locked():
            q.unlock_door()
        q.open_door()
    q.advance()
```

###  1.3. <a name='Loops'></a>Loops  
looping constructs in python are:
1. while loop 
- allows general repetition based upon the repeated testing of a Boolean condition. 
2. for loop 
- provides convenient iteration of values from a defined series string, list, range)

###  1.4. <a name='Whileloopsyntax'></a>While loop syntax

> While loop syntax
```python
while (condition):
    body
```

What does the condition evaluate to?
- condition is a boolean expression

Explain the while loops execution pattern.
- The execution of a while loop begins with a test of the Boolean condition. 
- If that condition evaluates to True, the body of the loop is performed.
- After each execution of the body, the loop condition is retested
- If it evaluates to True, another iteration of the body is performed. 
- When the conditional test evaluates to False (assuming it ever does), the loop is exited and the flow of control continues just beyond the body of the loop.

Does a while loop support nested constructs?
- nested control constructs can be placed inside the while loop

> Example: loop a sequence of characters until finding an entry with value X or reaching the end of the sequence.
```python
j=0
while j < len(data) and data[j] !=   X :
j += 1
```

The `len` function returns the length of a sequence such as a `list` or `string`. 
We test `j < len(data)` to ensure that `j` is a valid index, prior to accessing element `data[j]`. 
- Had we written that compound condition with the opposite order, the evaluation of `data[j]` would eventually raise an `IndexError` when `X` is not found.
- variable j’s value will be the index of the leftmost occurrence of `X`, if found, or otherwise the length of the sequence (which is recognizable as an invalid index to indicate failure of the search). 
- NOTE: if the condition `j < len(data)` initially fail the body of the loop will never be executed.

###  1.5. <a name='ForLoops'></a>For Loops

- The for-loop syntax can be used on any type of iterable structure (`list`, `tuple`, `str`, `set`, `dict`, or `file` 
- Its general syntax appears as follows.
```python
for element in iterable:
    # body may refer to element as an identifier
    body
```
> simple example
```py
total = 0
for val in data:
total += val
```
- The loop body executes once for each element of the data sequence, with the iden- tifier, val, from the for-loop syntax assigned at the beginning of each pass to a respective element. 
> It is worth noting that `val` is treated as a standard identifier. 
- If the element of the original data happens to be mutable, the `val` identifier can be used to invoke its methods.

###  1.6. <a name='Index-BasedForLoops'></a>Index-Based For Loops
> What is some limitations of the for loop over elements of a list?
1. we do not know where an element resides within the sequence.

> Suppose that we want to know where the maximum element in a list resides.
- use the range function to generate an integer sequence. 
- the syntax range(n) generates the series of n values from 0 to n − 1. 
- Conveniently, these are precisely the series of valid indices into a sequence of length n. 
- Therefore, a standard Python idiom for looping through the series of indices of a data sequence uses a syntax
```python
for j in range(len(data)):
```
- In this case, identifier `j` is not an element of the data—it is an integer. 
- But the expression `data[j]` can be used to retrieve the respective element. 
> example, find the index of the maximum element of a list as follows:
```python
data = [1, 34, 54, 345, 65]
big_index = 0
for j in range(len(data)):
    if data[j] > data[big_index]:
        big_index = j
print('the largest number is {0} and resides at {1}'.format(data[big_index], big_index))
# returns: the largest number is 345 and resides at 3
```
###  1.7. <a name='BreakandContinueStatements'></a>Break and Continue Statements
- A `break` statement immediately terminates a `while` or `for loop` when executed within its body. 
- if applied within nested control structures, it causes the termination of the **most immediately enclosing `loop`**. 
- As a typical example, here is code that determines whether a target value occurs in a data set:

```python

found = False 
for item in data:
    if item == target: 
        found = True 
        break

''' put it to the test '''
data = ['lord of the rings', 'twin towers', 'peter rabbit']
target = str(input('What is the move your looking for? '))
found = False
for item in data:
    if item == target:
        print('ill you wanna watch {}'.format(item))
        found = True
        break

if found:
    print('hope you like it')
else:
    print('didnt find what you were looking for')
```

- Python also supports a `continue` statement 
- causes the current iteration of a loop body to stop
- subsequent passes of the loop will then proceed as expected.

What is the recommend usage of `break` and `continue`?
- We recommend that the break and continue statements be used sparingly. 
- Yet, there are situations in which these commands can be effectively used to avoid in- troducing overly complex logical conditions.

##  2. <a name='Functions'></a>Functions

> What is the distinction between functions and methods?
- function describes a traditional, stateless function that is invoked without the context of a particular class or an instance of that class). 
- method describes a member function that is invoked upon a specific object using an object-oriented message passing syntax, such as data.sort(). 

> The following function counts the number of occurrences of a given target value within any form of iterable data set.
```python
def count(data, target):
    """ count the number of occurrences of a given target value within iterable """
    n = 0
    for item in data:
        if item == target:
            n += 1
    return n

number_list = [1, 2, 4, 4, 4]

results = count(number_list, 4)
print('the target item occurs {} times'.format(results))
```
> A function's signature is the first line of the function beginning with the keyword `def` establishing:
- a new identifier as the name of the function (count, in this example)
- the number of parameters that it expects
- the names identifying those **parameters** (`data` and `target`, in this example). 

> A Python signature does not designate the `types` of its  parameters nor the `type` (if any) of a `return` value. 
- Those expectations should be stated in the function’s documentation and can be enforced within the body of the function
- misuse of a function will only be detected at run-time.

> the **body of the function** is the reamainder of the function definition
- The body of a function is expressed as an indented block of code. 

> Each time a function is called, Python creates a dedicated activation record that stores information relevant to the current call. 
- This activation record includes what is known as a *namespace* to manage all identifiers that have local scope within the current call. 

> The namespace includes the function’s parameters and any other identifiers that are defined locally within the body of the function. 

> An identifier in the local scope of the function caller has no relation to any identifier with the same name in the caller’s scope 
- alternatively identifiers in different scopes may be aliases to the same object. 
- In our first example, the identifier n has scope that is local to the function call, as does the identifier item, which is established as the loop variable.

###  2.1. <a name='ReturnStatement'></a>Return Statement
> A return statement is used within the body of a function to indicate that
- function should immediately cease execution
- an expressed value should be returned to the caller. 

> If a return statement is executed without an explicit argument, the `None` value is automatically returned. 
> Likewise, `None` will be returned if the flow of control ever reaches the end of a function body without having executed a return statement. 

> The return statement can be placed anywhere in the function body
- Often, a return statement will be the final command within the body of the function However
- there can be multiple return statements in the same function
- with conditional logic controlling you can command which one is executed, if any. 

```python
groceries_list = ['eggs', 'bacon', 'sausage']
verify_item = 'sausage'
def contains(data, target):
    for item in data:
        if item == target:
            print(item)
            return True
    return False

print(contains(groceries_list, verify_item))
```

- If the conditional within the loop body is ever satisfied, the `return True` statement is executed and the function immediately ends, with `True` designating that the target value was found. 
- Conversely, if the `for loop` reaches its conclusion without ever finding the match, the final `return False` statement will be executed.

###  2.2. <a name='InformationPassing'></a>Information Passing
1.5.1 Information Passing
> To be a successful programmer, one must have clear understanding of the mechanism in which a programming language passes information to and from a function. 
- In the context of a `function signature`, the `identifiers` used to describe the expected `parameters` are known as `formal parameters`, and the `objects` sent by the `caller` when invoking the function are the `actual parameters`. 

> Parameter passing in Python follows the semantics of the standard assignment statement. 
- When a function is invoked, each identifier that serves as a formal parameter is assigned, in the function’s local scope, to the respective actual parameter that is provided by the caller of the function.

> For example, consider the following call to our count function from page 23: prizes = count(grades, A )
Just before the function body is executed, the actual parameters, grades and   A , are implicitly assigned to the formal parameters, data and target, as follows:
```bash 
data   =   grades   
target =   A
```

###  2.3. <a name='MutableParameters'></a>Mutable Parameters
> Python’s parameter passing model has additional implications when a parameter is a mutable object. 

- Because the formal parameter is an alias for the actual parameter, the body of the function may interact with the object in ways that change its state. 
- Example, the following implementation of a method named scale whose primary purpose is to multiply all entries of a numeric data set by a given factor.

```python
def scale(data, factor):
    for j in range(len(data)):
        data[j] *= factor
```
###  2.4. <a name='DefaultParameterValues'></a>Default Parameter Values
> Python provides the means for functions to support more than one possible calling signature. 
- Such a function is said to be polymorphic (which is Greek for “many forms”). 
- Most notably, functions can declare one or more default values for parameters, thereby allowing the caller to invoke a function with varying numbers of actual parameters. 
- As an artificial example, if a function is declared with signature
```python
def foo(a, b=15, c=27):
```
- there are three parameters
- the last two offer default values. 
- A caller is welcome to send three actual parameters, as in foo(4, 12, 8), in which case the default values are not used. 
- If, on the other hand, the caller only sends one parameter, foo(4), the function will execute with parameters values a=4, b=15, c=27. 
- If a caller sends two parameters, they are assumed to be the first two, with the third being the default. 
- Thus, foo(8, 20) executes with a=8, b=20, c=27. 
>  It is illegal to define a function with a signature such as bar(a, b=15, c) with b having a default value, yet not the subsequent c; 
- if a default parameter value is present for one parameter, it must be present for all further parameters.

```python
def compute_gpa(grades, points={'A+': 4.0, 'A': 4.0, 'A-': 3.67, 
                                'B+': 3.33, 'B': 3.0, 'B-': 2.67,
                                'C+': 2.33, 'C': 2.0, 'C-': 1.67, 
                                'D+': 1.33, 'D': 1.0, 'F': 0.0}):
    num_courses = 0
    total_points = 0
    for g in grades:
        if g in points:
            num_courses += 1
            total_points += points[g]          # a recognizable grade
    return total_points / num_courses


# Student report card
grades = [ 'A', 'B', 'C', 'A']
# lets figure out how well they did shall we
results = compute_gpa(grades)
print(results) # returns 3.25
```

###  2.5. <a name='KeywordParameters'></a>Keyword Parameters
> The traditional mechanism for matching the actual parameters sent by a caller, to the formal parameters declared by the function signature is based on the concept of **positional arguments**. 
- For example, with signature `foo(a=10, b=20, c=30)`, parameters sent by the caller are matched, in the given order, to the formal parameters. 
- An invocation of `foo(5)` indicates that `a=5`, while `b` and `c` are assigned their default values.
> Python supports an alternate mechanism for sending a parameter to a function known as a **keyword argument**. 
- A keyword argument is specified by explicitly assigning an actual parameter to a formal parameter by name. 
- For example, with the above definition of function foo, a call foo(c=5) will invoke the function with parameters a=10, b=20, c=5.
- A function’s author can require that certain parameters be sent only through the keyword-argument syntax. 
- We never place such a restriction in our own function definitions, but we will see several important uses of keyword-only parameters in Python’s standard libraries. 
- As an example, the built-in `max` function accepts a keyword parameter, coincidentally named `key`, that can be used to vary the notion of “maximum” that is used.

```python
print(abs(max(-35, -101, 20, 100, key=abs))) # returns 101
```


##  3. <a name='Consoleinputandoutput'></a>Console input and output
> The [builtin function](https://docs.python.org/3/library/functions.html), print, is used to generate standard output to the console. 
- In its simplest form, it prints an arbitrary sequence of arguments, separated by spaces, and followed by a trailing newline character. 
- For example, the command `print( maroon , 5)` outputs the string maroon `5\n` .
- Note that arguments need not be string instances. 
- A nonstring argument `x` will be displayed as `str(x)`. 
- Without any arguments, the command `print()` outputs a single newline character.

> The print function can be customized through the use of the following keyword parameters 
-  By default, the print function inserts a separating space into the output between each pair of arguments. 
- The separator can be customized by providing a desired separating string as a keyword parameter, sep. 
- For example, colon-separated output can be produced as `print(a, b, c, sep= ':'` ). 
- The separating string need not be a single character; it can be a longer string, and it can be the empty string, sep= , causing successive arguments to be directly concatenated.
- By default, a trailing newline is output after the final argument. 

- An alternative trailing string can be designated using a keyword parameter, end. 
- Designating the empty string `end= ''` suppresses all trailing characters.
- By default, the print function sends its output to the standard console. 
- However, output can be directed to a file by indicating an output file stream (see Section 1.6.2) using file as a keyword parameter

###  3.1. <a name='files'></a>files
> Files are typically accessed in Python beginning with a call to a built-in function, named `open`, that returns a proxy for interactions with the underlying file. 
- For example, the command, `fp = open( sample.txt )`, attempts to open a file named `sample.txt`, returning a *proxy* that allows read-only access to the text file.
- The open function accepts an optional second parameter that determines the access mode. 
- The default mode is `r` for reading. 

- Other common modes are `w` for **writing** to the file (causing any existing file with that name to be overwritten), or `a` for **appending** to the end of an existing file. 
- Although we focus on use of text files, it is possible to work with binary files, using access modes such as `rb` or `wb`.
- When processing a file, the proxy maintains a current position within the file as an offset from the beginning, measured in number of bytes. 
- When opening a file with mode `r` or `w` , the position is initially 0
- if opened in **append mode**, `a`, the position is initially at the end of the file
- The syntax `fp.close()` closes the file associated with proxy `fp`
- This ensures that any written contents are saved. 

```python
# open, write, and save data to the file
with open('results.txt', 'w+') as fp:
    fp.write('hello world')
    fp.close()

# open, read, and close the file.
with open('results.txt') as f:
    lines = f.readlines() # save the files contents in a variable
    fp.close() 
    print(lines) #send the contents to the screen
```

##  4. <a name='ExceptionHandling'></a>Exception Handling 

> Exceptions are unexpected events that occur during the execution of a program. 
- An exception might result from a logical error or an unanticipated situation. 
- In Python, `exceptions` (also known as ***errors***) are objects that are `raised` (or ***thrown***) by code that encounters an unexpected circumstance. 
- The Python interpreter can also `raise` an `exception` should it encounter an unexpected condition, like running out of memory. 
- A `raised` ***error*** may be caught by a surrounding context that ***handles*** the `exception` in an appropriate fashion. 
- If ***uncaught***, an `exception` causes the interpreter to stop executing the program and to report an appropriate message to the console. 

- In this section, we examine the most common error types in Python, the mechanism for catching and handling errors that have been raised, and the syntax for raising errors from within user-defined blocks of code


###  4.1. <a name='CommonExceptionTypes'></a>Common Exception Types
> Python includes a rich hierarchy of [exception classes](https://docs.python.org/3/library/exceptions.html#exception-hierarchy) that designate various categories of errors; 
- The **Exception** class serves as a base class for most other error types. 
- An instance of the various subclasses encodes details about a problem that has occurred. 
- Several of these errors may be raised in exceptional cases by behaviors introduced in this chapter. 
- For example, use of an undefined identifier in an expression causes a `NameError`, and errant use of the dot notation, as in foo.bar(), will generate an `AttributeError` if object foo does not support a member named bar

- Sending the wrong number, type, or value of parameters to a function is another common cause for an exception. 
For example, a call to `abs( hello )` will raise a `TypeError` because the parameter is not numeric, and a call to `abs(3, 5)` will raise a `TypeError` because one parameter is expected. 
- A `ValueError` is typically raised when the correct number and type of parameters are sent, but a value is illegitimate for the context of the function. 
- For example, the `int` ***constructor*** accepts a ***string***, as with;
```python 
        int( '137' )
```
- but a `ValueError` is `raised` if that ***string*** does not represent an `integer`, as with; 
```python
        int( '3.14' )
        #or 
        int( 'hello' ).
```
- Python’s sequence types (e.g., `list`, `tuple`, and `str`) `raise` an `IndexError` when syntax such as `data[k]` is used with an integer `k` that is not a valid index for the given sequence. 
- `sets` and `dictionaries` raise a `KeyError` when an attempt is made to access a nonexistent element.

###  4.2. <a name='RaisinganException'></a>Raising an Exception
> An exception is thrown by executing the `raise` statement, with an appropriate instance of an `exception` class as an argument that designates the problem. 
- For example, if a function for computing a square root is sent a negative value as a parameter, it can `raise` an `exception` with the command:
```python
        raise ValueError( 'x cannot be negative' )
```
- This syntax raises a newly created instance of the `ValueError` class, with the error message serving as a parameter to the constructor. 
- If this `exception` is not caught within the body of the function, the `execution` of the function immediately ceases and the `exception` is propagated to the calling context (and possibly beyond).
- When checking the validity of parameters sent to a function, it is customary to first verify that a parameter is of an appropriate type, and then to verify that it has an appropriate value. 
- For example, the `sqrt` function in Python’s `math` library performs error-checking that might be implemented as follows:
```python
def sqrt(x):
""" note the tuple of allowable types"""
    if not isinstance(x, (int, float)):
        raise TypeError( 'x must be numeric' ) 
    elif x < 0:
        raise ValueError( 'x cannot be negative' ) 
    # do the real work here...
```
Whats happening here?
> Checking the type of an object can be performed at run-time using the built-in function, `isinstance`. 
- In simplest form, `isinstance(obj, cls)` returns `True` if `object`, `obj`, is an instance of class, `cls`, or any ***subclass*** of that type. 
- In the above example, a more general form is used with a `tuple` of allowable types indicated with the second parameter. 
- After confirming that the parameter is numeric, the function enforces an expectation that the number be nonnegative, raising a `ValueError` otherwise.

###  4.3. <a name='CatchinganException'></a>Catching an Exception
- There are several philosophies regarding how to cope with possible exceptional cases when writing code. 
- For example, if a **division x/y** is to be computed, there is clear risk that a `ZeroDivisionError` will be raised when variable `y` has value `0`. 
- In an ideal situation, the logic of the program may dictate that `y` has a nonzero value, thereby removing the concern for error. 
- However, for more complex code, or in a case where the value of `y` depends on some external input to the program, there remains some possibility of an error.
> One philosophy for managing exceptional cases is to **look before you leap.** 
- The goal is to entirely avoid the possibility of an exception being raised through the use of a **proactive conditional test**. 
```python
def y != 0
    ratio = x / y
else:
    # ...do something else...
```
- Revisiting our division example, we might avoid the offending situation by writing;
```python
try:
    ratio = x / y
except: ZeroDivisionError:
    # ...do something ele...
```
- the `try` block is the primary code to be executed.
- Following the try-block are one or more `except` cases
- each `except` case has its own 
    - identified error type 
    - indented block of code that should be executed if the designated error is raised within the try-block.
- The advantage of using a `try-except` structure is that the non-exceptional case runs efficiently, without extraneous checks for the exceptional condition. 
- However, handling the exceptional case requires slightly more time when using a `try-except` structure than with a standard conditional statement. 
> the `try-except` clause is best used when
- 1. There is reason to believe that the exceptional case is relatively unlikely
- 2. when it is prohibitively expensive to proactively evaluate a condition to avoid the exception (e.g. why the file didn't open)

> Exceptions are objects that can be examined when caught. 
- To do so, an identifier must be established with a syntax as follows:
```python
try:
    fp = open( sample.txt )
except IOError as e:
    print( Unable to open the file: , e)

# returns: Unable to open the file: [Errno 2] No such file or directory: 'sample.txt'
```
-  The name, `e`, denotes the **instance of the `exception` that was thrown**, and printing it causes a detailed error message to be displayed (e.g., “file not found”).

> A try-statement may handle more than one type of `exception`. 
- For example, consider the following;
```python
        age = int(input( 'Enter your age in years:   '))
```
- This command could fail if 
- 1. The call to input fails. 
- 2. If the user has not entered a valid `integer`. 
> If we want to handle two or more types of errors in the same way, we can use a single `except-statement`, as in the following example:
```python
age = -1  # an initially invalid choice while age <= 0:
while age <= 0:
    try:
        age = int(input( 'Enter your age in years: '))
        if age <= 0:
            print( 'Your age must be positive' )
        else:
            print('You entered: ' + str(age))
    except (ValueError, EOFError):
        print( 'Invalid response')
```
- The tuple, `(ValueError, EOFError)` designates the types of errors that we wish to catch with the `except-clause`. 
- In this implementation, we catch either error, print a response, and continue with another pass of the enclosing while loop. 
>  When an error is raised within the `try-block`, the remainder of that body is immediately skipped. 
- In this example, if the exception arises within the call to `input`, or the subsequent call to the **`int`** ***constructor***, the assignment to `***age***` never occurs, nor the message about needing a positive value. continue. 
- If we preferred to have the while loop continue without printing the Invalid response message, we could have written the exception-clause as
```python 
except (ValueError, EOFError): 
    pass
```
> The keyword, **`pass`**, is a statement that does nothing, yet it can serve syntactically as a body of a control structure. 
- In this way, we ***quietly catch the exception***, thereby allowing the surrounding **`while`** loop to **`continue`**.

- It is permissible to have a final except-clause without any identified error types, using syntax `except:`, to catch any other exceptions that occurred. 
- However, this technique should be used sparingly, as it is difficult to suggest how to handle an error of an unknown type. 
- A try-statement can have a **`finally`** clause, with a body of code that will always be executed in the standard or exceptional cases, even when an ***uncaught*** or ***re-raised*** exception occurs. 
> That **`finally`** block is typically used for critical cleanup work, such as closing an open file.


