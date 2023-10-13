---
layout: post
title:  "Copy and Paste-able Python List Comprehension"
author: Orion Bowers
description: "A simple tutorial on using python list comprehension" 
image: "/assets/images/AIGenerated/FutureTypewriter.png"
---
# Introduction
Have you ever gone out and bought yourself some Scandinavian furniture in a box?
Then you opened the box and found some cool interchangeable pieces, an allen wrench, and no instructions?

Not me. The instructions have been in there every time I've bought furniture (granted, that's not too many times).

But every single time I try to unpack interchangeable parts from a Python list, the instructions are sadly lacking.

This blog post aims to be those quick reference instructions, copy and paste-able as needed.

So let's get into it.

# Section for people who want to copy and paste
Below contains some visuals you can use for constructing your own python lists. Feel free to copy, paste, and edit as needed.
(no allen wrench necessary)

```python
# Simplest List Comprehension
iterable = [1,2,3,4,5,6,7,8,9,10]
def funct(x):
    return x
[funct(item) for item in iterable]

# List Comprehension with condition on iterable
iterable = [1,2,3,4,5,6,7,8,9,10]
def condition(x):
    return x>5 or x%2==0
[item for item in iterable if condition(item)]

# List Comprehension applying a function based on a condition
iterable = [1,2,3,4,5,6,7,8,9,10]
def funct1(x):
    return x
def funct2(x):
    return 0
def condition(x):
    return x>5 or x%2==0
[funct1(item) if condition(item) else funct2(item) for item in iterable]
```

# Section for people who want to know more

For those of you wanting to read this furniture's instructions, I've included 2 types of examples below. Both are fairly simple, but they can get you started making more complex list comprehensions by using the same principles.

Python list comprehension is a fancy way of avoiding using `for` loops or similar devices to fill a list (similar options are available for dictionaries and other iterables). They take less code to write, they're easier to read (once you understand the format), and they often execute faster than a `for` loop.

## Simplest List Comprehension

The simplest list comprehension you can do involves taking a preexisting iterator (lists, tuples, dictionaries, sets, etc) and applying a function to each item in that iterator. For example, you might want to emphasize something by converting a list of strings (like a sentence) to all caps (but still have a list of strings).

```python
sentence = ["putting","together","furniture","is","hard!"]
new_sentence = [word.upper() for word in sentence]
> ['PUTTING', 'TOGETHER', 'FURNITURE', 'IS', 'HARD!']
```

Or round each number in a list to a certain place.

```python
cost_of_new_tables = [39.40,39.40,39.40,65.99]
rounded_costs = [round(num) for num in cost_of_new_tables]
> [39, 39, 39, 66]
```
These are relatively simply functions to perform on the items of our iterables, but what if your function is fairly messy?

You can actually use a function inside list comprehension that will be applied to each item in the iterable.

```python
rounded_costs = [39, 39, 39, 66]
def funct(x):
    return "$"+str(x)
rounded_costs_units = [funct(num) for num in rounded_costs]
> ['$39', '$39', '$39', '$66']

```

Reading this comprehension in English might look something like this:

"For every number in my list, add a $, then add it to my new list as a string."

Or a more general form:

"For every item in my iterable, apply this function to it, then add the result to my new list."


## List Comprehension with Conditions

Let's try something trickier. What if we wanted to filter our iterable so it only contained items that met a condition?

```python
monthly_furniture_costs = [0,20.99, 0, 0, 0, 0, 0, 0, 65.99, 184.19, 33.21, 5.45]
def condition(x):
    return x>0
nonzero_furniture_costs = [item for item in monthly_furniture_costs if condition(item)]
> [20.99, 65.99, 184.19, 20.99, 5.45]
```
You'll want to write the condition after the iterable so it only returns items that meet the condition from that iterable.

What if, instead, we wanted to apply the function based on a condition?

```python
monthly_furniture_costs = [0,20.99, 0, 0, 0, 0, 0, 0, 65.99, 184.19, 33.21, 5.45]
def funct1(x):
    return x
def funct2(x):
    return 0
def condition(x):
    return x>30.00
costs_caused_by_the_cat = [funct1(item) if condition(item) else funct2(item) for item in monthly_furniture_costs]
> [0, 0, 0, 0, 0, 0, 0, 0, 65.99, 184.19, 33.21, 0]
```
Most of the time, instead of defining separate functions, you'll find it's easier to just write the code inside the list comprehension. I've included separate functions in case you do have a more complex operation and want to know how to do it.

## Wrap Up
So that's it, 3 ways to use list comprehension in Python. Hopefully you can walk away feeling a little more confident reading other people's code or writing your own. So get out there and unpack some furniture!

Now if you excuse me, I have to move my cat off the table again.