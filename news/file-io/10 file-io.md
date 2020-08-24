# Reading, writing, and finding files; file I/O

Throughout coming exercises and in future projects you will come across many situations where you need to read data from a file. In this writeup we will introduce you to some of the basics of reading, writing, and finding files using Python.

## Opening a file

Let's start with the basics. `open()` returns a file object, and is most commonly used with two arguments: `open(filename, mode)`.

    f = open('some_file.txt', 'r')

The first argument is a string containing the path to the file (including the filename). The second argument, `mode`, is another string containing a few characters describing what you will do with the file. `mode` can be `'r'` when the file will only be read, `'w'` for only writing (an existing file with the same name will be overwritten), and `'a'` opens the file for appending; any data written to the file is automatically added to the end. It is also possible to open a file for both reading and writing with `'rw'`.

Normally, files are opened in text mode, that means, you read and write strings from and to the file. Adding `'b'` to the `mode` opens the file in binary mode: now the data is read and written in the form of bytes objects. This mode should be used for all files that don’t contain text.

> The rest of the examples assume that there is some variable `f` that holds an opened file object.

## File encodings

When using `open()`, it is possible to pass an optional parameter named `encoding`. This parameter can be set to one of the various text-encoding codecs that is available in Python. These codes define how the bits and bytes in the file should be enterpreted as strings. Most data files use `utf-8`, and if the codec is not defined for your dataset it is probably `utf-8`. More supported codecs are listed [here](https://docs.python.org/3/library/codecs.html#standard-encodings), but an easier way to deal with codec errors is to set the optional parameter `errors='replace'`. This replaces any unknown characters with the character of a question mark.

    f = open('some_file.txt', 'r', encoding='utf-8', errors='replace')

## Reading from a file

There is multiple ways to read a file's contents. None of the methods that are described here are wrong, but they all have their own advantages and disadvantages. It is up to you to select the appropriate method.

To read an entire file's contents, call `f.read()`. This function has an optional argument named `size` that can be used to read specific quantity of data from the file. When it is omitted, or negative, the entire contents of the file will be returned. This is not advisable for large files, as it will try to allocate memory for the entire file at once, which may not be available. The method is however, very useful when you want to read a specific amount of data from a file. If the end of the file is reached, `f.read()` returns an empty string: `''`.

    >>> f.read()
    'This is the first line of the file.\n Second line of the file.\n'
    >>> f.read()
    ''

There are two methods of reading a file line by line. The first is `f.readline()`, which reads a single line from the file. It stops when it finds a newline character `\n`, which included in end of the string it returns. An empty string is returned when the end of the file has been reached, while blank lines are represented by a string containing a newline: `'\n'`.

    >>> f.readline()
    'This is the first line of the file.\n'
    >>> f.readline()
    'Second line of the file\n'
    >>> f.readline()
    ''

The second method of reading a file line by line is looping over the file object. Functionally, this is the same as calling `f.readline()` until an empty string is returned, but it results in slightly cleaner code:

    >>> for line in f:
    ...     print(line)
    ...
    This is the first line of the file.

    Second line of the file

If you want to read all the lines of a file into a list of strings, you can also use `list(f)` or `f.readlines()`. Keep in mind that for large files this would require a lot of memory.

## Writing to files

Writing to files is fairly simple. Use `f.write(some_string)` to wite the content of `some_string` to the file. The method returns the number of characters that was written to a file. Keep in mind that `f.write()` only accepts strings, so you might need to convert your variables to strings before writing them.


## The `with` keyword

It is good practice to use the `with` keyword when dealing with file objects. The advantage is that the file is automatically properly closed, even if an exception is raised or an error occurs at some point.

    with open('some_file.txt', 'r') as f:
        data = f.read()

If you're not using the with keyword, then you should call `f.close()` to close the file. After a file object is closed, either by `with` or by `f.close()`, attempts to use the file object will automatically fail.

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

# OS - operating system interfaces

One Python library often used in combination with file reading and writing is `os`. Different Operating Systems have different methods of describing filepaths; ie Linux uses a forward slash `/`, while Windows uses a backward slash `\`. The `os`-module provides methods that can be used to create and explore filepaths that work across multiple Operating Systems. In other words: the functions that the `os`-module provides allow you to interface with the underlying operating system that Python is running on – be it Windows, Mac or Linux. While the `os`-module has many functionalities, we will only discuss a couple of functionalities that are interesting in the context of file I/O.

The first thing you might need in a situation where you are required to build a filepath, is `os.path.join()`. This function can take two strings and concatenate them using the correct OS directory separators. Let's say that we know that we have a directory `'data'`, and in `'data'` there is some file named `'example.csv'`. Using `filepath = os.path.join('data', 'example.csv')` we would get `'data/example.csv'` when running the code on Linux, and `'data\example.csv'` on Windows. Giving no second argument, or an empty string, creates a string with one separator at the end. This is useful for creating the relative path to a folder.

A very useful method that can be used to get a list containing every file and folder in a given directory is `os.listdir(path)`. When no `path` is given to this function, the current working directory (CWD; the directory from which the program was run) is used. Essentially, this is the Python equivalent to your command line's `ls`.

A more complex method that gives a more detailed view of the local filestructure is `os.walk()`. This method generates a whole directory-tree by "walking" through every possible folder and subfolder, meanwhile keeping track of every file it finds. The command returns a tuple with three values for every directory that it finds: `(root, dirs, files)`. `root` is a string containing the relative path to the directory `os.walk()` is currently exploring. `dirs` is a list of every directory that is found in that directory. `files` is a list of every file that is found in that directory. Let's say we are currently in the following working directory:

    my_project
    |_> my_program.py
    |_> LICENSE
    |_> README.md
    |_> my_string_package
        |_> __init__.py
        |_> conversions.py
        |_> manipulations.py

And that we run the following code from our main folder `my_project`:

    for (root, dirs, files) in os.walk('.'):
        print(f'Currently working from: {root}')
        print(f'Found directories: {dirs}')
        print(f'Found files: {files}')

This would result in the following output:

    Currently working from: .
    Found directories: ['my_string_package']
    Found files: ['LICENSE', 'my_program.py', 'README.md']
    Currently working from: ./my_string_package
    Found directories: []
    Found files: ['conversions.py', 'manipulations.py', '__init__.py']

Indicating that, in our main folder (indicated by `'.'`), there is one folder named `'my_string_package'`, and three files named `['LICENSE', 'my_program.py', 'README.md']`. In the folder `'my_string_package'`, found by traversing from our root `.` to `'my_string_package'`, there are no folders, and three files named `['conversions.py', 'manipulations.py', '__init__.py']`. Let's say that we would want to do something with every file that is found, we could program something like this:

    for (root, dirs, files) in os.walk('.'):
        for file in files:
            do_something(os.path.join(root, file)

Which will apply `do_something()` to each of the files in our main folder, before applying the function to all files in the first subfolder, then that subfolder's subfolders, etc. `os.walk()` is a very powerful tool that can make short work of otherwise very complicated file-managing tasks!
