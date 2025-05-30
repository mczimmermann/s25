---
layout: lab
num: lab05
ready: true
desc: "Ordered Linked Lists"
assigned: 2025-05-07 10:59:59.59-7
due: 2025-05-13 23:59:59.59-7
---

In this lab, you'll have the opportunity to practice:

* Defining classes in Python
* Overloading an operator in a Python class
* Implementing an Ordered Linked List
* Testing your functionality with pytest

**Note: It is important that you start this lab early so you can utilize our office hours to seek assistance / ask clarifying questions during the week before the deadline if needed!**

You will write a program that will organize Book objects into a Book Collection. The Book Collection will be implemented as an Ordered Linked List with a `head` reference. The implementation in this lab will be different than an Unordered Linked List since you will need to **organize the nodes by the Book's author (in lexicographical / alphabetical order)**. In the event of a tie (several books are written by the same author), the published **year** will be used to determine the Book object's place in the Ordered Linked List. If the author and year published are the same, then the Book's **title (lexicographical / alphabetical order)** will be used to determine the Book object's place in the Ordered Linked List.

This lab will require you to define classes for a `Book`, `BookCollection`, and a `BookCollectionNode`, as well as writing your own unit tests to verify the correctness of your implementation.

## Instructions

You will need to create four files:
* `Book.py` - file containing a class definition for a Book object
* `BookCollection.py` - file containing a class definition for a collection of Books that will be implemented as an Ordered Linked List
* `BookCollectionNode.py` - file containing a class definition for a Node in the BookCollection
* `testFile.py` - file containing pytest functions testing the overall correctness of your class definitions

There will be no starter code for this assignment, but rather the class descriptions and required methods are defined in the specification below.

You should organize your lab work in its own directory. This way all files for a lab are located in a single folder. Also, this will be easy to import various files into your code using the `import / from` technique shown in lecture.

## Cybersecurity Application
While this lab focuses on organizing books in a collection, the skills you're developing have direct applications in cybersecurity, particularly in incident response and digital forensics.
Consider the following real-world application of the **Security Incident Timeline Construction**.

When investigating a security breach, analysts need to collect and organize logs from various sources (network devices, servers, applications) into a cohesive incident timeline. This process is remarkably similar to what you're doing with the BookCollection:

- **Ordered Data Structure**: Just as you're creating an ordered linked list of books, security professionals build ordered timelines of security events. The proper chronological ordering is critical for understanding attack progression.
- **Multi-level Sorting**: Your books are sorted by author, then year, then title. Similarly, security incidents might be sorted by timestamp, then severity, then source device.
- **Filtering Capabilities**: Your `get_books_by_author()` method parallels how an analyst might filter security events by specific IP addresses or user accounts.
- **Recursive Searching**: The recursive search technique you're implementing could be used to efficiently locate specific types of security events within a large dataset.
- **Data Removal**: The `remove_author()` method is comparable to filtering out false positives or irrelevant events from an investigation.

By mastering these programming techniques, you're building transferable skills for creating, managing, and analyzing ordered datasets -- a fundamental capability in cybersecurity incident response, threat hunting, and digital forensics.

## Book.py class

The `Book.py` file will contain the definition of a Book. We will define the Book attributes as follows:

* `title` - str that represents the title of the Book
* `author` - str that represents the author of the Book. This will be in a LastName, FirstName format. You may assume this will always be the case
* `year` - int that represents the year the Book was published

You should write a constructor that allows the user to construct a book object by passing in values for all of the fields. Your constructor should set the `title` and `author` attribues to empty strings (`""`), and the `year` attribute to `None` by default.

* `__init__(self, title, author, year)`

In addition to your constructor, your class definition should also support "getter" methods that can receive the state of the Book object:

* `get_title(self)`
* `get_author(self)`
* `get_year(self)`

You will implement the method

* `get_book_details(self)`

that returns a `str` with all of the Book attributes. The string should contain all attributes in the following EXACT format (**Note: There is no `\n` character at the end of this string**):

```python
b = Book("Ready Player One", "Cline, Ernest", 2011)
print(b.get_book_details())
```

<b>Output</b>

```
Title: Ready Player One, Author: Cline, Ernest, Year: 2011
```

* Lastly, your `Book` class will overload the `>` operator (`__gt__`). This will be used when finding the proper position of a Book in the Ordered Linked List using the specification above. We can compare books using the `>` operator while walking down the list and checking if the inserted book is `>` than a specific Book in the Ordered Linked List.
   * Double-check by writing several tests that the `__gt__` method in Book class works correctly for author, year, and title comparisons.

We reviewed operator overloading in class and the textbook does discuss overloading Python operators. You can also refer to this reference on overloading various operators as well:

[https://www.geeksforgeeks.org/operator-overloading-in-python/](https://www.geeksforgeeks.org/operator-overloading-in-python/)

## BookCollectionNode.py

The `BookCollectionNode.py` file will define the `BookCollectionNode` class. This will be similar to the Linked List Node implementation done in lecture. You will need to write the following methods:

* `__init__(self, data)` - constructor that will assign the parameter `data` (a Book object) as part of this node. Each node will also have a `next` reference associated with it. When constructing a `BookCollectionNode`, the `next` reference should be `None` by default.
* `get_data(self)` - getter method that returns the data (Book object)
* `get_next(self)` - getter method that returns the next `BookCollectionNode` in the Linked List structure
* `set_data(self, newData)` - updates the Node's data with the parameter `newData`
* `set_next(self, newNext)` - updates the Node's next reference with the `newNext` parameter (another `BookCollectionNode`)


## BookCollection.py

The `BookCollection.py` file will contain the definition of a collection of Book objects stored in an Ordered Linked List. The `BookCollection` will manage an Ordered Linked List containing `BookCollectionNode`s. The `BookCollection` class will be responsible for maintaining the overall structure of the Ordered Linked List. Your `BookCollection` class will need to support the following methods:

* `__init__(self)` - constructor that will have a `head` reference that references the first node in the Ordered Linked List. The `head` should be set to `None` by default (indicating that the list is empty).
.
* `is_empty(self)` - method that returns `True` (boolean) if the BookCollection is empty, and returns `False` otherwise.

* `get_number_of_books(self)` - method that returns the total number of Books (`int`) in the BookCollection. Returns a 0, if the collection is empty.

* `insert_book(self, book)` - method that inserts a Book in the appropriate place. This function is effectively a setter for the collection (sets the head to the new node). As mentioned before, all Books in the BookCollection are ordered based on **1)** the Book's author (alphabetical / lexicographical order), then **2)** the Book's year of publication, and then **3)** the Book's title (alphabetical / lexicographical order). Here is where we can utilize the Book's `>` operator. You'll need to use some logic to replace the references for the BookCollectionNodes when inserting the Book in the appropriate place. **Note that the comparison of the strings should be case insensitive (e.g., `'a' == 'A'`).**

When testing this function, make sure to write tests that test the insertion of items to the beginning, middle, as well as to the end of the collection to test both "edges" and the more regular scenario. Test case insensitivity as well.

* `get_books_by_author(self, author)` - method that returns a `str` containing all of the Book details by a specified author. **Note that each book will be in its own line (each line ending with a `\n` character)**. Also note that the input parameter (`author`) may be in a different case than the case of the author that the book was constructed with - in this situation, the comparison of the authors' names should be case insensitive (`'a' == 'A'`). An example (with the correct order) is shown below:

```python
b0 = Book("Cujo", "King, Stephen", 1981)
b1 = Book("The Shining", "King, Stephen", 1977)
b2 = Book("Ready Player One", "Cline, Ernest", 2011)
b3 = Book("Rage", "King, Stephen", 1977)

bc = BookCollection()
bc.insert_book(b0)
bc.insert_book(b1)
bc.insert_book(b2)
bc.insert_book(b3)
print(bc.get_books_by_author("KING, Stephen"))
```

<b> Output: </b>

```
Title: Rage, Author: King, Stephen, Year: 1977
Title: The Shining, Author: King, Stephen, Year: 1977
Title: Cujo, Author: King, Stephen, Year: 1981

```

* `get_all_books_in_collection(self)` - method that returns a `str` containing the details of all Books in the BookCollection. **Note that each book will be in its own line (each line, _including the last one_, ending with a `\n` character)**. An example (with correct order) is shown below:

```python
b0 = Book("Cujo", "King, Stephen", 1981)
b1 = Book("The Shining", "King, Stephen", 1977)
b2 = Book("Ready Player One", "Cline, Ernest", 2011)
b3 = Book("Rage", "King, Stephen", 1977)

bc = BookCollection()
bc.insert_book(b0)
bc.insert_book(b1)
bc.insert_book(b2)
bc.insert_book(b3)
print(bc.get_all_books_in_collection())
```

<b> Output: </b>

```
Title: Ready Player One, Author: Cline, Ernest, Year: 2011
Title: Rage, Author: King, Stephen, Year: 1977
Title: The Shining, Author: King, Stephen, Year: 1977
Title: Cujo, Author: King, Stephen, Year: 1981

```

When testing this function, make sure to write tests that test the retrieval of items from the beginning, middle, as well as from the end of the collection to test both "edges" and the more regular scenario.

* `remove_author(self, author)` - method that removes all Books written by a specified author. Since this is an Ordered Linked List, all Books written by a specific author should be located right next to each other in the Book Collection assuming your `insert_book` method has been implemented correctly. **Note:** the input parameter (`author`) may be in a different case than the case of the author that the book was constructed with - your solution must account for these situations.
        * When testing this function, make sure to write tests that delete items from the beginning as well as from the end of the collection to test both "edges".
        * Ensure case-insensitive comparisons for author names; test removals thoroughly to confirm all books by a specific author are removed, including consecutive ones.

* `recursive_search_title(self, title, bookNode)` - method that searches the `BookCollection` for a specific Book title passed in the method. **Note: this method must be done recursively.** This method will return a **Boolean value**: `True` if a Book in the BookCollection has the same title as the parameter `title` (str), and return `False` otherwise.
	* Since this solution is recursive, this method will take in a reference to a `BookCollectionNode` object (`bookNode`) in the `BookCollection` that needs to be searched.
	* The initial call to `recursive_search_title` would pass in the head of the `BookCollection` since that's the starting point to search through the entire `BookCollection`. For example:

	```python
	b0 = Book("Cujo", "King, Stephen", 1981)
	b1 = Book("The Shining", "King, Stephen", 1977)
	b2 = Book("Ready Player One", "Cline, Ernest", 2011)
	bc = BookCollection()
	bc.insert_book(b0)
	bc.insert_book(b1)
	bc.insert_book(b2)
	assert bc.recursive_search_title("CUJO", bc.head) == True
	bc.remove_author("King, Stephen")
	assert bc.recursive_search_title("CUJO", bc.head) == False
	assert bc.recursive_search_title("Twilight", bc.head) == False
	```

	* You can then recursively search through the `BookCollection` sub parts by recursively referring to the next `BookCollectionNode` in `BookCollection` that needs to be searched if the Book in `bookNode` does not have the title we're looking for.
	* **Note:** the input parameter `title` may be in a different case than the case of the title that the Book was constructed with - your solution must account for these situations (see assert statement above).

## testFile.py pytest

This file should import your `Book`, `BookCollection`, and `BookCollectionNode` classes so you can write unit tests using pytest to test your functionality is correct. Think of various scenarios and edge cases when testing your code. Write your tests first in order to check the correctness of the `Book`, `BookCollection` and `BookCollectionNode` methods. Gradescope requires `testfile.py` to be submitted before running any autograded tests. 

You should write at least one test for each method in each of these classes and ensure your test cases are covering all branches of the code effectively (but more tests can help you debug various cases!). See the suggestions above for what potential cases to check.

## Submission

Once you're done with writing your class definitions and tests, submit your `Book.py` and `BookCollection.py` `BookCollectionNode.py`, and `testFile.py` files to the `Lab05` assignment on Gradescope. Remember to remove any `print` statements or put them in the `if __name__ == "__main__":` block in your code since printing may confuse the autograder. There will be various unit tests Gradescope will run to ensure your code is working correctly based on the specifications given in this lab.

If the tests don't pass, you may get some error message that may or may not be obvious. Don't worry - if the tests didn't pass, take a minute to think about what may have caused the error, and try writing more comprehensive tests for various cases. If your tests didn't pass and you're still not sure why you're getting the error, feel free to ask your TAs or Learning Assistants.

---

## Cross-Domain Applications

The programming skills you're developing in this lab extend well beyond just organizing books or security incidents. Here are several ways these skills apply across different domains:

### Data Organization & Analysis
- **Healthcare**: Patient records can be organized by primary physician, treatment dates, and condition severity, allowing for efficient retrieval of medical histories.
- **Financial Services**: Transaction records can be sorted by account, date, and amount for fraud detection algorithms.
- **Research**: Scientific observations can be organized by researcher, experiment date, and measurement type.

### Algorithm Implementation
- The ordered linked list implementation teaches fundamental concepts about data structures that apply to numerous computational problems across fields.
- Understanding insertion ordering logic helps with implementing any priority-based system, from hospital triage to network packet handling.

### Object-Oriented Design
- Creating classes with appropriate attributes and methods is a universal skill in modern software development.
- Operator overloading (like the `>` operator) demonstrates how to customize object behavior for domain-specific applications.

### Testing Methodology
- Writing comprehensive tests with pytest teaches verification practices essential in any field where code reliability matters.
- Edge case identification is particularly valuable in systems where failures could have significant consequences.

### Recursive Problem Solving
- The recursive search implementation develops a thinking pattern applicable to many complex problems across disciplines.
- Fields like artificial intelligence, natural language processing, and mathematics frequently employ recursive approaches.

These skills create a foundation for modeling real-world relationships in code—whether you're working with financial data, scientific measurements, network traffic, or social connections.
The ability to structure, manipulate, and search ordered data is fundamental to computational thinking in virtually every professional domain.

---


## Troubleshooting

* Ensure the `head` is set to `None` to start with an empty list properly.

* Verify that new nodes link correctly during insertion at any position (front, middle, end).

* Double-check the `__gt__` method in Book class for correct author, year, and title comparisons.

* Avoid infinite loops by ensuring loop exit conditions are correct.

* Ensure case-insensitive comparisons for author names; test removals thoroughly to confirm all books by a specific author are removed, including consecutive ones.

* If you get the error `Incorrect logic for get_books_by_author method after adding a single book with author ...` make sure that you correctly implemented the method that the error is alerting you about.

---

<sup>_* Acknowledgment: This lab has been modified in collaboration with Noah Spahn to incorporate cybersecurity context._</sup>
