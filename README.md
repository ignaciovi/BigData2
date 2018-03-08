# Page Rank with Spark in Java
Our dataset is constituted of Wikipedia articles from its creation until the year 2008.

In this project, we have change the provided Page Rank algorithm. Page Rank is used in search engines as a way of measuring the importance of website pages. The algorithm have several DAG transformations which are:

# Map
We take the input (whole article) and divide it by lines. A list of strings is returned, where each position is a line from that article.

# MapToPair
A list of lines is received, we store the article title, the revision date and the outlinks and a tuple(String and List of Strings) is returned, where the String is the article title and the List of Strings have in its first position the revision date and then all the outlinks for that article.

# ReduceByKey
For same key (same articles title) pairs of lists are received. We then select the list with the appropiate revision date, and it is returned.

# MapToPair
Receive an article title as Key and a list with a date and outlinks as the Value. Here we remove duplicated oulinks, the date (we do not need it anymore since we already have the right article chosen) and self loops, i.e. remove outlinks that are same than the article title. This returns a tuple such as: *(String articleTitle, List<String> outlinks)*

# MapValues
We receive a list of outlinks and we return each of the the outlinks and a double 1.0 (the starting poing for the page rank algorithm)

//TODO nacho, deberiamos cambiar las cosas y decir solo las nuevas y quitar las que ya estaban?
# For loop for calculating score
## Join
## Values
## FlapMapToPair
## ReduceByKey

# Map
For swapping key for value so we can order them

# SortBy
It sorts the keys in descending order (key now is the score)

# Map
For swapping again

# SaveAsTextFile
It saves the output in a file.
