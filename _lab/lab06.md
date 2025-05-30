---
layout: lab
num: lab06
ready: true
desc: "Sorting Apartments"
assigned: 2024-05-14 23:59:59.59-7
due: 2024-05-20 23:59:59.59-7
---

# Introduction

In this lab, you'll have the opportunity to practice:

* Defining classes in Python
* Overloading the `==`, `<`, and `>` operators in a Python class
* Implementing an **O(n log n)** mergesort on a list of Apartment objects
* Writing functions that ensure the list of Apartment objects are in sorted order
* Determining the best/worst apartment in a list
* Listing out all of the apartments that are affordable
* Testing your functionality with pytest

**Note:** It is important that you start this lab early so you can utilize our office hours to seek assistance / ask clarifying questions during the week before the deadline if needed!


For this lab, you have been hired as a realtor for an up-and-coming property management company located in Isla Vista. You are tasked with renting out as many apartments as you can. In order to do so, you will write a program that will sort apartment objects. You have decided that the three most important properties of an Apartment object are its **rent**, **meters from UCSB**, and **condition**. You have decided to sort Apartments as follows. First, you will organize the Apartment by increasing rent. In the event of a tie (several Apartments have the same rent), the meters from UCSB will be used to determine the Apartment's place in the list. The closer the apartment is to campus, the better. If the rent and the meters from campus are the same, then the Apartment's condition will be used to determine the Apartment's place in the list. An apartment can have either a `"bad"`, `"average"`, or `"excellent"` condition - the better the condition is, the better the apartment. You may assume that apartment objects will have either `"bad"`, `"average"`, or `"excellent"` as their condition when comparing / sorting apartments.

## Cybersecurity Context
The apartment sorting algorithm teaches you to classify and prioritize data based on multiple attributes - a critical skill in security incident response. When security analysts face numerous alerts, they must quickly determine which potential threats deserve immediate attention based on multiple criteria (severity, asset value, exploit availability, etc.).

By implementing custom comparison operators for apartment objects, you're learning how to create sophisticated rules for comparing complex objects - essential when building:

- Threat intelligence prioritization systems
- Vulnerability management platforms
- Security event correlation engines

The `get_affordable_apartments()` function demonstrates filtering data based on thresholds - similar to how security tools filter events based on risk scores or confidence values.


This lab will require you to define an `Apartment` class and create the file `lab06.py`. Note that `labO6.py` *is not a class*.

# Instructions

You will need to create three files:
* `Apartment.py` - file containing a class definition for an Apartment object
* `lab06.py` - file containing mergesort and other functions defined in the `lab06.py` section of this lab.
* `testFile.py` - file containing pytest functions testing the overall correctness of your class definitions

There will be no starter code for this assignment, but rather the class descriptions and required methods are defined in the specification below.

You should organize your lab work in its own directory. This way all files for a lab are located in a single folder. Also, this will be easy to import various files into your code using the `import / from` technique shown in lecture.

# `Apartment.py` class

The `Apartment.py` file will contain the definition of an `Apartment`. We will define the Apartment attributes as follows:

* `rent` - integer that represents the rent of the Apartment
* `meters_from_UCSB` - integer that represents the Apartment's distance, in meters, from UCSB
* `condition` - string that represents the condition of the Apartment. This string will be one of three options: `"bad"`, `"average"`, or `"excellent"`.

You should write a constructor that allows the user to construct an apartment object by passing in values for all of the fields. You may assume that all attributes of the Apartment object will be defined. Therefore, there should be no default values for `rent`, `metersFromUCSB`, or `condition`.

* `__init__(self, rent, meters_from_UCSB, condition)`

In addition to your constructor, your class definition should also support "getter" methods that can receive the state of the Apartment object:

* `get_rent(self)`
* `get_meters_from_UCSB(self)`
* `get_condition(self)`

You will also implement the method

* `get_apartment_details(self)`

that returns a `str` with all of the Apartment attributes. The string should contain all attributes in the following EXACT format (**Note: There is no `\n` character at the end of this string**):

```python
a0 = Apartment(1204, 200, "bad")
print(a0.get_apartment_details())
```

<b>Output</b>

```
(Apartment) Rent: $1204, Distance From UCSB: 200m, Condition: bad
```

* Lastly, your `Apartment` class should overload the `>`,`<`, and `==` operators. This will be used when finding the proper position of an Apartment in the list using the specifications (first by rent, then distance and then condition) in the **Introduction** section of this lab. In this context for example, the `<` operator will return True for `Apartment1 < Apartment2` if Apartment1 is **better than** Apartment2. We reviewed operator overloading in class and the textbook does discuss overloading Python operators. You can also refer to this reference on overloading various operators as well:

[https://www.geeksforgeeks.org/operator-overloading-in-python/](https://www.geeksforgeeks.org/operator-overloading-in-python/)


## A Brief Note on Sorting Apartments

A common question that students have when working through this lab is

*The directions say that a0 < a1 should return true if apartment a0 is a better apartment than a1. Intuitively though, why would the apartment that is lesser (<) be "better than" the other apartment?*

Recall that you are sorting apartments in ascending order. For example, if you sorted runners in a race by the position they finished in you would do something like this:
```
 1 4 3 2 5 —> 1 2 3 4 5
```

It is clear that 1<2, 2<3 etc. Notice that the 1st place runner finished in a “better” position even though they have a “lesser” position than the others. The same concept applies here to apartments.



# `lab06.py`

This file will contain functions that sort a list of Apartment objects, ensures that the list of Apartment objects are in asending order (best-to-worst), retrives information about the best/worst apartments, and gets the info of every affordable apartment in the list. These function defintions as well as their descriptions are provided below. Note that in order for the autograder to correctly check your implementation, function defintions must match exactly.

* `merge_sort(apartmentList)` - Performs a mergesort on the apartmentList passed as input. Sorts the Apartment objects based on the specifications in the **Introduction** section of this lab. **Gradescope will test to ensure that your mergesort implementation's Big-O is O(NlogN)**. You may refer to the implementation given in the textbook.
* `ensure_sorted_ascending(apartmentList)` - method that returns a boolean value. True if the apartmentList is sorted correctly in asending order. False otherwise.
* `get_best_apartment(apartmentList)` - method that returns a string detailing the **best** Apartment's rent, meters from UCSB, and condition. Make use of `get_apartment_details(self)` and `merge_sort(apartmentList)`. You can assume that apartmentList has at least one apartment.
* `get_worst_apartment(apartmentList)` - method that returns a string detailing the **worst** Apartment's rent, meters from UCSB, and condition. Make use of `get_apartment_details(self)` and `merge_sort(apartmentList)`. You can assume that apartmentList has at least one apartment.
* `get_affordable_apartments(apartmentList, budget)` - method that returns a labeled, newline separated string detailing the rent, meters from UCSB, and condition of **all** the apartments **whose rent is less than or equal to `budget`** from the apartmentList **in sorted order**. Make use of `get_apartment_details(self)` and `merge_sort(apartmentList)`.
**Note:** You can assume that apartmentList has at least one apartment and that there is no newline at the end of the string returned by this method. If there are no apartments that are affordable in the apartmentList, this method returns an empty string.

# How to Best Approach This Lab

There are a lot of parts to this lab that rely on one another. So if you're failing a test and find yourself stuck it might be because of code that you've written elsewhere. To alleviate some of this stress, here are the suggested order in which you complete the functions required for this lab:

1. constructor and getters in `Apartment.py`
2. `get_apartment_details` in `Apartment.py`
3. `<`, `>`, and `==` overloaded operators in `Apartment.py`
3. `ensure_sorted_ascending` in `lab06.py`
4. `merge_sort` in `lab06.py`
5. `get_best_apartment` and `get_worst_apartment` in `lab06.py`
6. `get_affordable_apartments` in `lab06.py`

# Sample Output 1

```python
a0 = Apartment(1115, 215, "bad")
a1 = Apartment(950, 215, "average")
a2 = Apartment(950, 215, "excellent")
a3 = Apartment(950, 190, "excellent")
a4 = Apartment(900, 190, "excellent")
a5 = Apartment(500, 250, "bad")
apartmentList = [a0, a1, a2, a3, a4, a5]


print('apartmentList is NOT SORTED:')
for apartment in apartmentList:
    print(apartment.get_apartment_details())

assert ensure_sorted_ascending(apartmentList) == False
merge_sort(apartmentList)
assert ensure_sorted_ascending(apartmentList) == True

print('apartmentList is SORTED:')
for apartment in apartmentList:
    print(apartment.get_apartment_details())
```

<b> Output: </b>

```
apartmentList is NOT SORTED:
(Apartment) Rent: $1115, Distance From UCSB: 215m, Condition: bad
(Apartment) Rent: $950, Distance From UCSB: 215m, Condition: average
(Apartment) Rent: $950, Distance From UCSB: 215m, Condition: excellent
(Apartment) Rent: $950, Distance From UCSB: 190m, Condition: excellent
(Apartment) Rent: $900, Distance From UCSB: 190m, Condition: excellent
(Apartment) Rent: $500, Distance From UCSB: 250m, Condition: bad
apartmentList is SORTED:
(Apartment) Rent: $500, Distance From UCSB: 250m, Condition: bad
(Apartment) Rent: $900, Distance From UCSB: 190m, Condition: excellent
(Apartment) Rent: $950, Distance From UCSB: 190m, Condition: excellent
(Apartment) Rent: $950, Distance From UCSB: 215m, Condition: excellent
(Apartment) Rent: $950, Distance From UCSB: 215m, Condition: average
(Apartment) Rent: $1115, Distance From UCSB: 215m, Condition: bad
```

# Sample Output 2

```python
a0 = Apartment(1200, 200, "average")
a1 = Apartment(1200, 200, "excellent")
a2 = Apartment(1000, 100, "average")
a3 = Apartment(1000, 215, "excellent")
a4 = Apartment(700, 315, "bad")
a5 = Apartment(800, 250, "excellent")
apartmentList = [a0, a1, a2, a3, a4, a5]

assert ensure_sorted_ascending(apartmentList) == False

print('Best Apartment in apartmentList:')
print(get_best_apartment(apartmentList))

print('Worst Apartment in apartmentList:')
print(get_worst_apartment(apartmentList))

```

<b> Output: </b>

```
Best Apartment in apartmentList:
(Apartment) Rent: $700, Distance From UCSB: 315m, Condition: bad
Worst Apartment in apartmentList:
(Apartment) Rent: $1200, Distance From UCSB: 200m, Condition: average
```

# Sample Output 3

```python
a0 = Apartment(1115, 215, "bad")
a1 = Apartment(970, 215, "average")
a2 = Apartment(950, 215, "average")
a3 = Apartment(950, 190, "excellent")
a4 = Apartment(900, 190, "excellent")
a5 = Apartment(500, 250, "bad")
apartmentList = [a0, a1, a2, a3, a4, a5]

print('All apartments whose rent is <= in SORTED order:')
print(get_affordable_apartments(apartmentList, 950))

```

<b> Output: </b>

```
All apartments whose rent is <= in SORTED order:
(Apartment) Rent: $500, Distance From UCSB: 250m, Condition: bad
(Apartment) Rent: $900, Distance From UCSB: 190m, Condition: excellent
(Apartment) Rent: $950, Distance From UCSB: 190m, Condition: excellent
(Apartment) Rent: $950, Distance From UCSB: 215m, Condition: average
```


# Cross-Domain Applications
This lab develops fundamental skills valuable across multiple disciplines. For example:
 - **Economics**: Sorting financial data based on multiple attributes for portfolio optimization, filtering investments based on risk thresholds, and analyzing market trends from large datasets.
- **Applied Mathematics**: Implementing efficient algorithms for large dataset analysis, creating custom comparison logic for complex mathematical objects, and developing rigorous testing frameworks to validate computational models.
- **Biology**: Sorting genetic sequences or protein structures based on multiple properties, filtering specimens based on specific criteria, and efficiently processing large genomic datasets for pattern identification and classification.

These programming fundamentals enable students to handle complex, multi-attribute data analysis challenges essential in research and industry applications across diverse fields.


## testFile.py pytest

This file should import your `Apartment.py` class and your `lab06.py` function. You should write tests using pytest to test if the functionality is correct. Think of various scenarios and edge cases when testing your code. Write your tests first in order to check the correctness of the `Apartment` and then `lab06.py` methods. Gradescope requires `testFile.py` to be submitted before running any autograded tests. You should write at least one test for each method in each of these classes. This includes the overloaded operators but excludes the getters.

## Submission

Once you're done with writing your recursive function definitions and tests, submit your `Apartment.py` and `lab06.py` to the `Lab06` assignment on Gradescope. There will be various unit tests Gradescope will run to ensure your code is working correctly based on the specifications given in this lab. There also will be tests to ensure that your mergesort in `lab06.py` runs in **O(n log n)** time. Note that if your autograder seems to be running for a really long time, your mergesort does not run O(NlogN).

If the tests don't pass, you may get some error message that may or may not be obvious at this point. Don't worry - if the tests didn't pass, take a minute to think about what may have caused the error. If your tests didn't pass and you're still not sure why you're getting the error, feel free to ask your TAs or Learning Assistants.

---

<sup>_* Acknowledgment: This lab has been modified in collaboration with Noah Spahn to incorporate cybersecurity context._</sup>
