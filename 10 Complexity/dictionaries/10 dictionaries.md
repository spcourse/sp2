# Dictionaries

Dictionaries are one of the fundamental data structures of Python, and
just like lists, they can be used to store several elements together in
one variable. Unlike lists, dictionaries store *mappings* from a key to a
value.

The difference between dictionaries and lists is that instead of using an index
to access elements, we use a key. Searching for things by their keys is the
main reason dictionaries are used so often and why they are such an efficient
data structure. In a list, if we don't know at what index something is stored
exactly, we'd have to loop over the list until we found the matching element.
Whereas in a dictionary, we can just search by key. More on why this is
efficient later, for now lets just see a simple example.

One way we could use a dictionary, is to store the mappings in an actual
English-Spanish translation dictionary. We might have the string "Yes" and we
want to store its Spanish translation:

	KEYS            VALUES
	------------------------
	Yes         :   Si
	No          :   No
	Please      :   Por favor
	Thank you   :   Gracias 

Here the English words are the keys and we can easily look up their Spanish
translation in the dictionary.

	Dictionary[Please]
	-> Por favor

The mapping here is from one element to another associated element (its
translation), which we might want to look up. This is generally how
dictionaries are used in Python. Lets take a closer look at at the syntax in
Python and some more cases where we might want to use dictionaries.

So, dictionaries are an efficient way to store pairs of variables together. As
another example, we could make a fruit basket and store the quantity we have of the different types of fruit. In our previous example we stored Spanish
translations for English words in our dictionary, and here we are going to
store counts for each type of fruit. Using dictionaries in this way, as a
mapping from elements to some count (or a score) is another very common way to use dictionaries

    >>> basket = {'apple': 4, 'banana': 7, 'orange': 2}
    >>> basket
    {'apple': 4, 'orange': 2, 'banana': 7}

Note that the order of these elements has changed! Dictionaries are unordered collections of pairs, which means we can easily find back each pair, but cannot make any assumptions about the order in which they are stored. If we want to know how many apples there are in the fruit basket, we can write

    >>> basket['apple']
    4

The left half of each pair is called the **key** and the right half is called
the **value**. So, here we used the key `'apple'` to find the value `4`. This
syntax is very similar to using square brackets to get elements from a *list*,
but instead of using the **index** to retrieve the element stored at that
place in the list, we use the **key** to retrieve the corresponding **value**
from the dictionary.

Using this same syntax, we can add a new *key-value pair*

    >>> basket['strawberry'] = 10
    >>> basket
    {'apple': 4, 'orange': 2, 'strawberry': 10, 'banana': 7}

Or we could use this syntax to modify an existing pair. Lets say we ate one of
the bananas, then we could update the dictionary by writing

    >>> basket['banana'] -= 1
    >>> basket
    {'apple': 4, 'orange': 2, 'strawberry': 10, 'banana': 6}

Each *key* in a dictionary **must** be unique, so if we try to adding a *key*
that already exists, we'll end up overwriting the corresponding *value*. So,
if we try to add another key for apples, will just end up replacing the old
pair

    >>> basket['apple'] = 6
    >>> basket
    {'apple': 6, 'orange': 2, 'strawberry': 10, 'banana': 6}

Note that values **do not** have to be unique, as dictionaries are only a
one-way mapping, so you can only use the *keys* to retrieve the corresponding
*values*, not the other way around. Searching for a pair using the value will
produce a *KeyError*

    >>> basket[2]
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    KeyError: 2

because the key `2` does not exist in our basket. The value `2`, does of
course occur in our basket, stored under the key `'orange'`

    >>> basket['orange']
    2

If we try to retrieve the number of *mango*, which aren't in the basket at all,
we also get a *KeyError*

    >>> basket['mango']
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    KeyError: 'mango'

We can also use the `get()` function instead of the square brackets, and as the
second argument tell the dictionary what value we want if the key is not
present in the dictionary

    >>> basket.get('mango', 0)
    0

So now we know that our fruit basket unfortunately contains zero mangoes, but in
many situations this result is much more useful then producing an error.

We can also explicitly ask if a key is present in the dictionary using `in`

    >>> if 'banana' in basket:
    ...   print("We've got bananas!")
    ... 
    We've got bananas!

This works exactly the same way as it does for lists, *with 1 important
difference.* Using `in` on a list will search through the entire list, and so
this will actually take longer to complete as more elements are added to the
list, because it is actually an $$O(N)$$ operation. As stated in the
introduction, dictionaries are not just convenient to use, but also very
efficient. In fact, they are so efficient that searching in a dictionary is an
$$O(1)$$ operation. This means the search will take approximately the
same time if the dictionary contains 1 or **1 million** elements!

This is a *strange and counter-intuitive* fact, and why this is true is well
beyond the scope of this text, but it should give you an idea of the power of
dictionaries and why they are used so often: Checking if a key is present in a
dictionary or retrieving the value stored with that key are both **constant
time** $$O(1)$$ operations, irrespective of the number of elements
stored in that dictionary.

As a result, dictionaries are mostly used for these look-up operations, but
sometime you'll also want to loop over the elements in your dictionary.
Dictionaries support many of the same operations that lists do. For instance,
you can use `len` to ask how many pairs there are in the dictionary

    >>> len(basket)
    4

We can also use `for` loops with dictionaries, like so

    >>> for fruit in basket:
    ...   print(fruit)
    ...
    apple
    orange
    strawberry
    banana

This will only loop over the keys of the dictionary, but we could just use the
square brackets to retrieve the values as well

    >>> for fruit in basket:
    ...   print(fruit, basket[fruit])
    ...
    apple 6
    orange 2
    strawberry 10
    banana 6

We can even use the `items` function to easily loop over both

    >>> for fruit, amount in basket.items():
    ...   print(fruit, amount)
    ... 
    apple 6
    orange 2
    strawberry 10
    banana 6

This concludes this introduction to dictionaries.

Next up, we'll cover another data structure called *tuples*.
