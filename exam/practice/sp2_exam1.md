# Practice exam Scientific Programming 2

This is a digital exam. The exam consists of 3 assignment in which you have to write a short python program.

You're only evaluated based on the _correctness_ of your solutions. Code design is not important. So, you don't have to worry about comments or the style guide.

You can test your code using checkpy. First download the tests for the exam:

    checkpy -d /spcourse/exam-tests

Run checkpy:

    checkpy sp2_exam1

# Rules

- Create one file for all your solutions called `sp2_exam1.py`. This is the file you'll hand in at the end of your exam.
- You're only allowed to use `pandas` package. You're not allowed any other external Python package.
- You're only allowed to use the websites sp1.mprog.nl/sp2.mprog.nl and the Pandas documentation from https://pandas.pydata.org/. You're not allowed to use any other website. (So also no Google!)
- You are allowed to look at your own code that you wrote during the course.
- You cannot get any help with programming during the exam.
- Submit your solutions when you're done. **Check with the teacher present if you handed in your assignment correctly before leaving the exam venue.**

### 1. Expense

You're writing a program that keeps track of your expenses. You're using a dictionary that keeps track of the monthly expenses in euros per category (_food_, _rent_, _internet_, _utilities_, _social activities_, etc.). Now you would like to know what percentages of you monthly expenses these categories represent.

Write a function  `euros_to_percentage(expenses)` that accepts a dictionary containing the expenses in euros. It should create a new dictionary containing the expenses in percentages.

Have a look a this example:

    expenses_january_in_euros = {'rent': 735, 'utlities': 221,
                                 'food': 167, 'social activities': 185,
                                 'internet + netflix + spotify': 58, 'phone': 25}
    expenses_january_in_percentages = euros_to_percentage(expenses_january_in_euros)
    print(expenses_january_in_percentages)

This should produce the output:


    {'rent': 52.83968368080517, 'utlities': 15.88785046728972, 'food': 12.005751258087706, 'social activities': 13.299784327821712, 'internet + netflix + spotify': 4.169662113587347, 'phone': 1.7972681524083394}


**Note:** the order in which this result is printed does not need to be the same as the example above. Check whether each category has the right value. If this is the case, your code probably works!


### 2. Oddity

**Without using any loop construction** (other than the one already defined in `my_map`), write a function `half_double(my_list)` that maps a lists of numbers (`my_list`): if a number is odd, double it, if the number is even, half it.

Example usage:

    l = [1, 2, 3, 4, 5]
    l2 = half_double(l)
    print(l2)

Expected output:

    [2, 1, 6, 2, 10]

You're allowed to use this `my_map` function below:

    def my_map(fun, my_list):
        return [fun(e) for e in my_list]


### 3.

In the old practice exam there is a `pandas` question here. You should expect a question on Object Oriented Programming instead.

For now you can ignore the `checkpy` tests that correspond to this question.
