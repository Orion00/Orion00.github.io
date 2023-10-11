---
layout: post
title:  "Copy and Paste-able Python List Comprehension"
author: Orion Bowers
description: "A simple tutorial on using python list comprehension" 
image: "/assets/images/AIGenerated/FutureTypewriter.png"
---

# Section for people who want to copy and paste
```python
# Simplest List Comprehension
iterable = [1,2,3,4,5,6,7,8,9,10]
def funct(x):
    return x**2
[funct(item) for item in iterable]

# List Comprehension with condition on iterable
iterable = [1,2,3,4,5,6,7,8,9,10]
def condition(x):
    return x>5 or x%2==0
[item for item in iterable if condition(item)]

# List Comprehension with condition on result of function
iterable = [1,2,3,4,5,6,7,8,9,10]
def funct1(x):
    return x
def funct2(x):
    return x/10
def condition(x):
    return x>5 or x%2==0
[funct1(item) if condition(item) else funct2(item) for item in iterable]
```

# Section for people who want to know more
Have you ever gone out and bought yourself some Scandinavian furniture in a box?
Then you opened the box and found some cool interchangeable pieces, a weird Allen wrench, and no instructions?

Not me. The instructions have been in there every time I've bought furniture (granted, that's not too many times).

But every single time I try to unpack interchangeable parts from a Python list, the instructions are sadly lacking.

This blog post aims to be those quick reference instructions, copy and paste-able as needed.

So let's get into it.

## Simplest List Comprehension

The simplest list comprehension you can do involves taking a preexisting iterator (lists, tuples, dictionaries, sets, etc) and applying a function to each item in that iterator. For example, you might want to emphasize something by converting a list of strings (like a sentence) to all caps (but still a list of strings).

```python
sentence = ["putting","together","furniture","is","hard!"]
new_sentence = [word.upper() for word in sentence]
```

Or round each number in a list to a certain place.

```python
cost_of_new_tables = [39.40,39.40,39.40,65.99]
rounded_costs = [round(num) for num in cost_of_new_tables]
```
These are relatively simply functions to perform on the items of our iterables, but what if your function is fairly messy?

You can actually use a function inside list comprehension that will be applied to each item in the iterable.

```python
rounded_costs = [39, 39, 39, 66]
def funct(x):
    return "$"+str(x)
rounded_costs_units = [funct(num) for num in rounded_costs]

```

Reading this comprehension in English might look something like this:

"For every number in my list, add a $, then add it to my new list as a string.

Or a more general form:

"For every item in my iterable, apply this function to it, then add the result to my new list.

## List Comprehension with condition on iterable

Let's try something trickier. What if we wanted to filter our iterable so it only contained items that met a condition?



