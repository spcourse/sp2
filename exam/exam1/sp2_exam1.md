# Exam Scientific Programming 2

Date: March 30 2022

This is a digital exam. The exam consists of 3 assignment in which you have to write a short python program.

You're only evaluated based on the _correctness_ of your solutions, code design is not important. So, you don't have to worry about comments or the style guide.

You can test your code using checkpy. First download the tests for the exam:

    checkpy -d /spcourse/exam-tests

Run checkpy:

    checkpy sp2_exam2

# Rules

- Create one file for all your solutions called `sp2_exam2.py`. This is the file you'll hand in at the end of your exam.
- You're only allowed to use `pandas` package. You're not allowed any other external Python package.
- You're only allowed to use the websites sp1.mprog.nl/sp2.mprog.nl and the Pandas documentation from https://pandas.pydata.org/. You're not allowed to use any other website. (So also no Google!)
- You are allowed to look at your own code that you wrote during the course.
- You cannot get any help with programming during the exam.
- Submit your solutions when you're done. **Check with the teacher present if you handed in your assignment correctly before leaving the exam venue.**


### 1. Library

We have loaded information about book genres into a dictionary called `library`. The dictionary has the titles of the books as keys and the genres as values (see usage example below). We would like to group the titles by genre. Write a function called `group_titles_by_genre(library)`, that takes the dictionary and outputs a new dictionary where each key is a genre and each value is a list of all titles that belong to the given genre.

Example usage:

    library = {"Life of Pi": "Adventure",
               "One World The Water Dancer": "Fantasy",
               "The Three Musketeers": "Adventure",
               "To Kill a Mockingbird": "Classics",
               "Circe": "Fantasy",
               "The Call of the Wild": "Adventure",
               "Little Women": "Classics"}

    grouped = group_titles_by_genre(library)
    print(grouped)

Expected output:

    {'Adventure': ['Life of Pi', 'The Three Musketeers', 'The Call of the Wild'], 'Fantasy': ['One World The Water Dancer', 'Circe'], 'Classics': ['To Kill a Mockingbird', 'Little Women']}

### 2. Vowels

**Without using any loop construction** (other than the one already defined in `my_filter`), write a function `no_vowel(text)` that has as an input a `text` and returns a list with all words that do not end in a vowel ('a', 'e', 'i', 'o', or 'u'). You may assume that the input text does not contain any punctuation or special characters.

Example usage:

    text = "I do not like words that end in vowels"
    l = no_vowel(text)
    print(l)

Expected output:

    ['not', 'words', 'that', 'end', 'in', 'vowels']

You're allowed to use this `my_map` function below:

    def my_filter(pred, my_list):
        return [e for e in my_list if pred(e)]

Tip: You can split a text into a list of words using the `text.split()` method.

### 3. Sepal

Download the [`iris.csv`](iris.csv) for this exam. Read the file using Pandas and store it as a DataFrame called `iris`. Print the first 5 rows of the DataFrame holding all data.

The output of this part of your program should be:

       sepal_length  sepal_width  petal_length  petal_width species
    0           5.1          3.5           1.4          0.2  setosa
    1           4.9          3.0           1.4          0.2  setosa
    2           4.7          3.2           1.3          0.2  setosa
    3           4.6          3.1           1.5          0.2  setosa
    4           5.0          3.6           1.4          0.2  setosa

We're going to try to combine the width and length features of petals or sepals together into a new feature. This feature will be area of the petal or sepal, which we'll approximate using an ellipse.

Create a function `compute_area(iris_dataframe)`, that creates a copy of the input DataFrame (`iris_dataframe`) and adds two new collumns: `sepal_area` and `petal_area`. Since we assume the sepal and petal to be an ellipse, you can compute the area's with the formula $$0.5 * L * 0.5 * W * \pi$$ where $$L$$ and $$W$$ are the length and with of the sepal or petal. The function returns this new DataFrame. You may assume $$\pi$$ to be $$3.14$$

The output of the function should be a floating point number, which has been rounded to two decimals. Test the function with:

    iris_area = compute_area(iris)
    print(iris_area.head())

Which should print:

       sepal_length  sepal_width  petal_length  petal_width species  sepal_area  petal_area
    0           5.1          3.5           1.4          0.2  setosa    14.01225      0.2198
    1           4.9          3.0           1.4          0.2  setosa    11.53950      0.2198
    2           4.7          3.2           1.3          0.2  setosa    11.80640      0.2041
    3           4.6          3.1           1.5          0.2  setosa    11.19410      0.2355
    4           5.0          3.6           1.4          0.2  setosa    14.13000      0.2198
