+++
title = "Fundamentals of Dictionaries"
description = "Created in 2021-08-23"
tags = [
    "python",
    "data structures",
    "development",
]
date = "2023-05-17"
categories = [
    "article",
]
menu = "main"
+++

Are you interested in learning about a more efficient way to store and access information than using a traditional list? Consider using dictionaries. A dictionary, also known as an associative array, map, hash, or hash map, is a data structure that represents objects as key-value pairs, making it easy to access information by knowing a key. 

For instance, suppose you want to create an inventory of your video games, including information like name, genre, platforms, and ratings. Instead of using a list and scanning through it to find a particular video game feature, you can define the name of the video game as a key and the rest of its information as values in a dictionary, as shown in **Fig. 1**. This way, you only need to look up the name of the video game (key) to access its information (values).

![Dictionary]({{< resource url="/blog/dictionary.png" >}})
**Fig. 1** A sample dictionary that includes three key-value pairs from a video game collection\
&nbsp;

## **What differentiates a dictionary from a list?**
Uniqueness and order. Dictionaries have keys rather than indexes and each key is unique. Generally, keys are integer or string data types. Values, on the other hand, are not unique and can be of any data type, as shown in **Fig. 1**. Because dictionaries lack indexes, elements in a dictionary cannot be sorted out. Therefore, when you add a new key-value pair to a dictionary, it is allocated with no intrinsic order.

## **What are the main operations on dictionaries?**
Although the [syntax and features of dictionaries](https://en.wikipedia.org/wiki/Comparison_of_programming_languages_(associative_array)) can vary across programming languages, typically you can perform the following tasks:

* Lookup a value using its key
* Insert a new key-value pair
* Update a value  
* Remove a key-value pair

## **What are some issues with dictionaries?**
Dictionaries are quite efficient for lookup and insertion operations. They can get the same performance as lists by turning keys into list indexes using a [hash function](https://en.wikipedia.org/wiki/Hash_function). However, when processing [large data](https://towardsdatascience.com/python-memory-and-objects-e7bec4a2845), dictionaries can consume a lot of resources because they are prone to [allocating more memory](https://lerner.co.il/2019/05/12/python-dicts-and-memory-usage/) than needed. Therefore, it is essential to consider your use case scenario before using dictionaries to store and access information.

## **Conclusion**
Unlike traditional lists, dictionaries represent an efficient way to store and access a collection of objects using key-value pairs. If you’re interested in learning more about dictionaries, you can consult the following resources:

* [Fundamentals of data structures: Dictionaries](https://en.wikibooks.org/wiki/A-level_Computing/AQA/Paper_1/Fundamentals_of_data_structures/Dictionaries#:~:text=A%20dictionary%20is%20a%20general,has%20a%20single%20associated%20value.&text=Typically%2C%20the%20keys%20in%20a,can%20be%20of%20any%20type.)
* [What’s the use of a Dictionary Data Structure? — With JavaScript](https://medium.com/@the.asantiagojr/whats-the-use-of-a-dictionary-data-structure-with-javascript-620ce087fa65)
* [Dictionaries and Sets](https://www.oreilly.com/library/view/high-performance-python/9781449361747/ch04.html#dict_set_how_work)
