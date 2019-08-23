# Defining efficiency

For this assignment we are going to start with some short examples and\
questions about **efficient** code. You probably have noticed by now that there\
can be quite a few different ways to solve some problems in *Python*. Swapping\
a `for` loop with a `while` loop might not change a lot, but in most cases the\
choice for one approach will have some effect. Which approach you end up\
choosing, can depend on a few different factors:

1. Some approaches might be shorter to write than others (not always the best\
   reason).
2. Some approaches might be more readable, requiring less documentation to be\
   understandable.
3. Some approaches might take less time to compute a solution to the same\
   problem, making them more efficient.

Note that all 3 of these are distinctly different criteria, and shorter code\
definitely does not imply faster to compute. If it isn't code length, then what\
*does* determine a program's speed?

## Big O notation

A general rule for efficiency is that it becomes more important as the data you\
are working with gets larger. If you have to process millions of data points,\
then inefficient code might have you waiting for the results for a long time,\
or worse, make your solution infeasible altogether. Because in science we often\
work with large data sets, studying the fundamentals of efficient code for any\
size of input will prove to be a useful tool.

In computer science, the primary measure for efficiency is called the *big\
$\\mathcal{O}$ notation*. It is used to relate how the computation time for\
piece of code grows as the size of its input grows. Let's take the simple\
function below as an example

```python
def sum_list(inputs):
    total = 0
    for elem in inputs:
        total += elem
    return total
```

As the number of elements in this list grows, so does the number of steps in\
this for loop. So, we would expect longer lists to take longer to compute.\
Let's test that hypothesis, by seeing how long different calls of this function\
end up taking. We'll use the `numpy` library to quickly to generate a list of\
$N$ numbers between $0$ and $100$ and use the `time` library to measure the\
time the computation takes in seconds.

```python
    import time
    import numpy

    def random_list(N, max_int=100):
        # Generate N random numbers between 0 and max_int
        return list(numpy.random.randint(0, max_int, N))

    def timed_function_list(function, *args):
        # Measure start time
        start = time.time()
        # Call the function with the provided arguments
        result = function(*args)
        # Measure end time
        end = time.time()

        print("The %s of %s elements took %6f seconds to compute." % \
            (function.__name__, str(len(args[0])).rjust(10), end-start))

        return result

    for i in range(5, 9):
        inputs = random_list(10**i)
        total = timed_function_list(sum_list, inputs)
        print("The sum total was", total)
```

```
The sum_list of     100000 elements took 0.008087 seconds to compute.
The sum total was 4951878
The sum_list of    1000000 elements took 0.080046 seconds to compute.
The sum total was 49488344
The sum_list of   10000000 elements took 0.743973 seconds to compute.
The sum total was 494901280
The sum_list of  100000000 elements took 7.268038 seconds to compute.
The sum total was 4949616780
```

Although not exactly, we can see that for each factor of 10 more numbers,\
approximately requires a factor of 10 longer to compute. Intuitively, this\
might make sense, as the number of steps in the for loop grows scales linearly\
with the number of elements in the list. This means our function has a linear\
complexity, denoted as big $\\mathcal{O}(N)$.

The big $\\mathcal{O}$ notation is quite a coarse measure, which only concerns\
what the dominating factor will for the computation time as the input grows. In\
contrast, these timing tests are accurate to the microsecond ($10^{-6}$\
seconds), so there will always be some differences between the theoretical\
factor and the measured scale factor. In addition, your computer will also be\
performing other tasking in the background, so there will even be differences\
in the times if you repeat the measurements, eventhough the computation steps\
are identical every time.

Both these effects will be more pronounced for smaller input sizes, and should\
smooth out as the input becomes larger, but computing for larger inputs\
requires waiting for the results longer. For each of the experiments in this\
assignment we've tried to strike a balance between the two, so the scale is\
large enough to see *the general trend for different input sizes*, but does\
not take too long to compute. Note that some of these experiments are therefore\
done at different input scales, based on the complexity of the problems, so\
keep this in mind when comparing the results between experiments.

## Quadratic Complexity

So, the `sum_list` function had complexity of $\\mathcal{O}(N)$, but\
unfortunately, not all problems can be solved with a linear complexity. Lets\
take a look at another example, where we are trying to count how often each\
number occurs in our list. We will take a somewhat naive approach and generate\
a new list indicating how often each number occurs:

```python
def count_occurrence(inputs):
    counts = []
    for elem_1 in inputs:
        # Counts for each element start at 0
        c = 0
        for elem_2 in inputs:
            # If the elements match, increase the count by 1
            if elem_1 == elem_2:
                c += 1

        # After comparing to all the elements in the list, add the count
        counts.append(c)

    # Return the list of counts for each element
    return counts

for i in range(2, 5):
    inputs = random_list(10**i)
    counts = timed_function_list(count_occurrence, inputs)

    # Show the counts for the first 5 numbers
    for j in range(5):
        print("The number", inputs[j], "occurs", counts[j], "times")
```

```
The count_occurrence of        100 elements took 0.000695 seconds to compute.
The number 1 occurs 2 times
The number 39 occurs 2 times
The number 87 occurs 4 times
The number 23 occurs 1 times
The number 66 occurs 3 times
The count_occurrence of       1000 elements took 0.042067 seconds to compute.
The number 2 occurs 8 times
The number 40 occurs 10 times
The number 34 occurs 15 times
The number 59 occurs 13 times
The number 86 occurs 8 times
The count_occurrence of      10000 elements took 4.298409 seconds to compute.
The number 10 occurs 113 times
The number 54 occurs 109 times
The number 54 occurs 109 times
The number 9 occurs 84 times
The number 22 occurs 112 times
```

Some important things to note here: Firstly, the number of elements we are\
using to make this comparison is **much** smaller, in order to keep the\
computation times manageable. Secondly, for this function, with every factor 10\
more elements, the computation time scales up by about a factor 100!

This is because our function `count_occurrence` has a quadratic complexity,\
denoted as $\\mathcal{O}(N^2)$. This means that as the size of the input for\
this function grows by some factor $N$, we expect the computation time to grow\
approximately by $N^2$.

Recall that computing the sum of the elements with our linear $\\mathcal{O}(N)$\
function for $10^9$ elements took about 7 seconds. For the quadratic\
`count_occurrence` function, the last measurement we have was for $10^5$\
elements, taking approximately 4 seconds (on this machine). We can use the\
$\\mathcal{O}(N^2)$ complexity of the function to try and estimate how long this\
might take for $10^9$ elements.

An input size of $10^9$ elements would be an increase of a factor $10^4$ in\
input size compared to $10^5$. Given the quadratic complexity, we would expect\
a $(10^4)^2$ increase in computation time, meaning about $4$ seconds $\\times\
10^8$ or **13 years!**

Here we can really see a practical difference between a $\\mathcal{O}(N)$ or a\
$\\mathcal{O}(N^2)$ function. For $10^3$ elements or less, you probably won't\
notice any difference at all, as all computations will be well under 1 second.\
For $10^6$ it already makes the difference between less than 1 second and\
several minutes of waiting for your results. And at $10^9$ it is the difference\
between a couple of seconds and a completely infeasible couple of years.

Nowadays having millions or more elements in your data set is really quite\
common, so knowing the difference between linear and quadratic solutions can\
really be critical.

## Constant time

There is one last complexity class we will introduce here, to round out your\
perspective on complexity; big $\\mathcal{O}(1)$. Big $\\mathcal{O}(1)$ is also\
called *constant time* and it means that the time to compute a function\
remains constant as the input grows in size. This is the best possible complexity\
any algorithm can have, as it means that the time for the function will remain\
roughly the same, even if you have billions of elements to process.

What kind of function could meet this ideal complexity might be hard to\
imagine for now, but we'll start with a trivial example. Later in this module we'll see\
much more interesting functions with $\\mathcal{O}(1)$ complexity, specifically\
when we cover dictionaries. Lets start by considering this simple function, which\
always returns the first element from a list:

```python
def get_first_element(inputs):
    return inputs[0]


for i in range(5, 9):
    inputs = random_list(10**i)

    elem = timed_function_list(get_first_element, inputs)
    print("The first element was", elem)
```

```
The get_first_element of     100000 elements took 0.000003 seconds to compute.
The first element was 79
The get_first_element of    1000000 elements took 0.000003 seconds to compute.
The first element was 5
The get_first_element of   10000000 elements took 0.000002 seconds to compute.
The first element was 58
The get_first_element of  100000000 elements took 0.000004 seconds to compute.
The first element was 46
```

As you a can see, getting the first element takes about the same time for each\
of these input sizes, even though the inputs get bigger with a factor 10 each\
time. This means the function `get_first_element` has a complexity of\
$\\mathcal{O}(1)$. So in theory, we could get the first element from a list with\
*any* number of elements and it would still only take 0.000004 seconds (although at some point we might have some trouble fitting that list in our computers memory).

Next, take a look at the videos on data structures. These videos will not just\
the operations the data structures support, but also the complexity is of these\
operations. Many data structures are used *specifically* because they are more\
efficient in certain situations.
