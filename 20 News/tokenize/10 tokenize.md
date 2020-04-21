# Tokenize

## Goal

Write a program that reads a text file and transforms it into a list of words . You're going to use the package `functional` you created in the previous two exercises for analyzing texts.

## Downloads

* First download the data that you need for this exercise: [news topic data](../downloads/news-topic-data.zip)
* Save the file in your project directory for this module (e.g., `module 6`).
* Unzip the file.

Your `module-6` directory now contains two new sub-directories:

* `data`: We will ignore this directory for now. It contains files for the next exercise.
* `articles`: This directory contains a  number of text files containing articles from different news sources.

Before you start programming have a look at the articles to get a feel for the data.

## Specification

Implement a program called `list_words.py` that generates a list of all the words in a given text file and prints that list. Each word in the output should written in lowercase, and stripped from punctuation marks and white spaces. For example:

    # python list_words.py "articles\short.txt"
    [for, sale, baby, shoes, never, worn]

## Tips

* For some string s, `s.strip()` will remove any newlines and space behind and in front of the string.
* The method `s.split(',')` will split s on every ','.
* The variable `sys.argv` is a list containing the command line arguments. Lets, for example, say that the file `test.py` contains the following code:

    ```python
    import sys
    print(sys.argv[1])
    ```


  Then running `python test.py "Hello, world!"` should produce the output `Hello, world!`.
