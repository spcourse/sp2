# Text classification

For the this exercise we're going to use the package `functional` you created in the previous two exercises for analyzing texts.

## Part 1: unigrams

The goal is to write a program called `classify_unigram.py` that can classify newspaper articles. For instance we have an article from HuffPost on the question if it is better to cook vegetables or eat them raw. The tool you're going to write should be able to determine the topics of this article.

### Example usage:

When you run `python classify_unigram.py "articles\\cooking veggies.txt"`, you should see:

```
FOOD & DRINK             2323
TASTE                    2157
WELLNESS                 1449
HEALTHY LIVING           1172
SCIENCE                  1041
```

Note that the location of the text file is provided by the first command line argument.

### Downloads

First, download the model files:

[data](news/downloads/news-topic-data.zip)

## TODO

### data/unigrams

The directory data contains both a folder `unigrams` and `bigrams`. For now we'll focus on only the `unigrams` . This directory contains 41 files ( `ARTS.csv`, `BUSINESS.csv`, `TASTE.csv`, etc.), all these files contains lists of words and scores pertaining to the category. For example the file `TRAVEL.csv` contains the lines:

```
overtourism,17
airfares,17
lagoons,17
lençóis,17
...
saltwater,10
floridian,10
croatian,10
...
```

It contains many, many more lines, these are just a couple of examples. Every line contains a keyword, related to the topic and a score reflecting how strongly the keyword is related (separated by a comma). So, the word 'overtourism' (with a score of 17) is more strongly related to 'TRAVEL' than 'croatian' (with a score of 10).

> Note: This list is compiled by analyzing many tens of thousands of articles from HuffPost ([News Category Dataset | Kaggle](https://www.kaggle.com/rmisra/news-category-dataset)).

## articles

The directory `articles` contains a selection of text files containing articles from different news sources.

## Goal

1. Create a program called `classify_unigram.py` that can read a text file provided as command line argument.
2. Tokenize the text (create a list containing every word--also duplicates--of the text).
3. For each category compute the total score:
   1. Read the csv file for the category.
   2. Look up the score for every word of the tokenized text. (If the word is not in the category list, you may assume the score is 0.)
   3. Add all the scores together. This is the category score
4. Print a sorted list with the 5 highest scoring categories for the text. (The formatting should be the same as shown above.)
5. Do all of the above using the functions `my_map`, `my_filter`, and `my_reduce`. Don't use loops for step 3.2 and 3.3. In fact, try not to use loops at all. It is possible to avoid them entirely.

### Tips

- If you cannot figure out how to avoid using a loop, write the program with loops first. Try to replace them with  `my_map`, `my_filter`, and `my_reduce` later.
- For some string s, `s.strip()` will remove any newlines and space behind and in front of the string.
- The method `s.split(',')` will split s on every ','.
- Don't forget about string slicing and lambda's.
- The following code prints all the lines of `TRAVEL.csv`:
```
 with open('data/unigram/TRAVEL.csv') as f:
 	for line in f:
    	print(line)
```
- If you use `my_map`, `my_filter`, and `my_reduce `correctly you shouldn't need to write a lot of code.
- The variable `sys.argv` is a list containing the command line arguments. Lets, for example, say that the file `test.py` contains the following code:
```
import sys
print(sys.argv[1])
```
Then running `python test.py "Hello, world!"` should produce the output `Hello, world!`.

## Part 2: bigrams

The problem with using keywords can sometimes be the lack of context. When we encounter the word `Will` in a text, it is not very clearly related to a topic, the same for the word `Smith`. But if we know they occur one after the other, we might suspect that the text has something to do with the topic _entertainment_. So it can be very useful to look at pairs of words, called bigrams.

For example, the phrase "Will Smith levitates in first-ever fashion campaign" contains the following bigrams: "Will Smith", "Smith levitates", "levitates in", "in first-ever", "first-ever fashion", "fashion campaign".

Not all of those bigrams provide useful information (e.g., "in first-ever"), but some of them might contain much more information than the single words would have (e.g., "Will Smith" and "fashion campaign").

> Side note: of course you could even go further by creating trigrams, four-grams or even-more-grams. In general we just refer to ngrams for any-length-grams. In fact, Google has a very cool analytical tool based on ngrams. You can check it out [here](https://books.google.com/ngrams/graph?content=natural+language+processing%2Cfunctional+programming&year_start=1960&year_end=2008&corpus=15&smoothing=3&share=&direct_url=t1%3B%2Cnatural%20language%20processing%3B%2Cc0%3B.t1%3B%2Cfunctional%20programming%3B%2Cc0) (don't forget to come back at some point).

### data/bigrams

The folder `data/bigrams`, contains list of scored bigrams for every category. For example `TRAVEL.csv` contains the following lines:

```
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
```

### Goal

The goal is very similar to the previous part, but instead of using unigrams, you are to use bigrams. (In fact it is so similar that it shouldn't require a whole lot of new code to do this).

1. Create a program called **`classify_bigram.py`** that can read a text file provided as command line argument.
2. **Generate all the bigrams** of the provided text.
3. For each category compute the total score:
   1. Read the **bigram** csv file for the category.
   2. Look up the score for every **bigram** of the text. (If the word is not in the category list, you may assume the score is 0).
   3. Add all the scores together. This is the category score
4. Print a sorted list with the 5 highest scoring categories for the text. (The formatting should be the same as shown above.
5. Do all of the above using the functions `my_map`, `my_filter`, and `my_reduce`. Don't use loops for step 3.2 and 3.3. In fact, try not to use loops at all. It is possible to avoid them entirely.

### Tips

- The function `zip()` in python (together with some clever list-slicing) can be useful for creating bigrams. The function zip can combine two lists:
```
>>> zipped_list = list(zip(['a', 'b', 'c'], ['X', 'Y', 'Z'])
>>> print(zipped_list)
[('a', 'X'), ('b', 'Y'), ('c', 'Z')]
```

## Part 3: Finishing touches

Let's treat this assignment as if you are going to make it a public project, that you would like to share. Try to make the design and style of the code as good as you can.

One question deserves special attention: Is there a lot of duplication of code? It is likely that the files `classify_unigram.py` and `classify_bigram.py `contain a lot of duplicate code. Is there a way to move parts of the code to an external module to avoid this?

Provide a README.md, containing a description for the project. This doesn't have to be in Markdown format but can be plain text.

Provide a LICENSE file with the project. [Here](https://choosealicense.com/) you can find a tool for selecting the right license for your project. Choose an *open source* licence that you deem appropriate and copy the text into the LICENSE file.
