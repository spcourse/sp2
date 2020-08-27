# Functional programming

Functional programming is the process of building software by composing so-called "pure" functions. These functions avoid having interactions outside of their own scope and as such have no side-effects. All these functions do, is somehow transform an input into an output. We will discuss some higher-order functions that abide by the principles of functional programming that can be used to manipulate lists.

When manipulating lists, we often find ourselves writing more or less the same code in different applications. In fact most list operations can be categorized in three main patterns: *map*, *filter* and *reduce*. Here, we will discuss those patterns one by one and understand their use cases.

> Note that in the examples below the functions `my_map`, `my_filter` and `my_reduce` do not exist. Those are purely hypothetical examples.

## Map

Often we want to traverse a list, apply some function to each of the elements and collect the output. For example this program to square all elements:

    >>> def square(x):
    >>>     return x * x

    >>> items = [1, 2, 3, 4, 5]
    >>> squared = []
    >>> for e in items:
    >>>     squared.append(square(e))
    >>> print(squared)
    [1, 4, 9, 16, 25]


Or, this very similar program that doubles all elements:

    >>> def double(x):
    >>>     return x * 2

    >>> items = [1, 2, 3, 4, 5]
    >>> squared = []
    >>> for e in items:
    >>>     squared.append(double(e))
    >>> print(squared)
    [2, 4, 6, 8, 10]

The two examples are almost identical. In fact, only the function that is applied to each element differs. We could say that both examples follow the same *design pattern*. In fact this is such a common pattern there is a special name for it: a *map*. Since this is such a common pattern, it can be convenient to generalize it.

The idea is to have a function `my_map` that applies a function to all the items in an input list, using the following blueprint:

    my_map(function_to_apply, list_of_inputs)


A function like `my_map` would allow us to implement the examples in a much cleaner way.

The first example:

    >>> items = [1, 2, 3, 4, 5]
    >>> squared = my_map(square, items)
    >>> print(squared)
    [1, 4, 9, 16, 25]

The second example:

    >>> items = [1, 2, 3, 4, 5]
    >>> squared = my_map(double, items)
    >>> print(squared)
    [2, 4, 6, 8, 10]

You can see that only the function that is provided to `my_map` differs in both examples.

## Filter

Another common design pattern is a *filter*. A filter selects elements from a list that meet a specific condition. Typically a filter uses a function that returns `True` or `False` for each element from the list. The filter generates a new list with only those elements for which `True` is returned. For example:

    >>> def is_negative(x):
    >>>     return x < 0
    >>>     
    >>> number_list = [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
    >>> less_than_zero = []
    >>> for e in number_list:
    >>>     if is_negative(e):
    >>>         less_than_zero.append(e)
    >>> print(less_than_zero)
    [-5, -4, -3, -2, -1]

Also here, the idea is to generalize this pattern using a function with the following blueprint:

    my_filter(function_to_apply, list_of_inputs)

This function simply applies the provide function to all elements in the list and returns a new list with only those elements for which `True` is returned. Like so:

    >>> number_list = [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
    >>> less_than_zero = my_filter(is_negative, number_list)
    >>> print(less_than_zero)
    [-5, -4, -3, -2, -1]

## Reduce

Often you want to *reduce* a list to one single aggregate element. For example the sum of all the elements in the list:

    >>> def add(x, y):
    >>>     return x + y
    >>>     
    >>> list = [1, 2, 3, 4]
    >>> sum = 0
    >>> for num in list:
    >>>     sum = add(sum, num)
    >>> print(sum)
    10

Or the product of all elements:  

    >>> def mul(x, y):
    >>>     return x * y
    >>>
    >>> list = [1, 2, 3, 4]
    >>> product = 1
    >>> for num in list:
    >>>     product = mul(product, num)
    >>> print(product)
    24

The above example reduces the list to the product of its elements. These examples maintain an accumulator (`sum` and `product` respectively) and iteratively apply a binary function to the accumulator and the next element of the list.

This pattern could also be generalized into a function. Blueprint:

    my_reduce(function_to_apply, list_of_inputs)

Example usage:

    >>> product = my_reduce(mul, [1, 2, 3, 4])
    >>> print(product)
    24

The implementation of this function is a bit trickier then `my_map` and `my_filter`. For one, what is the initial value of the accumulator? If it is `0` it would not work for multiplication, but `1` does not work for addition. The best solution is to initialize the accumulator with the first element of the list and then start applying the function starting with the second element of the list.

## Lambda expressions

When using map, filter and reduce you often need to provide a very simple function like `square` in the example below:

    def square(x):
        return x * x

For creating very simple functions you can use the lambda notation like below:

    >>> square = lambda x : x * x
    >>> print(square(5))
    25

One of the advantages of  having lambda's is that they don't need to be explicitly named first. They can be created on the spot. Which makes it particularly useful to use in combination with map:

    >>> items = [1, 2, 3, 4, 5]
    >>> squared = my_map(lambda x : x * x, items)
    >>> print(squared)
    [1, 4, 9, 16, 25]

Lambda functions can take any number of arguments. Lambda's that take two arguments are useful to use with reduce.

    >>> product = my_reduce(lambda x, y : x * y, [1, 2, 3, 4])
    >>> print(product)
    24

## Summary

All in all, we introduced many ways we could implement the same functionality. For example let's say we want to define a function `only_upper` that selects all strings from a list that are uppercase. We can do this many different ways:

Method 1, classic:

    def only_upper(t):
        res = []
        for s in t:
            if s.isupper():
                res.append(s)
        return res

Method 2, list comprehensions:

    def only_upper(t):
        return [s for s in t if s.isupper()]

Method 3, map:

    def is_upper(s):
        return s.isupper()

    def only_upper(t):
        return map(is_upper, t)

Method 4, map and lambda:

    def only_upper(t):
        return map(lambda s: s.isupper(), t)

So, which is better? That depends on the goal, personal taste, and context. I tend to prefer functional solutions because the resulting code looks cleaner. But I tend to avoid lambda functions because they don't help the readability of the code. So in this case I would probably opt for method 3. But there are many good arguments to make for the other methods. The most important is to be consistent. Try to choose one style of programming and stick to it throughout the project.

## Notes on MapReduce

 >MapReduce is a programming paradigm used in many programming libraries to enable users to apply functions to large swathes of data at once. Since it basically provides a general strategy for split-apply-combine, it enables the library to apply the function in parallel, thereby increasing efficiency by solving parts of the task at the same time before combining results. You will come by multiple Python libraries that utilize it in the future.

 In the coming exercises you will practice with map, reduce, and filter operations extensively. Note that **everything** in these exercises could have also been done with regular for-loops, but the goal of the exercise is to use those as little as possible to train this alternative method of solving problems.
