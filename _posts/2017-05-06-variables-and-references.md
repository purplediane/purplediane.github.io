---
layout: post
title:  "Variables and References in Python"
date:   2017-05-6 12:01:01
categories: Python
excerpt: "How does Python handle variables and what are references?"
---
<small><span style="color: #555;"><strong>Note: </strong>I started out writing this material for my students after getting questions about the way strange things sometimes happen with lists in Python. After working on it for a while, I decided it made more sense to put it on my blog.</span></small>

Sometimes, it's nice to imagine variables as buckets that contain the data in the variable.  In Python, however, variables aren't really the actual objects, but ***references*** to the objects. Think of the variable as a handle of the bucket and not the bucket itself.

Say you have a variable `x` that is a list; when you do `y = x`, you are just making a **new variable reference** to the same list object that `x` points to. Both `x` and `y` are handles of the same bucket.

### Mutable vs. Immutable Objects ###

Lists, dictionaries, and sets are *mutable* objects. That means they can be modified. The basic data types, integers, floats, tuples, and even strings, are all *immutable* data types, and cannot be changed. If you think you are modifying an object of an immutable type, be assured that what really happens is *a new object is created and the variable is changed to reference the new object*.

**Increment vs. Assignment**

The `+=` ("increment") operator behaves differently than the `=` ("assignment") operator when the left-side variable type is mutable (for example, a list). The `+=` operator modifies the underlying object in place, *without changing the reference*. The variable uses the same handle to the bucket.

The `=` operator is different. When there is an `=` operator, the *entire* right side of the assignment is evaluated and the result is assigned to the left side, so the variable will reference a *new object*. The old handle is thrown away, and the variable gets a new handle to a new bucket.

Let's see some examples:

```python
>>> x = [1, 2, 3]
>>> y = x
>>> x == y
True
>>> x is y
True
>>> id(x)
4315345416
>>> id(y)
4315345416
```

The `id()` function tells you the memory location of the object. You can see here that variables `x` and `y` reference the same object. The `is` operator returns yes, if the objects have the same id.

```python
>>> y += [3, 2, 1]
>>> x == y
True
>>> y is x
True
>>> id(y)
4315345416
>>> x
[1, 2, 3, 3, 2, 1]
>>> y
[1, 2, 3, 3, 2, 1]
```

This is not what most people would expect to happen here; why should `x` change too. Note that the id of `y` did not change with the use of the increment operator. Now let's see what happens here:

 ```python
>>> x = [1, 2, 3]
>>> y = x
>>> y is x
True
>>> y = y + [3, 2, 1]
>>> y is x
False
>>> y == x
False
>>> id(x)
4315345416
>>> id(y)
4315362824
>>> x
[1, 2, 3]
```

Now `y` and `x` are not equal, nor are they the same according to the "is" operator, because the id of `y` is now different. The use of the assignment operator caused `y` to get a new reference.

```python
>>> x = [1, 2, 3]
>>> z = [1, 2, 3]
>>> x == z
True
>>> x is z
False
```

Here, `z` and `x` are equal, but they are not referencing the same object. **This is why you should never use the "is" operator to check if things are equal**; because you will probably get the wrong answer! The only time you should use "is" is when you are comparing to the special singleton variables `None`, `True`, and `False`. They are always in the same location, and any variable that is equal to one of these is referencing the same location.

If you want to make a *copy* of a list so you can manipulate them independently, use the `list` constructor:

```python
>>> x = [1, 2, 3]
>>> y = list(x)
>>> y is x
False
>>> x == y
True
>>> y += [3, 2, 1]
>>> x
[1, 2, 3]
```

In this case, we can increment `y` without affecting `x` because they were never the same object.

### More Examples with Matrices ###

A matrix is a 2-dimensional list of numbers. In Python, we can use lists of lists to represent them. For example:

```python
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

Say we want to create a 3 by 3 matrix initialized to zero. How would you do this?

Let's try a few things with lists. What happens when we do this?

```python
>>> [0] * 3
[0, 0, 0]
```

That looks promising. Let's create our matrix!

```python
>>> matrix = [[0] * 3] * 3
>>> matrix
[[0, 0, 0], [0, 0, 0], [0, 0, 0]]
```

Raise your hand if you like that result! What if we want to change a value in the matrix? How about changing the middle value to 1:

```python
>>> matrix[1][1] = 1
```

So let's see what `matrix` is now:

```python
>>> matrix
[[0, 1, 0], [0, 1, 0], [0, 1, 0]]
```

Wait, what? How did this happen? It's that crazy old bucket vs. reference thing again. When we created `matrix`, the system created 3 references to the list `[0] * 3`. So when we changed the middle value, it appears to change all 3 of the middle lists, but really there is only one physical list, with 3 references to it.

How to create the matrix correctly? We could try:

```python
>>> matrix = [0, 0, 0] * 3
>>> matrix
[0, 0, 0, 0, 0, 0, 0, 0, 0]
>>> matrix = [[0, 0, 0]] * 3
>>> matrix
[[0, 0, 0], [0, 0, 0], [0, 0, 0]]
>>> matrix[1][1] = 1
>>> matrix
[[0, 1, 0], [0, 1, 0], [0, 1, 0]]
```

But that doesn't work either! To create the matrix correctly, we can use a list comprehension:

```python
>>> matrix = [[0] * 3 for n in range(3)]
>>> matrix
[[0, 0, 0], [0, 0, 0], [0, 0, 0]]
>>> matrix[1][1] = 1
>>> matrix
[[0, 0, 0], [0, 1, 0], [0, 0, 0]]
```

Hooray, it works!

### More Dire Warnings 🙄 ###

Note that this reference issue is not just on lists! I used lists as examples because they are easy to read. Any other mutable data type, including dictionaries and sets will have this issue too if you are not careful.

You need to be careful when passing mutable objects to functions. Or rather, you need to be careful when you are writing functions that accept mutable objects, because the variables you receive are just references . You don't want to do anything that might modify the objects passed into the function.

Let's see a completely contrived example. Consider this function:

```python
>>> def changeit(iterable):
...     my_vars = iterable
...     my_vars[0] = 1.234
...
>>> nums = [1, 2, 3, 4]
>>> changeit(nums)
>>> nums
[1.234, 2, 3, 4]
>>>
```

Even though it appears that it is modifying a local copy of the input iterable, it is actually modifying one of the items of the input.

All this brings up another warning: **Do not use mutable objects such as lists or dictionaries as defaults in functions!** Once they get changed, they don't revert back to an empty default. For example, Allen Downey shows a great example of this problem in his book [Think Python][thinkpython], with the problem [Bad Kangaroo - exercise 2 on this page][badkangaroo]. An empty list is used as the default for a parameter to the `__init__` method. This is OK for the first instance created, but the next instance receives the SAME reference value, and therefore the contents of the lists are the same.

Here are some StackOverflow questions - it is a common Python confusion issue, and there are many more:

1. [How to copy a dictionary and only edit the copy][so1]
1. [Function which returns dictionary overwriting all dictionaries][so2]
1. [Original arguments get overwritten][so3]

Hope this helps! If you have comments, please DM me on Twitter!

[thinkpython]: https://www.amazon.com/gp/product/1491939362/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491939362&linkCode=as2&tag=greenteapre01-20&linkId=QGWNVBOEV6JIMH4Y
[badkangaroo]: http://greenteapress.com/thinkpython2/html/thinkpython2018.html#sec208
[atom]: https://atom.io/
[so1]: http://stackoverflow.com/questions/2465921/how-to-copy-a-dictionary-and-only-edit-the-copy
[so2]: http://stackoverflow.com/questions/43564986/function-which-returns-dictionary-overwriting-all-dictionaries/
[so3]: http://stackoverflow.com/questions/20550473/original-arguements-get-overwritten
