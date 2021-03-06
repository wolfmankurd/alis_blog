---
layout: post
title:  "Anigramer - A simple C anigram finder"
date:   2015-10-23-12-00-00
categories: anigramer c
---

I spent today having some fun with anigrams using my simple anigramer. This program written in C (using libreadline) takes input from a wordlist and stdin allowing you to search for anigrams.

It does this rather quickly by first pasting the wordlist into a binary heap with anigrams in a linked list and then searching the binary heap for your input.

It shows use of libreadline (awesome library) and the power of linked lists and binary heap trees. Linked lists can easily be made with C.

{% highlight c %}
struct linkedlist_node_s {
       void *data;
       struct *linkedlist_node_s;
};
typedef struct linkedlist_node_s ll_node;
{% endhighlight %}

This simple struct defines a singly linked list node. Which is a great data structure when you need to access data quickly for example our wordlist however to find a particularly element in a dataset of N takes on average N/2 comparisons (if the list is unordered).

This is fine by us since we simply need to print out the entire linked list of anagrams.

A binary tree on the other hand holds data in a sorted fashion.

{% highlight c %}
struct binarytree_node_s {
       ll_node *list;
       struct binarytree_node_s *left;
       struct binarytree_node_s *right;
};
typedef struct binarytree_node_s bintree_node;
{% endhighlight %}

As elements are added to a binary tree they go on the left or right of a node depending on a comparison function we'll use strcmp for this. And it's a good template for any [comparison function](http://www.gnu.org/software/libc/manual/html_node/Comparison-Functions.html#Comparison-Functions) you need such as for qsort. It returns a value less than, equal to or greater than zero.
The cool thing about a binary tree is you greatly reduce the number of comparisons you need to do to find an item. If the binarytree contains N items you would need to do on average ln(N+1)/ln(2) searches.

![Binary Heap trees quickly outperform linked lists]({{ site.url }}/~ali/upload/bintreevlinkedlist.png)

You can find the code [here](https://github.com/wolfmankurd/anigramer). I'll be writing some more posts on the ins and outs and breaking down the code.

Enjoy,

Ali
