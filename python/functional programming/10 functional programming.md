# Functional programming

Many modern programming languages like python have the functions map, filter and reduce. These are three functions that facilitate a functional approach to programming. We will discuss them one by one and understand their use cases.

### 2.1 Map

`Map` applies a function to all the items in an input_list. Here is the blueprint:

```
map(function_to_apply, list_of_inputs)
```

Most of the times we want to pass all the list elements to a function one-by-one and then collect the output. For instance:

```
>>> def square(x):
>>> 	return x * x

>>> items = [1, 2, 3, 4, 5]
>>> squared = []
>>> for e in items:
>>>     squared.append(square(e))
>>> print(squared)
[1, 4, 9, 16, 25]
```

`Map` allows us to implement this in a much simpler and nicer way. Here you go:

```
>>> items = [1, 2, 3, 4, 5]
>>> squared = list(map(square, items))
>>> print(squared)
[1, 4, 9, 16, 25]
```

### 2.2 Filter

As the name suggests, `filter` creates a list of elements for which a function returns true. Here is a short and concise example:

```
>>> def negative(x):
>>> 	return x < 0
>>>     
>>> number_list = [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
>>> less_than_zero = list(filter(negative, number_list))
>>> print(less_than_zero)
[-5, -4, -3, -2, -1]
```

The filter resembles a for loop but it is a builtin function and faster.

### 2.3 Reduce

`Reduce` is a really useful function for performing some computation on a list and returning the result. It applies a rolling computation to sequential pairs of values in a list. For example, if you wanted to compute the product of a list of integers.

So the normal way you might go about doing this task in python is using a basic for loop:

```
>>> def mul(x, y):
>>>		return x * y
>>>     
>>> product = 1
>>> list = [1, 2, 3, 4]
>>> for num in list:
>>>     product = product * num
>>> print(product)
24
```

Now let’s try it with reduce:

```
>>> from functools import reduce
>>> product = reduce(mul, [1, 2, 3, 4])
>>> print(product)
24
```

(adapted from pythontips.org)

## 2.4 Lambda expressions

When using map, filter and reduce you often need to provide a very simple function like `squared`in the example below:

```
def square(x):
	return x * x
```

For creating very simple functions you can us the lambda lambda notation like below:

```
>>> squared = lambda x : x * x
>>> print(squared(5))
25
```

One of the advantages of  having lambda's is that they don't need to be explicitly named first. They can be created on the spot. Which makes it particularly useful to use in combination with map:

```
>>> items = [1, 2, 3, 4, 5]
>>> squared = list(map(lambda x : x * x, items))
>>> print(squared)
[1, 4, 9, 16, 25]
```

Lambda functions can take any number of arguments. Lambda's that take two arguments are useful to use with reduce.

```
>>> from functools import reduce
>>> product = reduce(lambda x, y : x * y, [1, 2, 3, 4])
>>> print(product)
24
```

## Summary

All in all we introduced many ways we could implement the function `only_upper`.

Method 1, classic:

```
def only_upper(t):
  res = []
  for s in t:
    if s.isupper():
    	res.append(s)
  return res
```

Method 2, list comprehensions:

```
def only_upper(t):
	return [s for s in t if s.isupper()]
```

Method 3, map:

```
def is_upper(s):
	return s.isupper()

def only_upper(t):
	return map(is_upper, t)
```

Method 4, map and lambda:

```
def only_upper(t):
	return map(lambda s: s.isupper(), t)
```

So, which is better? That depends on the goal, personal taste, and context. I tend to prefer functional solutions because the resulting code looks cleaner. But I avoid lambda functions because they don't help the readability of the code. So in this case I would probably opt for method 3. But there are many good arguments to make for the other methods. The most important is to be consistent. Try to choose one style of programming and stick to it throughout the project.
