# Python Basics – Lesson Notes
This lesson introduced the foundational concepts of Python programming, focusing on the core skills needed for scripting, automation, and cybersecurity fundamentals.

## Hello World
The very first step was printing text to the screen using the print() function. This classic starting point helps demonstrate how output works in Python.

Example:
print("Hello World")

## Mathematical Operators
Python can be used like a basic calculator. We covered several types of operators:

Arithmetic operators:

for addition

for subtraction

for multiplication
/ for division
% for modulus (remainder)
** for exponents

## Comparison operators:

> greater than
< less than
== equal to
!= not equal to
= greater than or equal to
<= less than or equal to

These are essential when building conditionals and loops.

## Variables and Data Types
Variables are used to store and update information. The common data types we explored include:

String – a sequence of text (example: movie title)
Integer – a whole number (example: number of views)
Float – a decimal number (example: a rating like 4.3)
Boolean – true or false value (example: favorite = True)
List – a group of items (example: list of users who watched a movie)

## Logical and Boolean Operators
Logical operators help compare values, while Boolean operators allow combining multiple conditions.

Logical: ==, <, <=, >, >=
Boolean:
and – both conditions must be true
or – at least one condition must be true
not – reverses the condition's truth value

## Introduction to If Statements
If statements let the program make decisions based on a condition.

Example:
if age < 17:
  print("You are NOT old enough to drive")
else:
  print("You are old enough to drive")

The structure uses indentation to show which lines belong to the condition.

## Loops
Loops repeat actions until a condition is no longer met.

While loop example:
i = 1
while i <= 10:
  print(i)
  i += 1

This will print numbers 1 through 10.

For loop example:
websites = ["facebook.com", "google.com", "amazon.com"]
for site in websites:
  print(site)

This will print each item in the list one at a time.

## Introduction to Functions
Functions are blocks of code that can be reused whenever needed.

Example:
def sayHello(name):
  print("Hello " + name + "! Nice to meet you.")

sayHello("Ben")

This makes the code easier to manage, especially in larger programs.

## Files
Python can read from and write to files. This is useful for scripts that generate or process large amounts of data.

Reading:
f = open("file_name", "r")
print(f.read())

Writing:
f = open("file_name", "w")
f.write("This is some text")
f.close()

Appending:
f = open("file_name", "a")
f.write("Adding more text")
f.close()

## Imports
Python allows importing libraries to extend its functionality. These libraries are either built-in or can be installed with pip.

Examples:
import requests – for making HTTP requests
import scapy – for packet analysis and manipulation
import pwntools – for CTFs and exploit development

To install something like scapy:
pip install scapy

## Summary
This lesson introduced essential Python basics that are commonly used in cybersecurity workflows. Understanding variables, logic, loops, functions, and file handling sets the stage for scripting tasks, automation, and building your own tools in the future.
