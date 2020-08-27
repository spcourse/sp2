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
