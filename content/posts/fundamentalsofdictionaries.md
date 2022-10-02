+++
title = "Fundamentals of Dictionaries"
description = ""
tags = [
    "python",
    "data structures",
    "development",
]
date = "2021-08-23"
categories = [
    "article",
]
menu = "main"
+++

Let’s say you want to create an inventory of your video games. You are interested in storing information like name, genre, platforms, and ratings. You would like to access this information simply by knowing the name of the video game. Instead of using a database, you compare how practical it is to use dictionaries rather than lists. With a list, you need to store the information sequentially and scan through the whole list to find a particular video game name. On the other hand, with a dictionary, you can define the video game names as “keys” and the rest of the information as “values”. Therefore, instead of reading every item of the dataset, you simply look up the name of the video game (key) to access the information (values).  

## **What is a dictionary?**
A dictionary is a data structure that contains a collection of objects. It represents these objects as key-value pairs. Similar to the key that grants you access to your house’s possessions, dictionaries use keys to get a direct reference to a group of objects. In this sense, a key is unique as each house is. You can grab objects from a dictionary by simply knowing their key. In the literature, you may find other names for dictionaries such as associative arrays, maps, hashes, and hashmaps. 

## **What differences a dictionary from a list?**
What differentiates dictionaries from lists is uniqueness and order. Dictionaries have keys rather than indexes. Each key is unique. Because there are no indexes, elements in a dictionary cannot be sorted out. Therefore, when you add a new key-value pair to a dictionary, it is allocated with no intrinsic order. Keys generally use integers and strings as data types. Values, on the other hand, are not unique and can be of any data type, as shown in **Fig. 1**.

![Dictionary]({{< resource url="/blog/dictionary.png" >}})
**Fig. 1** A sample dictionary that includes three key-value pairs from a video game collection\
&nbsp;


## **What are the main operations on dictionaries?**
The syntaxis and features of dictionaries vary across programming languages. [Here](https://en.wikipedia.org/wiki/Comparison_of_programming_languages_(associative_array)) is a comparison of dictionary features over 40 programming languages. However, typically you can perform the following tasks using dictionaries:

* Lookup a value using its key
* Insert a new key-value pair
* Update a value  
* Remove a key-value pair

## **What are some issues with dictionaries?**
Dictionaries are quite efficient for lookup and insertion operations. They can get the same performance as lists by turning keys into list indexes using a [hash function](https://en.wikipedia.org/wiki/Hash_function). However, when the elements of a dictionary increase, to process for example [big data](https://towardsdatascience.com/python-memory-and-objects-e7bec4a2845), they can consume a lot of resources because they [allocate more memory](https://lerner.co.il/2019/05/12/python-dicts-and-memory-usage/) than they need. Hence, it is essential to be mindful and know your use case scenario for using dictionaries to store and access information. 

## **Conclusion**
In sum, dictionaries represent an efficient way to store and access a collection of objects. These objects have arbitrary indexing and are stored as key-value pairs. If you want to know more about dictionaries, you can consult the following resources:

* [Fundamentals of data structures: Dictionaries](https://en.wikibooks.org/wiki/A-level_Computing/AQA/Paper_1/Fundamentals_of_data_structures/Dictionaries#:~:text=A%20dictionary%20is%20a%20general,has%20a%20single%20associated%20value.&text=Typically%2C%20the%20keys%20in%20a,can%20be%20of%20any%20type.)
* [What’s the use of a Dictionary Data Structure? — With JavaScript](https://medium.com/@the.asantiagojr/whats-the-use-of-a-dictionary-data-structure-with-javascript-620ce087fa65)
* [Dictionaries and Sets](https://www.oreilly.com/library/view/high-performance-python/9781449361747/ch04.html#dict_set_how_work)
