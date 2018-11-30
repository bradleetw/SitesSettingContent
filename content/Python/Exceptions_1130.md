---
title: "[Python] Exceptions: An introductions"
date: 2018-11-30T10:01:10+08:00
draft: false
tags:
    ["PythonGeneral"]
categories:
    - Python
authors: ["bradlee"]
toc: true
---
Refer to https://realpython.com/python-exceptions/

# Raising an Exception
Example

```python
x = 10
if x > 5:
    raise Exception('x should not exceed 5.')
```

# The AssertionError Exception
refer to https://dbader.org/blog/python-assert-tutorial

Python’s assertions are a **powerful debugging tool** that’s frequently underused by Python developers.

## What is the assert
If the condition is `True`, it does nothing and your program just continues to execute.

But if the assert condition evaluates to `False`, it raises an `AssertionError` exception with an optional error message.

```python
assert( x < 5 )
```
```python
assert( x < 5 ), 'x should not exceed 5.'
```
```python
import sys
assert ('linux' in sys.platform), "This code runs on Linux only."
```

## When use assert statement
The proper use of assertions is to inform developers about **unrecoverable** errors in a program.

Another way to look at it is to say that assertions are **internal self-checks** for your program.

Python’s assert statement is a **debugging aid, not a mechanism for handling run-time errors**. The goal of using assertions is to let developers find the likely root cause of a bug more quickly. An assertion error should never be raised unless there’s a bug in your program.

## Common Pitfalls With Using Asserts in python
### Don't Use Asserts for Data Validation
Asserts can be turned off globally in the Python interpreter. Don’t rely on assert expressions to be executed for data validation or data processing.

How to turn off globally in the Python interpreter? https://docs.python.org/3/using/cmdline.html#cmdoption-o

With `-O`: Remove assert statements and any code conditional on the value of **__debug__**.

### Asserts That Never Fail
When you pass a tuple as the first argument in an assert statement, the assertion always evaluates as true and therefore never fails.

# The `try` and `except` Block: Handling Exceptions
(1) **try** clause: Run this code

(2) **except** clause: Execute this code when there is an exception

(3) **else** clasue: No exceptions? Run this code

(4) **finally** clause: Always run this code.

Example
```python
try:
    linux_interaction()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
finally:
    print('Cleaning up, irrespective of any exceptions.')
```

# Summary
- **raise** allows you to throw an exception at any time.
- **assert** enables you to verify if a certain condition is met and throw an exception if it isn’t.
- In the **try** clause, all statements are executed until an exception is encountered.
- **except** is used to catch and handle the exception(s) that are encountered in the try clause.
- **else** lets you code sections that should run only when no exceptions are encountered in the try clause.
- **finally** enables you to execute sections of code that should always run, with or without any previously encountered exceptions.
