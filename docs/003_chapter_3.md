# Chapter 3 - Functions

In the context of programming, a function is a named sequence of statements that performs
a computation.
When you define a function, you specify the name and the sequence of
statements.
Later, you can "call" the function by name.

## Function calls

We have already seen one example of a function call:

```python linenums="1"
>>> type(42)
<class 'int'>
```

The name of the function is type.
The expression in parentheses is called the argument of the function.
The result, for this function, is the type of the argument.

It is common to say that a function "takes" an argument and "returns" a result.
The result is also called the **return value**.
Python provides functions that convert values from one type to another.
The `int` function takes any value and converts it to an integer, if it can, or complains otherwise:

```python linenums="1"
>>> int('32')
32
>>> int('Hello')
ValueError: invalid literal for int(): Hello
```

The `int` function can convert floating-point values to integers, but it doesn’t round off.
It chops off the fraction part:

```python linenums="1"
>>> int(3.99999)
3
>>> int(-2.3)
-2
```

The `float` function converts integers and strings to floating-point numbers:

```python linenums="1"
>>> float(32)
32.0
>>> float('3.14159')
3.14159
```

Finally, the `str` function converts its argument to a string:

```python linenums="1"
>>> str(32)
'32'
>>> str(3.14159)
'3.14159'
```

## Math functions

Python has a math module that provides most of the familiar mathematical functions.
A **module** is a file that contains a collection of related functions.
Before we can use the functions in a module, we have to import it with an **import statement**:

```python linenums="1"
>>> import math
```

This statement creates a **module object** named math.
If you display the module object, you get some information about it:

```python linenums="1"
>>> math
<module 'math' (built-in)>
```

The module object contains the functions and variables defined in the module.
To access one of the functions, you have to specify the name of the module and the name of the function, separated by a dot (also known as a period).
This format is called **dot notation**.

```python linenums="1"
>>> import math
>>> ratio = signal_power / noise_power
>>> decibels = 10 * math.log10(ratio)

>>> radians = 0.7
>>> height = math.sin(radians)
```

The first example uses the `math.log10` function to compute a signal-to-noise ratio in decibels (assuming that signal_power and noise_power are defined).
The math module also provides `log`, which computes logarithms base `e.`

The second example finds the sine of radians.
The variable name radians is a hint that `sin` and the other trigonometric functions (`cos`, `tan`, etc.) take arguments in radians.
To convert from degrees to radians, divide by `180` and multiply by `π`:

```python linemuns="1"
>>> degrees = 45
>>> radians = degrees / 180.0 * math.pi
>>> math.sin(radians)
0.707106781187
```

The expression `math.pi` gets the variable `pi` from the math module.
Its value is a floatingpoint approximation of `π`, accurate to about 15 digits.

If you know trigonometry, you can check the previous result by comparing it to the square
root of two, divided by two:

```python linemuns="1"
>>> math.sqrt(2) / 2.0
0.707106781187
```

##  Composition

So far, we have looked at the elements of a program (variables, expressions, and
statements) in isolation, without talking about how to combine them.
One of the most useful features of programming languages is their ability to take small
building blocks and compose them.
For example, the argument of a function can be any kind of expression, including arithmetic operators:

```python linemuns="1"
x = math.sin(degrees / 360.0 * 2 * math.pi)
```

And even function calls:

```python linemuns="1"
x = math.exp(math.log(x+1))
```

Almost anywhere you can put a value, you can put an arbitrary expression, with one exception: the left side of an assignment statement has to be a variable name.
Any other expression on the left side is a syntax error (we will see exceptions to this rule later).

```python linenums="1"
>>> minutes = hours * 60 # right
>>> hours * 60 = minutes # wrong!
SyntaxError: can't assign to operator
```

## Adding new functions

So far, we have only been using the functions that come with Python, but it is also possible
to add new functions.
A **function definition** specifies the name of a new function and the
sequence of statements that run when the function is called.
Here is an example:

```python linenums="1"
def print_lyrics():
  print("I'm a lumberjack, and I'm okay.")
  print("I sleep all night and I work all day.")
```

The `def` is a keyword that indicates that this is a function definition.
The name of the function is `print_lyrics`.
The rules for function names are the same as for variable names: letters,
numbers and underscore are legal, but the first character can’t be a number.
You can’t use a keyword as the name of a function, and you should avoid having a variable and a function with the same name.

The empty parentheses after the name indicate that this function doesn’t take any arguments.
The first line of the function definition is called the header.
The rest lines are called the body.
The header has to end with a colon and the body has to be indented.
By convention, indentation is always four spaces.
The body can contain any number of statements.

The strings in the print statements are enclosed in double quotes.
Single quotes and double quotes do the same thing.
Most people use single quotes except in cases like this, where a single quote (which is also an apostrophe) appears in the string.

All quotation marks (single and double) must be "straight quotes", like the ones in this sentence.
"Curly quotes" (`“ ”`), are not legal in Python.

If you type a function definition in interactive mode, the interpreter prints dots (`...`) to let you know that the definition isn’t complete:

```python linenums="1"
>>> def print_lyrics():
... print("I'm a lumberjack, and I'm okay.")
... print("I sleep all night and I work all day.")
...
```

To end the function, you have to enter an empty line.
Defining a function creates a **function object**, which has type function:

```python linemuns="1"
>>> print(print_lyrics)
<function print_lyrics at 0xb7e99e9c>
>>> type(print_lyrics)
<class 'function'>
```

The syntax for calling the new function is the same as for built-in functions:

```python linemuns="1"
>>> print_lyrics()
I'm a lumberjack, and I'm okay.
I sleep all night and I work all day.
```

Once you have defined a function, you can use it inside another function.
For example, to repeat the previous refrain, we could write a function called `repeat_lyrics`:

```python linemuns="1"
def repeat_lyrics():
  print_lyrics()
  print_lyrics()
```

And then call `repeat_lyrics`:

```python linemuns="1"
>>> repeat_lyrics()
I'm a lumberjack, and I'm okay.
I sleep all night and I work all day.
I'm a lumberjack, and I'm okay.
I sleep all night and I work all day.
```

But that’s not really how the song goes.

## Definitions and uses

Pulling together the code fragments from the previous section, the whole program looks
like this:

```python linemuns="1"
def print_lyrics():
  print("I'm a lumberjack, and I'm okay.")
  print("I sleep all night and I work all day.")

def repeat_lyrics():
  print_lyrics()
  print_lyrics()

repeat_lyrics()
```

This program contains two function definitions: `print_lyrics` and `repeat_lyrics`.
Function definitions get executed just like other statements, but the effect is to create function objects.
The statements inside the function do not run until the function is called, and the
function definition generates no output.

As you might expect, you have to create a function before you can run it.
In other words, the function definition has to run before the function gets called.
As an exercise, move the last line of this program to the top, so the function call appears
before the definitions.
Run the program and see what error message you get.
Now move the function call back to the bottom and move the definition of `print_lyrics`
after the definition of `repeat_lyrics`. What happens when you run this program?
