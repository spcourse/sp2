# Package

The functions `my_map`, `my_filter`, and `my_reduce` are very general, they could be used in many different contexts. In fact most of the typical manipulations of list that you find in actual programs could be expressed in terms of only these three functions.

So it make sense to create a package to bundle those functions together into one package. This way it will become easier to reuse them in other projects.

1. Move the functions my_map, my_filter, and my_reduce to a new package called `functional`.
2. Create a file `test-ftools.py`in the module directory to test the package.
3. Add documentation to the package.

For the file `test-ftools.py` copy the code below. If you created the package correctly, this code should work as is.

```
from functional import my_map, my_filter, my_reduce

def rev(x):
	return 6 - x

def not_three(x):
	return x != 3

def stick(x, y):
	return x * 10 + y

numbers1 = [1, 2, 3, 4, 5]
print(numbers1)

numbers2 = my_map(rev, numbers1)
print(numbers2)

numbers3 = my_filter(not_three, numbers2)
print(numbers3)

number = my_reduce(stick, numbers3)
print(number)
```

If everything went right you should get the following output:

```
[1, 2, 3, 4, 5]
[5, 4, 3, 2, 1]
[5, 4, 2, 1]
5421
```

> Add some tests of your own to the file, to convince yourself the functions always work as expected. Think about edge cases: What happens if you provide an empty list as argument? What happens if your function has side effects (like print statements)?

Make sure that you document the package in such a way that `pydoc` can automatically extract the right information.

When running `pydoc functional`, you should see something like this:

After

```
Help on package functional:

NAME
    functional

DESCRIPTION
    This package contains a collection of functional programming tools.
    Also see:
            pydoc functional.tools

PACKAGE CONTENTS
    tools

FILE
    your-home-dir/module6/functional/__init__.py
```

If your package contains sub-modules, like in our case the module `tools`, make sure those modules are correctly documented as well. E.g., `pydoc functional.tools`:

```
NAME
    functional.tools - This module provides a number of classical functional programming tools.

FUNCTIONS
    my_filter(p, l)
        Select all elements from l that yield True for function p.

        Parameters
        ----------
        p : a predicate
                A function that takes a single argument and returns True or False
        l : list
                The list of elements to which p is applied

        Returns
        -------
        list
                A list containing only the elements for which p yields True

    my_map(f, l)
        ...
```

There are many ways to write documentation, you can find some examples [here](https://docs.python-guide.org/writing/documentation/). The most important is consistency: pick one style and stick to it.
