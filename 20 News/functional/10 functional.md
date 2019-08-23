# Functional Programming

The functional tools map, reduce and filter are already part of Python, but we're not going to use those. We will create our own versions of those tools.

1. If you haven't done so already, create a new directory for this module (e.g., `module 6`).
2. Create a file tools.py in the module directory.
3. Implement and *test* the function `my_map()`.
4. Implement and *test* the function `my_filter()`.
5. Implement and *test* the function `my_reduce()`.

Of course you're not allowed to use the built-in python versions of these functions. You are however allowed to use those as a reference for your own versions.

Here below you find some examples of how these functions should work.

## Examples of my_map

### Example 1

```
numbers = [1, 2, 3, 4]

def square(x):
 return x * x

def repeat(x):
 return x + 10*x

squared_numbers = my_map(square, numbers)
repeated_numbers = my_map(repeat, numbers)

print(squared_numbers)
print(repeated_numbers)
```

expected output:

```
[1, 4, 9, 16]
[11, 22, 33, 44]
```

### Example 2:

```
story = ['For', 'sale', ':', 'baby', 'shoes', ',', 'never', 'worn', '.']

def initial(x):
 return x[0]

initials = my_map(initial, story)
lengths = my_map(len, story)

print(initials)
```

expected output:

```
['F', 's', ':', 'b', 's', ',', 'n', 'w', '.']
[3, 4, 1, 4, 5, 1, 5, 4, 1]
```

#TODO

## Examples of my_filter

## Examples of my_reduce
