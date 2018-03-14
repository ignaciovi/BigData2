Mario Llamas Lanza 2346097L
Ignacio Valdelvira Isla 2340187V

# Page Rank with Spark in Java
Our dataset is constituted of Wikipedia articles from its creation until the year 2008.

In this project, we have changed the Page Rank algorithm provided in the lecture slides. Page Rank is used in search engines as a way of measuring the importance of website pages. The algorithm has several DAG transformations which are, in order of appearance:

# Map
We take the input (whole article) and divide it by lines. A list of strings is returned, where each position is a line from that article.

# MapToPair
A list of lines is received, we store the article title, the revision date and the outlinks. A tuple (String and List of Strings) is returned, where the String is the article title and the List of Strings have in its first position the revision date and, after that, all the outlinks for that article.

# ReduceByKey
For same key (same articles title) pairs of lists are received. We then select the list with the appropiate revision date, and it is returned.

# MapToPair
Receive an article title as Key and a list with a date and outlinks as the Value. Here we remove duplicated oulinks, the date (we do not need it anymore since we already have the right article chosen) and self loops, i.e. remove outlinks that are same than the article title. This returns a tuple such as: *(String articleTitle, List<String> outlinks)*

# MapValues
We receive a list of outlinks and we return each of the outlinks and a double 1.0 (the starting point for the page rank algorithm)

# Calculating score
The input is article title, outlinks and a 1.0. We start with the first iteration.

For every outlink, we calculate rank/(number of outlinks in the article title). In the first iteration, the starting rank will be 1.0.

For all the article titles that aren't outlinks of any other title, we assign always 0 value to its previous score. Therefore, the articles that are not outlinks of any other title will have rank = 0.15, because 0.15 + 0.85x0.

At the end of the iteration, we calculate the new rank and go back to another iteration changing 1.0 by the new rank. We repeat the rank calculation for all the iterations stated.

# Map
The final step will be to sort all the scores in a descendent order. We will swap key for value because we will apply sortby.

# SortBy
If all the keys are now the scores, we have an easy way to sort them in a descending order.

# Map
For swapping again so we can print the results properly.

# SaveAsTextFile
It saves the output in a file.




