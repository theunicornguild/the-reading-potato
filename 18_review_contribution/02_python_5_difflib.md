This is the page where the author will be able to review the contribution and make their decision on whether they want these changes to be applied to their article or not.

Before we jump into the code, Let's take a step back and think about this for a minute.

The author wants to make a decision in this page about whether they want the new modified content or to keep the old content.

That means the author will be seeing both the new content and the current content.

If the article is a 100 lines long, and the contribution is only one small change in line 43. We need a way to let the author know where changes are made without him having to read through the new and current content seperately and trying to find the difference.

Thankfully python provides this library [`difflib`](https://docs.python.org/3/library/difflib.html) which helps in comparing two sequences or in our case two strings. 

If you take a look at the documentation, you'll find a class `Differ` that specifically conpares lines of text and returns the differences. Take a look at [this table](https://docs.python.org/3/library/difflib.html#difflib.Differ). This table helps differentiate between each line returned after comparing the two contents and what their relationship is with these contents.

Let's take a look at how we can use this library
```python
import difflib

string1 = """Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
"""

string2 = """Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
Unos aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
"""

d = difflib.Differ()
comparison = d.compare(string1.splitlines(), string2.splitlines())
print(list(comparison))
```

We first created an instance of the class `Differ`
```python
d = difflib.Differ()
```

Next we used the above instance to compare between the two strings. However we need to keep in mind that the `compare` method will compare the strings letter by letter because the string is a sequence of characters. So, instead we'll split the string into a sequence of individual lines so that the `compare` method will compare the strings line by line by using the string method `splitlines()`.
```python
comparison = d.compare(string1.splitlines(), string2.splitlines())
```

Finally, to get the comparison in a format that easy to handle by the `template`, we'll turn it into a list of lines and print it for the sake of the example.
```python
print(list(comparison))
```

Take the above code and run it, change the two strings as you want just so you can see how the library is working.

![still here](https://media.giphy.com/media/Wwfto5K9ixU9xzf5lK/giphy.gif)

Go try the code and then come back
