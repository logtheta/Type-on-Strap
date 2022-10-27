---
layout: post
title: Reverse a Singly Linked List - Python3
author: glaguteta
feature-img: "assets/img/pexels/wall1.jpg"
thumbnail: "assets/img/pexels/computer.jpeg"
tags: [Python3, Coding]
excerpt_separator: <!--more-->
---

## What is a singly linked list?

A Singly Linked List (SLL) is a data structure to represent special graphs in which the nodes are connected by a single reference. 

![]({{ "/assets/img/posts/linked_list2.png" | relative_url}})

In the picture above we can see a generic singly linked list where `[1]` is the head (no previous nodes) and `[3]` the tails (the next node points to *null*). The tipical definition of a SLL node is:
<!--more-->
```python
class Node:
    def __init__(self, val, next:Node=None):
        self.val=val
        self.next=next
```
As we can see the attribute ```val``` doesn't have a type definition, we could host any value, while the attribute `next` represents the next node linked to the current one.

## Reverse a list in place

There are many ways to reverse a singly linked list, some use recursion, some others make use of 3 pointers and perform the inversion node by node. Let's create a class SinglyLinkedList and add some utility methods to populate the list (see function `add_node`)

```python
class SinlgyLinkedList:

    class Node:
        def __init__(self, value, next=None):
            self.value=value
            self.next=next

    def __init__(self):
        self.head=None
        self.size=0

    # This will add a node at the end of the list
    # we could optimized it using a pointer to the tail
    def add_node(self, val):
        node=self.Node(val)
        # the list is empty
        if not self.head:
            self.head = node
        else:
            curr = self.head
            while curr.next:
                curr=curr.next 
            curr.next=node
        self.size +=1
        return node

# Instantiate a SLL object and add nodes
mySLL=SinlgyLinkedList()
mySLL.add_node(1)
mySLL.add_node(3)
mySLL.add_node(2)
mySLL.add_node(3)

```
At this point we have our singly linked list, let's implement reverse:

```python
def reverse_no_pythonic(self, head):
    curr=prev=self.head
    while curr:
        next=curr.next
        curr.next=prev
        prev=curr
        curr=next
```

As you can see we need three pointers:
- `curr`: the current node we are processing
- `prev`: the previous node we processed, needed to reverse the reference
- `next`: and auxiliary pointer to temporarely save `curr.next` before change its value 

The previous implementation can be simplified by using a special feauture provided by Python, multiple variable assignement:

![]({{ "/assets/img/posts/linked_list.png" | relative_url}})


```python
def reverse(self, head):
    curr=prev=self.head
    while curr:
        curr.next, prev, curr = prev, curr, curr.next

    self.head=prev
    return self.head
```
Please notice, when `curr` becomes `curr.next`, the value of `curr.next` is not changed yet by the previous assignement (`curr.next=prev`). All the variable are assigned at the same time but without collisions. This is very handy for example where we want to swap two variables, we could just write:

```python
...

a,b=b,a
...

```

Ok, this is the final complete code to reverse a singly linked list:

```python
class SinlgyLinkedList:

    class Node:
        def __init__(self, value, next=None):
            self.value=value
            self.next=next

    def __init__(self):
        self.head=None
        self.size=0

    # This will add a node at the end of the list
    # we could optimized it using a pointer to the tail
    def add_node(self, val):
        node=self.Node(val)
        # the list is empty
        if not self.head:
            self.head = node
        else:
            curr = self.head
            while curr.next:
                curr=curr.next 
            curr.next=node
        self.size +=1
        return node
    
    # Reverse the list and return then new head
    def reverse(self, head):
        curr=prev=self.head
        while curr:
            curr.next, prev, curr = prev, curr, curr.next

        self.head=prev
        return self.head

# Instantiate a SLL object and add nodes
mySLL=SinlgyLinkedList()
mySLL.add_node(1)
mySLL.add_node(3)
mySLL.add_node(2)
mySLL.add_node(3)

```
