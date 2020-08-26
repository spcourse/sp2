# Bigrams

## Goal

Write a program called `classify_bigram.py` that, similar to the previous assignment, can classify newspaper articles. This time use pairs of words (bigrams) instead of (single) words.

The problem with using single keywords can sometimes be the lack of context. When we encounter the word `Will` in a text, it is not very clearly related to a topic. The same for the word `Smith`. But if we know they occur one after the other, we might suspect that the text has something to do with the category entertainment. So it can be useful to look at pairs of words (called bigrams).

For example, the phrase "Will Smith levitates in first-ever fashion campaign" contains the following bigrams: "Will Smith", "Smith levitates", "levitates in", "in first-ever", "first-ever fashion", "fashion campaign".

Not all of those bigrams provide useful information (e.g., "in first-ever"), but some of them might contain much more information than the single words would have (e.g., "Will Smith" and "fashion campaign").

> Side note: of course you could even go further by creating trigrams or even four-grams. In general we just refer to ngrams for any-length-grams. In fact, Google has a very cool analytical tool based on ngrams. You can check it out [here](https://books.google.com/ngrams/graph?content=natural+language+processing%2Cfunctional+programming&year_start=1960&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2Cnatural%20language%20processing%3B%2Cc0%3B.t1%3B%2Cfunctional%20programming%3B%2Cc0) (don't forget to come back).

## Bigrams

The directory `bigrams` in `data` contains list of scored bigrams for every category. For example `TRAVEL.csv`contains the following lines:

    lonely,planet,17
    most,tourists,17
    tourists,do,17
    its,pet,17
    to,tripadvisor,17
    ...
    flying,in,12
    go,somewhere,12
    world,famous,12
    airline,industry,12
    ireland,is,12
    ...

In this example the bigram `lonely planet` has a score of 17 for the category `travel`, and the bigram `airline industry` has a score of 10.

Running the bigram program should result in something like this:

    $ python classify_bigram.py "articles/cooking veggies.txt"
    FOOD & DRINK        1935
    WELLNESS            1572
    TASTE               1378
    HEALTHY LIVING      1177
    SCIENCE             811

Note that the scores you get might not align with the example given above, as your tokenize might result in a slightly different wordlist. *This is okay.* In stead of comparing your scores to the scores listed above, it might be better to create your own short article (a couple of words) such that you can check your results manually.

## Specification

* Create a program called `classify_bigram.py` that can read a text file provided as command line argument.
* Read and tokenize the text file.
* Read and the bigram files and store the data in dictionaries.
* Use the bigram dictionaries and the tokenized text to compute the total category score for every category. Don't use any `for`-loops for *this* step, instead use the functions `my_map`, `my_filter`, and `my_reduce`.
* Print a sorted list with the 5 highest scoring categories for the text. (The formatting should be the same as shown above.)
* Cleanup and add a `README.md` and `LICENSE` file to the project (see below).

## Tips

* You will need to start with creating a bigram list for every article. You are allowed to use a for loop for this. But, if (in the spirit of this assignment) you would like to avoid using a loop, you can use the function `zip()` in python (together with some very clever list-slicing) to achieve the same. It combines two lists into one:

    >>> zipped_list = list(zip(['a', 'b', 'c'], ['X', 'Y', 'Z'])
    >>> print(zipped_list)
    [('a', 'X'), ('b', 'Y'), ('c', 'Z')]

## Cleanup

* Let's treat this assignment as if you were going to make it into a public project. Adorn your code with comments and docstrings where appropriate.
* Provide a README.md, containing a description for the project. This doesn't have to be in Markdown format but can be plain text.
* Provide a LICENSE file with the project. [Here](https://choosealicense.com/) you can find a tool for selecting the right license for your project. Choose an *open source* licence that you deem appropriate and copy the text into the LICENSE file.
* BONUS: One question merits special attention: Is there a lot of duplication of code?
    * It is likely that the files `classify_unigram.py` and `classify_bigram.py` have a lot of of code in common. Can you find a way to move parts of the code to an external module to avoid this? *Take care to backup your code before you start to restructure it*.
