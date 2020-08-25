# Tokenize

## Goal

Write a program that reads a text file and transforms it into a list of words. You're going to use the package `functional` you created in the previous two exercises for analyzing texts.

## Downloads

* First, download the data that you need for this exercise: [news topic data](../downloads/news-topic-data.zip)
* Save the file in your project directory for this module (e.g., `module_6`).
* Unzip the file.

Your `module_6` directory now contains two new sub-directories:

* `data`: We will ignore this directory for now. It contains files for the next exercise.
* `articles`: This directory contains a number of text files containing articles from different news sources.

Before you start programming have a look at the articles to get a feel for the data.

## Specification

Implement a program called `list_words.py` that generates a list of all the words in a given text file and prints that list. Each word in the output should written in lowercase, and stripped from punctuation marks and white spaces. For example:

    # python list_words.py "articles\short.txt"
    [for, sale, baby, shoes, never, worn]

## Tips

* For some string `s`, `s.strip()` will remove any newlines and space behind and in front of the string.
* The method `s.split(',')` will split s on every ','.
* After importing the module `string`, it is possible to get a list of every common type of punctuation in the variable `string.punctuation`. This variable contains: ``'!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'``. The same can be done for whitespace with `string.whitespace`, and digits with `string.digits`.
* The variable `sys.argv` is a list containing the command line arguments. Lets, for example, say that the file `test.py` contains the following code:


    import sys
    print(f'Number of arguments: {sys.argc}')
    print(f'Arguments: {sys.argv}')
    print(sys.argv[1])


  Then running `python test.py "Hello, world!"` should produce the output:

    Number of arguments: 2
    Arguments: ['test.py', 'Hello, World!']
    Hello, World!

Ultimately, you should check whether results are reasonable yourself. There might be some characters that you have to add to your "stripping" methods manually. Data cleaning code is always a bit messy and most of the time has a lot of problem-specific additions, but try to keep it nice and organized. Comment your code whereever it has these problem-specific additions and create functions where necessary.

Note that the way you tokenize affects the outcome of your unigram and bigram implementations such that it might not give the exact same results as the given examples. *This is not an issue.*
