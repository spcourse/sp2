# Exam Scientific Programming 2

Date: June 2 2022

This is a digital exam. The exam consists of 3 assignment in which you have to write a short python program.

You're only evaluated based on the _correctness_ of your solutions, code design is not important. So, you don't have to worry about comments or the style guide.

You can test your code using checkpy. First download the tests for the exam:

    checkpy -d /spcourse/exam-tests

Run checkpy:

    checkpy sp2_exam3

# Rules

- Create one file for all your solutions called `sp2_exam3.py`. This is the file you'll hand in at the end of your exam.
- You're only allowed to use `pandas` package. You're not allowed any other external Python package.
- You're only allowed to use the websites sp1.mprog.nl/sp2.mprog.nl and the Pandas documentation from https://pandas.pydata.org/. You're not allowed to use any other website. (So also no Google!)
- You are allowed to look at your own code that you wrote during the course.
- You cannot get any help with programming during the exam.
- Submit your solutions when you're done. **Check with the teacher present if you handed in your assignment correctly before leaving the exam venue.**


# 1. Booklist

For school, you are required to read books from a prescribed booklist. Instead of asking you to read at least 5 books from that list, the teacher asks you to read at least 1000 pages. Of course, even though you are an eager student, you don't want to read way too much. Write a function `count_pages(books_page_count, read_books)` that, given a dictionary of books (with the title of the book as a key, and the number of pages in that book as value) and a list of titles you have read, can calculate the total number of pages in the books that you have read. The function doesn't need to take into account invalid book titles.

    books_page_count = {'Nineteen Eighty-Four': 328, 'The Very Hungry Catterpillar': 22, 'Gulliver\'s Travels': 352, 'Frankenstein': 280, 'David Copperfield': 624, 'Moby-Dick': 736, 'Ulysses': 730, 'Lord of the Flies': 224, 'To Kill a Mockingbird': 281, 'The Picture of Dorian Gray': 272,'The Hobbit': 310}

    read_books = ['The Very Hungry Catterpillar', 'The Hobbit', 'Frankenstein', 'Lord of the Flies']

    page_total = count_pages(books_page_count, read_books)
    print(f'The books {read_books} have {page_total} pages in total.')


Should print:

    The books ['The Very Hungry Catterpillar', 'The Hobbit', 'Frankenstein', 'Lord of the Flies'] have 836 pages in total.


### 2. Hidden message

**Without using any loop construction** (other than the ones already defined in `my_filter` and `my_map`), write a function `decrypt(text)` that has as an input a `text` and returns the first character from every word in the text that is directly followed by punctuation.

Example usage:

    text = "So, that door is the nearest Exit? Correct. Used Rarely? Exactly. Terrific!"
    s = decrypt(text)

    print(s)

Expected output:

    ['S', 'E', 'C', 'R', 'E', 'T']

You're allowed to use these `my_filter` and `my_map` functions below:

    def my_filter(pred, my_list):
        return [e for e in my_list if pred(e)]

    def my_map(fun, my_list):
        return [fun(e) for e in my_list]

Hint: You can separate the text on the spaces using `.split()`.

### 3. Species

Download the [`iris.csv`](iris.csv) for this exam. Read the file using Pandas and store it as a DataFrame called `iris`. Print the first 5 rows of the DataFrame holding all data.

The output of this part of your program should be:

       sepal_length  sepal_width  petal_length  petal_width species
    0           5.1          3.5           1.4          0.2  setosa
    1           4.9          3.0           1.4          0.2  setosa
    2           4.7          3.2           1.3          0.2  setosa
    3           4.6          3.1           1.5          0.2  setosa
    4           5.0          3.6           1.4          0.2  setosa

Write a function `compute_average_per_species(iris_dataframe, column)` that returns for a `column` what the average value is per species. There are three species in this dataset.

Your result should be a dataframe or series. Test the function with:

    sepal_length_per_species = compute_average_per_species(iris, 'petal_width')
    print(sepal_length_per_species)

Which should print:

    species
    setosa        0.246
    versicolor    1.326
    virginica     2.026
    Name: petal_width, dtype: float64
