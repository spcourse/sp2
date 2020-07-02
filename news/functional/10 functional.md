# Functional Programming

## Goal

Implement the functions `my_map`, `my_filter`, and `my_reduce`.

## Specification


1. If you haven't done so already, create a new directory for this module (e.g., `module 6`).
2. Create a file tools.py in the module directory.
3. Implement and *test* the function `my_map()`, `my_filter()`, `my_reduce()` as specified in the previous readings. Make sure that it works for the examples below.

> Note: Python already has similar functions built-in. Of course you're not allowed to use those.

## Examples

### Example 1 (my_map)

    numbers = [1, 2, 3, 4]

    def square(x):
        return x * x

    def repeat(x):
        return x + 10*x

    squared_numbers = my_map(square, numbers)
    repeated_numbers = my_map(repeat, numbers)

    print(squared_numbers)
    print(repeated_numbers)

expected output:

    [1, 4, 9, 16]
    [11, 22, 33, 44]

### Example 2 (my_map):

    tokens = ['For', 'sail:', 'baby', 'schooner,', 'never', 'seen', 'before!']

    def replace(word):
        subs = {'sail:': 'sale:', 'schooner,': 'shoes,', 'seen': 'worn.'}
        new_word = subs.get(word, word)
        return new_word

    new_tokens = my_map(replace, tokens)

    print(new_tokens)

expected output:

    ['For', 'sale:', 'baby', 'shoes,', 'never', 'worn.', 'before!']

### Example 3 (my_filter):

    numbers = [0, -10, 8, 0, 1, -4, -8]

    def negative(x):
        return x < 0

    negative_numbers = my_filter(negative, numbers)
    print(f'Negative: {negative_numbers}')

expected output:

    Negative: [-10, -4, -8]

### Example 4 (my_filter):

    numbers = my_filter(lambda x:  x % 17 == 0, range(100))
    print(f'Divisible by 17: {numbers}')

expected output:

    Divisible by 17: [0, 17, 34, 51, 68, 85]

### Example 5 (my_filter):

    tokens = ['For', 'sale:', 'baby', 'shoes,', 'never', 'worn.', 'before!']

    def no_before(word):
        return word != 'before!'

    new_tokens = my_filter(no_before, tokens)

    print(new_tokens)

expected output:

    ['For', 'sale:', 'baby', 'shoes,', 'never', 'worn.']

### Example 6 (my_reduce):

    negative_numbers = [-10, -4, -8]

    def negative_mul(a, b):
        return -(a * b)

    number = my_reduce(negative_mul, negative_numbers)
    print(number)

expected output:

    -320

### Example 7 (my_reduce):

    tokens = ['For', 'sale:', 'baby', 'shoes,', 'never', 'worn.']

    def join(a, b):
        return a + ' ' + b

    text = my_reduce(join, tokens)
    print(text)

expected output:

    For sale: baby shoes, never worn.
