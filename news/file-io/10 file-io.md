# Reading, writing, and finding files; file I/O

The following code will open a file and print every line:

with open('some_file.txt', 'r') as f:
    for line in f:
        print(line, end='')

This will `open` `'some_file.txt'` in read mode (`'r'`), and assign it to the variable named `f`. Then, a for loop loops over every `line` in the file by finding the line endings indicated by `'\n'`. This `'\n'` is included in the variable `line`. The function print always adds a newline (another `\n`) when printing, unless we pass it `end=''`, which will make it add an empty string at the end. Let's say our file is set up as follows:

    'This is the first line of the file.\n Second line of the file.\n'

Then our program would output:

    This is the first line of the file.
    Second line of the file.

Throughout coming exercises and in future projects you will come across many situations where you need to read data from a file. In this writeup we will introduce you to some of the basics of reading, writing, and finding files using Python.

> All information that is in a box like the one this text is in, is advanced information which you can read if you want to know more about the methods.

## Opening a file

Let's start with the basics:

    f = open('some_file.txt', 'r')

`open()` returns a file object, and is most commonly used with two arguments: `open(filename, mode)`. The first argument is a string containing the path to the file (including the filename). The second argument, `mode`, is another string containing a few characters describing what you will do with the file. `mode` can be `'r'` when the file will only be read, `'w'` for only writing (an existing file with the same name will be overwritten). It is also possible to open a file for both reading and writing with `'rw'`.

> Normally, files are opened in text mode, that means, you read and write strings from and to the file. Adding `'b'` to the `mode` opens the file in binary mode: now the data is read and written in the form of bytes objects. This mode should be used for all files that don’t contain text. It is also possible to open the file for appending (writing) at the end of the file: `'a'`.

_The rest of the examples assume that there is some variable `f` that holds an opened file object._

## File encodings

When using `open()`, it is possible to pass an optional parameter named `encoding`. This parameter can be set to one of the various text-encoding codecs that is available in Python. These codes define how the bits and bytes in the file should be interpreted as strings.

    f = open('some_file.txt', 'r', encoding='utf-8', errors='replace')

> Most data files use `utf-8`, and if the codec is not defined for your dataset, it is probably `utf-8`. More supported codecs are listed [here](https://docs.python.org/3/library/codecs.html#standard-encodings), but an easier way to deal with codec errors is to set the optional parameter `errors='replace'`. This replaces any unknown characters with the character of a question mark.

## Reading from a file

There is multiple ways to read a file's contents. None of the methods that are described here are wrong, but they all have their own advantages and disadvantages. It is up to you to select the appropriate method.

### Reading the whole file

To read an entire file's contents at once, call `f.read()`.

>>> f.read()
'This is the first line of the file.\n Second line of the file.\n'
>>> f.read()
''

> `f.read()` has an optional argument named `size` that can be used to read specific quantity of data from the file. When it is omitted, or negative, the entire contents of the file will be returned. This is not advisable for large files, as it will try to allocate memory for the entire file at once, which may not be available. The method is however, very useful when you want to read a specific amount of data from a file. If the end of the file is reached, `f.read()` returns an empty string: `''`.

### Reading line by line

There are two methods of reading a file line by line. The first is `f.readline()`, which reads a single line from a file:

    >>> f.readline()
    'This is the first line of the file.\n'
    >>> f.readline()
    'Second line of the file.\n'
    >>> f.readline()
    ''

`f.readline()` stops when it finds a newline character `'\n'`, which is included at the end of the string it returns. An empty string is returned when the end of the file has been reached, while blank lines are represented by a string containing a newline: `'\n'`.

The second method of reading a file line by line is looping over the file object:

    >>> for line in f:
    ...     print(line)
    ...
    This is the first line of the file.

    Second line of the file

Functionally, this is the same as calling `f.readline()` until an empty string is returned, but it results in slightly cleaner code.

> If you want to read all the lines of a file into a list of strings, you can also use `list(f)` or `f.readlines()`. Keep in mind that for large files this would require a lot of memory.

## Writing to files

Writing to files is fairly simple:

    >>> some_string = 'something!'
    >>> len(some_string)
    10
    >>> f.write(some_string)
    10

 Use `f.write(some_string)` to wite the content of `some_string` to the file. The method returns the number of characters that was written to a file. Keep in mind that `f.write()` only accepts strings, so you might need to convert your variables to strings before writing them:

    >>> some_number = 42
    >>> f.write(str(some_number))
    2

## The `with` keyword

It is good practice to use the `with` keyword when dealing with file objects:

    with open('some_file.txt', 'r') as f:
        data = f.read()

The advantage of using `with` is that the file is automatically properly closed, even if an exception is raised or an error occurs at some point. If you're not using the `with` keyword, then you should call `f.close()` to close the file. After a file object is closed, either by `with` or by `f.close()`, attempts to use the file object will automatically fail.

## CSV files

The Comma Separated Values (CSV) format and variations of it is one of the most common formats for scientific data. There is no standard method of generating files in these format, and as such it can be quite annoying to process CSV files. Python's `csv`-module implements functions that are able to read and write most variations of data that is in CSV format. CSV files can be opened as any normal file, and then processed through `csv.reader()` as follows:

    >>> import csv
    >>> with open('example.csv', 'r') as csvfile:
    ...     rdr = csv.reader(csvfile)
    ...     for row in rdr:
    ...         # Create one string from the entire row and print it
    ...         print(', '.join(row))
    This, is, an, example!
    It, really, is.

Where `row` is a list that contains every element that was originally seperated by commas, essentially functioning the same as `string.split()`.

The `csv`-module has more functionalities than just this simple reader, but for now it is everything you will need.
