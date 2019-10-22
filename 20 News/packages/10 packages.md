# Packages

A big part of the challenge of becoming a good programmer is create code that not only works that one time all the stars were aligned just right, but that works reliably, that is easy to read, to extend and to improve. Especially with bigger projects it can be vital to organize your code into separate modules/packages and to document them correctly. Here you will learn how to do this in a couple of steps:

1. Create a new package
2. Adding documentation to the package
3. Add readme and license to the project

## Create a new package

Managing big projects can quickly become quite a challenge. A good way to keep bigger projects manageable is by making it more modular: split your program up in distinct modules that can be tested individually. Lets have a look at how we can do this.

We start with a folder called `my_project` containing one python file called `my_program.py`. So we have the following project structure:

    my_project
    |_> my_program.py

The file `my_program.py` contains the following code:

    def reverse_string(s):
        return s[::-1]

    def double_string(s):
        return s*2

    def convert_to_ints(s):
        return [int(e) for e in s.split()]

    my_string1 = '1 2 3 4 5 '

    my_string2 = double_string(my_string1)
    print(my_string2)

    my_string3 = reverse_string(my_string2)
    print(my_string3)

    my_number_list = convert_to_ints(my_string3)
    print(my_number_list)

When we run `python my_program.py` we get the following output:

    1 2 3 4 5 1 2 3 4 5
     5 4 3 2 1 5 4 3 2 1
    [5, 4, 3, 2, 1, 5, 4, 3, 2, 1]

The code works, but let's try to organize it a bit better.

### Move functions to module

When you look at the code you can see that there are three functions concerning strings. They seem to conceptually belong together. A first step is to move those into a separate file called `my_string_module.py`.

So we get the following project structure:

    my_project
    |_> my_program.py
    |_> my_string_module.py

Where `my_string_module.py` contains:

    def reverse_string(s):
        return s[::-1]

    def double_string(s):
        return s*2

    def convert_to_ints(s):
        return [int(e) for e in s.split()]

We can now remove those functions from `my_program.py`, but we have to tell the program where those functions can be found. We do that with the command `from <module> import <functions>` like this:

    from my_string_module import reverse_string, double_string, convert_to_ints

    my_string1 = '1 2 3 4 5 '

    my_string2 = double_string(my_string1)
    print(my_string2)

    my_string3 = reverse_string(my_string2)
    print(my_string3)

    my_number_list = convert_to_ints(my_string3)
    print(my_number_list)

### Bundle modules into package

When modules contain a lot of functions it might want to go one step further in our organizational efforts: we could create a package folder.

Let's split `my_string_module.py` into two parts: `conversions.py` (containing `convert_to_ints()`) and `manipulations.py` (containing the other two functions). We put those file in a new directory called `my_string_package`.

Project structure:

    my_project
    |_> my_program.py
    |_> my_string_package
        |_> conversions.py
        |_> manipulations.py

Code `conversions.py`:

    def convert_to_ints(s):
        return [int(e) for e in s.split()]

Code `manipulations.py`:

    def reverse_string(s):
        return s[::-1]

    def double_string(s):
        return s*2

We need to change the import statement in `my_program.py` such that it knows to look in the right folder and file like so:

    from my_string_package.manipulations import reverse_string, double_string
    from my_string_package.conversions import convert_to_ints

    my_string1 = '1 2 3 4 5 '

    my_string2 = double_string(my_string1)
    print(my_string2)

    my_string3 = reverse_string(my_string2)
    print(my_string3)

    my_number_list = convert_to_ints(my_string3)
    print(my_number_list)

The label `my_string_package.manipulations` in the import statement tells python to look in the folder `my_string_package` at the file `manipulations.py`.

### Add init

Even though it can be nice to have functions in separate files in a package, it can be annoying to have to specify this in your program with the lines:

    from my_string_package.manipulations import reverse_string, double_string
    from my_string_package.conversions import convert_to_ints

We can avoid this by adding an `__init__.py` file in the package directory:

    my_project
    |_> my_program.py
    |_> my_string_package
        |_> __init__.py
        |_> conversions.py
        |_> manipulations.py

In the  `__init__.py` we import the functions from the separate files:

    from .manipulations import reverse_string, double_string
    from .conversions import convert_to_ints

Now we can simplify the import statement in `my_program.py`:

    from my_string_package import reverse_string, double_string, convert_to_ints

    my_string1 = '1 2 3 4 5 '

    my_string2 = double_string(my_string1)
    print(my_string2)

    my_string3 = reverse_string(my_string2)
    print(my_string3)

    my_number_list = convert_to_ints(my_string3)
    print(my_number_list)

When python comes across the statement `from my_string_package import ...` it knows to look for a file `__init__.py` in the `my_string_package` folder. The other files can remain unchanged.

Code `conversions.py`:

    def convert_to_ints(s):
        return [int(e) for e in s.split()]

Code `manipulations.py`:

    def reverse_string(s):
        return s[::-1]

    def double_string(s):
        return s*2

## Add documentation

Once created a package you need to document it. So that the next person using the package (most likely your future self), can find out how to use it without having to read all the code. The tool `pydoc` can automatically extract information from python packages.

Run `$ pydoc my_string_package` (from the `my project` directory):

    Help on package my_string_package:

    NAME
        my_string_package

    PACKAGE CONTENTS
        conversions
        manipulations

    FILE
        [some path]\my_string_package\__init__.py

As you can see it `pydoc` automatically generated some information about our package. We get the name of the package, the sub-modules ( `conversions` and `manipulations`), and the location of the package. Type `q` to exit `pydoc`. 

We can even inspect the sub-modules themselves.

Run `$ pydoc my_string_package.manipulations`:

    Help on module my_string_package.manipulations in my_string_package:

    NAME
        my_string_package.manipulations

    FUNCTIONS
        double_string(s)

        reverse_string(s)

    FILE
        [some path]\my_string_package\manipulations.py

This also shows the names of the functions contained in the `manipulations` package.

### Add docstrings

We can use *docstrings* to provide `pydoc` with more information about the package. Docstrings are simply strings using triple quotes ("""") that, when placed correctly, will be automatically extracted for documentation.

Start by adding a docstring to top of `__init__.py`:

    """ (short description) Do stuff with strings!

    (long description) We got it all: reverse, double, and convert. You need it, we got it!
    """
    from .manipulations import reverse_string, double_string
    from .conversions import convert_to_ints

The first line will be interpreted as a short description of the package, and the rest as a more elaborate description. When we run `$ pydoc my_string_package` again we can see the effect:

    NAME
        my_string_package - (short description) Do stuff with strings!

    DESCRIPTION
        (long description) We got it all: reverse, double, and convert. You need it, we got it!

    PACKAGE CONTENTS
        conversions
        manipulations

You see `pydoc` added the short description to the name and added the rest to the new field `DESCRIPTION`.

### Add more docstrings

Similarly we can add docstrings to the top of the sub-packages.

Code `manipulations.py`:

    """Manipulate strings!

    All the functions in this module manipulate strings.
    """

    def reverse_string(s):
        return s[::-1]

    def double_string(s):
        return s*2

Run `$ pydoc my_string_package.manipulations`:

    NAME
        my_string_package.manipulations - Manipulate strings

    DESCRIPTION
        All the functions in this module manipulate strings.

    FUNCTIONS
        double_string(s)

        reverse_string(s)

### Yet more docstrings

To let `pydoc` generate a description of each function within the module, we can simply add a docstring to the beginning of each function.

Code `manipulations.py`:

    """Manipulate strings!

    All the functions in this module manipulate strings.
    """

    def reverse_string(s):
        """Reverse the order of characters in a strings
        """
        return s[::-1]

    def double_string(s):
        """Doubles (repeats) the string
        """
        return s*2

Run `$ pydoc my_string_package.manipulations`:

    NAME
        my_string_package.manipulations - Manipulate strings!

    DESCRIPTION
        All the functions in this module manipulate strings.

    FUNCTIONS
        double_string(s)
            Doubles (repeats) the string

        reverse_string(s)
            Reverse the order of characters in a string.

We should still add documentation to `conversions.py` and, of course, normally you would try to make the documentation a bit more helpful than in this example, but I suppose you get the point by now.

## Readme and license

We only documented the `my_string_package` package above. It is good practice to always document every function you write and every python file you create, even if it is not part of a package.

When you publish your project you also typically add at least a license and a readme file to the root of your project. The license file is a text file called LICENSE. It is best to stick to existing license texts (you can find an overview [here](https://choosealicense.com/)). The readme file is typically a markdown file called README.md. Markdown is a simple markup language that is made popular by the code-sharing platform [GitHub](https://github.com). If you're interested in learning Markdown you can find more information [here](https://www.markdownguide.org/).  

Once you added all these documents you should wind up with a minimal project structure that looks something like this:

    my_project
    |_> my_program.py
    |_> LICENSE
    |_> README.md
    |_> my_string_package
        |_> __init__.py
        |_> conversions.py
        |_> manipulations.py
