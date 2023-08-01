# Chapter 2 - Variables, expressions and statements

One of the most powerful features of a programming language is the ability to manipulate
**variables**.
A variable is a name that refers to a value.

#### Assignment statements

An assignment statement creates a new variable and gives it a value:

```python linenums="1"
>>> message = 'And now for something completely different'
>>> n = 17
>>> pi = 3.1415926535897932
```

This example makes three assignments.
The first assigns a string to a new variable named `message`; the second gives the integer 17 to `n`; the third assigns the (approximate) value of π to `pi`.
A common way to represent variables on paper is to write the name with an arrow pointing to its value.
This kind of figure is called a state diagram because it shows what state each of the variables is in (think of it as the variable’s state of mind).

The Figure below shows the result of the previous example.

<figure markdown>
<p class="p-center"> State diagram</p>
  ![stage_diagrama](../assets/images/state_diagram.png){ align=center }
</figure>

####  Variable names

Programmers generally choose names for their variables that are meaningful.
Names document what the variable is used for.

Variable names can be as long as you like.
They can contain both letters and numbers, but **they can’t begin with a number**. It is legal to use uppercase letters, but **it is conventional to use only lower case for variables names**.
The underscore character, `_`, can appear in a name.
It is often used in names with multiple words, such as `your_name` or `airspeed_of_unladen_swallow`;
If you give a variable an illegal name, you get a syntax error:

```python linenums="1" hl_lines="1 6 11"
>>> 76trombones = 'big parade' # (1)
  File "<stdin>", line 1
    76trombones = 'big parade'
     ^
SyntaxError: invalid decimal literal

>>> more@ = 1000000 # (2)
  File "<stdin>", line 1
    more@ = 1000000
          ^
SyntaxError: invalid syntax

>>> class = 'Advanced Theoretical Zymurgy' # (3)
  File "<stdin>", line 1
    class = 'Advanced Theoretical Zymurgy'
          ^
SyntaxError: invalid syntax
```

1. :man_raising_hand: `76trombones` is illegal because it begins with a number.
2. :man_raising_hand: `more@` is illegal because it contains an illegal character, `@`.
3. :man_raising_hand: `class` is one of Python’s keywords.

What’s wrong with class?
It turns out that `class` is one of Python’s keywords.
The interpreter uses keywords to recognize the structure of the program, and they cannot be used as variable names.
Python 3 has these keywords:

```python linenums="1"
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

Obs.: Não gostei do código acima.
