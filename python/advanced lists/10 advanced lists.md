# Advanced lists

Here we will discuss some more advanced list operations. Previously you learned how to create and manipulate lists, but Python has a lot of useful built-in list operations that we haven't seen before. Let's have a look at some of them:

## 1.1 Basic operations:

The `+` operator concatenates lists:

```
>>> a = [1, 2, 3]
>>> b = [4, 5, 6]
>>> c = a + b
>>> c
[1, 2, 3, 4, 5, 6]
```

The `\*` operator repeats a list a given number of times:

```
>>> [0] * 4
[0, 0, 0, 0]
>>> [1, 2, 3] * 3
[1, 2, 3, 1, 2, 3, 1, 2, 3]
```

The first example repeats `\[0\]` four times. The second example repeats the list `\[1, 2, 3\]` three times.

(source: think python)

## 1.2 Slicing:

A segment of a list is called a **slice**. Selecting a slice is similar to selecting a single element:

```
>>> s = [0, 1, 2, 3, 4, 5, 6, 7]
>>> s[0:4]
[0, 1, 2, 3]
>>> s[4:8]
[4, 5, 6, 7]
```

The operator `\[n:m\]` returns the part of the list from the “n-eth” character to the “m-eth” element, *including the first* but *excluding the last*. This behavior might seem counterintuitive, but it might help to imagine the indices pointing *between* the elements.

If you omit the first index (before the colon), the slice starts at the beginning of the list. If you omit the second index, the slice goes to the end of the list:

```
>>> fruit = ['b','a','n','a','n','a']
>>> fruit[:3]
['b', 'a', 'n']
>>> fruit[3:]
['a', 'n', 'a']
```

If the first index is greater than or equal to the second the result is an **empty list**:

```
>>> fruit = ['b','a','n','a','n','a']
>>> fruit[3:3]
[]

```

Some more examples:

```
>>> t = ['a', 'b', 'c', 'd', 'e', 'f']
>>> t[1:3]
['b', 'c']
>>> t[:4]
['a', 'b', 'c', 'd']
>>> t[3:]
['d', 'e', 'f']
```

If you omit the first index, the slice starts at the beginning. If you omit the second, the slice goes to the end. So if you omit both, the slice is a copy of the whole list.

```
>>> t[:]
['a', 'b', 'c', 'd', 'e', 'f']
```

Since lists are mutable, it is often useful to make a copy before performing operations that modify lists.

A slice operator on the left side of an assignment can update multiple elements:

```
>>> t = ['a', 'b', 'c', 'd', 'e', 'f']
>>> t[1:3] = ['x', 'y']
>>> t
['a', 'x', 'y', 'd', 'e', 'f']
```

(adapted from think python)

## 1.3 Built-in methods

Python provides methods that operate on lists. Some you have seen before. For example, append adds a new element to the end of a list:

```
>>> t = ['a', 'b', 'c']
>>> t.append('d')
>>> t
['a', 'b', 'c', 'd']
```

extend takes a list as an argument and appends all of the elements:

```
>>> t1 = ['a', 'b', 'c']
>>> t2 = ['d', 'e']
>>> t1.extend(t2)
>>> t1
['a', 'b', 'c', 'd', 'e']
```

This example leaves t2 unmodified.

sort arranges the elements of the list from low to high:

```
>>> t = ['d', 'c', 'e', 'b', 'a']
>>> t.sort()
>>> t
['a', 'b', 'c', 'd', 'e']
```

Most list methods are void; they modify the list and return None. If you accidentally write t = t.sort(), you will be disappointed with the result.

(source think python)

If you want a copy of the list instead, you can use the function [`sorted()`](https://docs.python.org/3/library/functions.html#sorted) function. It returns a new sorted list:

```
>>> sorted([5, 2, 3, 1, 4])
[1, 2, 3, 4, 5]
```

An important difference is that the [`list.sort()`](https://docs.python.org/3/library/stdtypes.html#list.sort) method is only defined for lists. In contrast, the [`sorted()`](https://docs.python.org/3/library/functions.html#sorted) function accepts any iterable.

```
>>> sorted({1: 'D', 2: 'B', 3: 'B', 4: 'E', 5: 'A'})
[1, 2, 3, 4, 5]
```

Both [`list.sort()`](https://docs.python.org/3/library/stdtypes.html#list.sort) and [`sorted()`](https://docs.python.org/3/library/functions.html#sorted) have a *key* parameter to specify a function to be called on each list element prior to making comparisons.

For example, here’s a case-insensitive string comparison:

```
>>> sorted("This is a test string from Andrew".split(), key=str.lower)
['a', 'Andrew', 'from', 'is', 'string', 'test', 'This']
```

The value of the *key* parameter should be a function that takes a single argument and returns a key to use for sorting purposes.

(source python.org)

## 1.4 List comprehensions:

Sometimes you want to traverse one list while building another. For example, the following function takes a list of strings and returns a new list that contains capitalized strings:

```
def capitalize_all(t):
    res = []
    for s in t:
        res.append(s.capitalize())
    return res
```

We can write this more concisely using a **list comprehension**:

```
def capitalize_all(t):
    return [s.capitalize() for s in t]
```

The bracket operators indicate that we are constructing a new list. The expression inside the brackets specifies the elements of the list, and the for clause indicates what sequence we are traversing.

The syntax of a list comprehension is a little awkward because the loop variable, s in this example, appears in the expression before we get to the definition.

List comprehensions can also be used for filtering. For example, this function selects only the elements of t that are upper case, and returns a new list:

```
def only_upper(t):
    res = []
    for s in t:
        if s.isupper():
            res.append(s)
    return res
```

We can rewrite it using a list comprehension

```
def only_upper(t):
    return [s for s in t if s.isupper()]
```

List comprehensions are concise and easy to read, at least for simple expressions. And they are usually faster than the equivalent for loops, sometimes much faster. So if you are mad at me for not mentioning them earlier, I understand.

But, in my defense, list comprehensions are harder to debug because you can’t put a print statement inside the loop. I suggest that you use them only if the computation is simple enough that you are likely to get it right the first time. And for beginners that means never.

(source think geek)
