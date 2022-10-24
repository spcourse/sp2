# Exam Scientific Programming 2

Date: June 23 2022

This is a digital exam. The exam consists of 3 assignment in which you have to write a short python program.

You're only evaluated based on the _correctness_ of your solutions, code design is not important. So, you don't have to worry about comments or the style guide.

You can test your code using checkpy. First download the tests for the exam:

    checkpy -d /spcourse/exam-tests

Run checkpy:

    checkpy sp2_exam4

# Rules

- Create one file for all your solutions called `sp2_exam4.py`. This is the file you'll hand in at the end of your exam.
- You're only allowed to use `pandas` package. You're not allowed any other external Python package.
- You're only allowed to use the websites sp1.mprog.nl/sp2.mprog.nl and the Pandas documentation from https://pandas.pydata.org/. You're not allowed to use any other website. (So also no Google!)
- You are allowed to look at your own code that you wrote during the course.
- You cannot get any help with programming during the exam.
- Submit your solutions when you're done. **Check with the teacher present if you handed in your assignment correctly before leaving the exam venue.**

### 1. Calorie intake

You're writing a program for a dietician. It tracks calories for a specific diet in which someone is allowed to eat 70% of your normal calorie intake. You're writing a program that based on your regular calorie intake and the food someone already ate, and it tells you how many calories that person can still eat.

For this, you have a dictionary that contains different types of food as key and the number of calories as value.

Write a function `allowed_calories(food, eaten, normal)` that accepts a dictionary containing food with it's corresponding calories, a list of foods already consumed, and an integer representing your normal calorie intake. The output is an integer representing how many calories are still allowed according to the diet.

Have a look a this example:

    food = {"banana": 88, "apple": 52, "nuts": 606, "chocolate": 545, "salmon": 208, "smoothie": 36, "fries": 322, "sandwich": 265}
    eaten = ["banana", "salmon", "fries"]
    allowed = allowed_calories(food, eaten, 2000)
    print(allowed)

This should produce the output:

    782

Tip: round the number of calories to the nearest integer, using the function `round()`.
Tip: the output may also be negative.


### 2. Oddity

**Without using any loop construction** (other than the one already defined in `my_filter`), write a function `starts_and_ends(text)` that filters a text such that only the words that both start and end with a vowel ("a", "e", "i", "o", "u") are added to a list.
You may assume that the input text does not contain any punctuation or special characters.

Example usage:

    text = "I really enjoy eating an apple more than a banana"
    words = starts_and_ends(text)
    print(words)

Expected output:

    ["I", "apple", "a"]

You're allowed to use this `my_filter` function below.

    def my_filter(pred, my_list):
        return [e for e in my_list if pred(e)]

Tip: You can split a text into a list of words using the `text.split()` method.


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

This data contains all the election results of the 2022 municipal elections of Amsterdam. It contains the name, position in the party and number of votes for each candidate. It contains also the party affiliation for each candidate, but that's encoded in an inconvenient way: The party is only mentioned for the first candidate of each party. The other ones contain a `NaN` value. You can assume that when the party is `NaN`, the party is the same as the one of the candidate above it. For example, the party of _Nadif_ is _Groenlinks_ and so is the party of _van der Veen_. And, for example, the party of _Moeskops_ is _D66_.

Every party makes their own ranking of party members. This ranking, however, could be different than the ranking made by the voting public.
Create a function `different_ranking(election_results, party)` that returns whether the highest voted candidate was also ranked highest by the party themselves.

Test the function with:

    different_rank = different_ranking(election_results, "GROENLINKS")
    print(different_rank)

    different_rank = different_ranking(election_results, "D66")
    print(different_rank)

Which should print:

    TRUE
    FALSE

The problem involves a number of steps:
1. First you will need to deal with the `NaN`. You can use the Pandas `fillna` method for this.
2. Second, you need to find the highest ranked member of a party (the first occurring row of that party) and the highest voted member of a party (the row with the most votes).
3. Final, you should check whether these two members are the same.
