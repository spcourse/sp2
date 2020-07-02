# Package

## Goal

Create a package for the functions you created in the previous assignment.

## Why?

The functions `my_map`, `my_filter`, and `my_reduce` are very general (i.e., they could be used in many different context). In fact most of the typical manipulations of list that you find in actual programs could be expressed in terms of those functions. So it make sense to create a package to bundle those functions together. This way it will become easier to reuse them in other projects.

## Specification

1. Move the functions my_map, my_filter, and my_reduce to a new package called `functional`.
2. Create a file `test-ftools.py`in the module directory to test the package (see below).
3. Add documentation to the package (see below).

## Testing

For the file `test-ftools.py` and copy the code below. If you created the package correctly, this code should work as is.

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

If everything went right you should get the following output:

    # python test-ftools.py
    [1, 2, 3, 4, 5]
    [5, 4, 3, 2, 1]
    [5, 4, 2, 1]
    5421

## Documentation

Make sure that you document the package in such a way that pydoc can automatically extract the right information. The pydoc documentation should look something like this:

    # pydoc functional

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

If your package contains sub-modules, like in our case the module `tools`, make sure those modules are correctly documented as well. For example:

    # pydoc functional.tools
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

There are many ways to write documentation, but a very popular style is NumPy style documentation. Have a look at some examples [here](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_numpy.html) and use this style of documentation.
