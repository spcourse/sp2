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


### 3. Elections

[Download the `election_results_amsterdam_2022.csv` for this exam here](election_results_amsterdam_2022.csv) and read it using Pandas. Store it as a DataFrame called `election_results`. Print the first 5 rows  and after that also row 39 to 44 of the DataFrame.

The output of this part of your program should be:

              party  candidate_number        candidate_name  votes
    0  1 GROENLINKS                 1   Groot Wassink, B.R.  12162
    1           NaN                 2             Nadif, I.  12435
    2           NaN                 3        Ernsting, Z.D.    694
    3           NaN                 4       Bentoumya, Y.E.   4313
    4           NaN                 5  van der Veen, K.S.N.    560
        party  candidate_number     candidate_name  votes
    39    NaN                40         Corton, E.    288
    40  2 D66                 1  van Dantzig, R.H.  15537
    41    NaN                 2   de Jager, D.O.C.  12294
    42    NaN                 3     Rooderkerk, I.   1857
    43    NaN                 4   Moeskops, E.D.M.   1545

This data contains all the election results of the 2022 municipal elections of Amsterdam. It contains the name, position in the party and number of votes for each candidate. It contains also the party affiliation for each candidate, but that's encoded in an inconvenient way: The party is only mentioned for the first candidate of each party. The other ones contain a `NaN` value. You can assume that when the party is `NaN`, the party is the same as the one of the candidate above it. For example, the party _Nadif_ is _Groenlinks_ and so is the party of _van der Veen_. And, for example, the party of _Moeskops_ is _D66_.

We know that the PvdA party won the most votes in the election, but now we're not interested in the total votes of the party. Instead we want to know the top candidates across all parties. Create a function `top_candidates(results)` that computes a DataFrame containing **all candidates that had more than 2%** of the total number of votes, including the party affiliation of each candidate.

**Don't use a loop for this assignment.**

Test the function with:

    top = top_candidates(election_results)
    print(top)

Which should print:

                                     party  candidate_number          candidate_name  votes  percentage_votes
    0                         1 GROENLINKS                 1     Groot Wassink, B.R.  12162          3.743663
    1                         1 GROENLINKS                 2               Nadif, I.  12435          3.827697
    40                               2 D66                 1       van Dantzig, R.H.  15537          4.782543
    41                               2 D66                 2        de Jager, D.O.C.  12294          3.784295
    90                               3 VVD                 1             Martens, C.  25012          7.699103
    140  4 Partij van de Arbeid (P.v.d.A.)                 1             Moorman, M.  42778         13.167769
    170       5 SP (Socialistische Partij)                 1  Alberts-Oosterbaan, R.   9465          2.913482
    195            6 Partij voor de Dieren                 1    van Lammeren, J.F.W.   9351          2.878391
    380                            13 JA21                 1            Nanninga, A.  11821          3.638697
    512                            25 Volt                 1            Broersen, J.   9018          2.775888


The problem involves a number of steps:
1. First you will need to deal with the `NaN`. You can use the Pandas `fillna` method for this.
2. Second, you need to compute the percentage of votes of each candidate and create a column `percentage_votes` which contains the number of votes as a percentage of the total votes cast.
3. Finally you should select only the rows where this percentage is higher then 2%.
