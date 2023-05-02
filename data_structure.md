# Data Structure
## Array and Strings
### Hash Tables
In this simple implementation, we use an array of linked lists and a hash code function. To insert a key 
(which might be a string or essentially any other data type) and value, we do the following: 
1. First, compute the key's hash code, which will usually be an int or long. Note that two different keys 
could have the same hash code, as there may be an infinite number of keys and a finite number of ints. 
2. Then, map the hash code to an index in the array. This could be done with something like hash (key) % 
array_length. Two different hash codes could, of course, map to the same index. 
3. At this index, there is a linked list of keys and values. Store the key and value in this index. We must use a 
linked list because of collisions: you could have two different keys with the same hash code, or two different 
hash codes that map to the same index. 

```
class HashTable:
    def __init__(self):
        self.size = 10
        self.table = [[] for _ in range(self.size)]

    def _hash_function(self, key):
        return hash(key) % self.size

    def insert(self, key, value):
        hash_value = self._hash_function(key)
        slot = self.table[hash_value]
        for i, (k, v) in enumerate(slot):
            if k == key:
                slot[i] = (key, value)  # Update value if key already exists
                return
        slot.append((key, value))  # Add new key-value pair

    def delete(self, key):
        hash_value = self._hash_function(key)
        slot = self.table[hash_value]
        for i, (k, _) in enumerate(slot):
            if k == key:
                del slot[i]  # Delete key-value pair if key is found
                return

    def get(self, key):
        hash_value = self._hash_function(key)
        slot = self.table[hash_value]
        for k, v in slot:
            if k == key:
                return v  # Return value if key is found
        return None  # Return None if key is not found
```

To retrieve the value pair by its key, you repeat this process. Compute the hash code from the key, and then 
compute the index from the hash code. Then, search through the linked list for the value with this key. 

### Array and Resizable Arrays
In some languages, arrays (often called lists in this case) are automatically resizable. The array or list will 
grow as you append items. In other languages, like Java, arrays are fixed length. The size is defined when 
you create the array.

When you need an array-like data structure that offers dynamic resizing, you would usually use an ArrayList. 
An ArrayList is an array that resizes itself as needed while still providing 0(1) access. A typical implementa￾tion is that when the array is full, the array doubles in size. Each doubling takes 0(n ) time, but happens so 
rarely that its amortized insertion time is still 0(1).

This is an essential data structure for interviews. Be sure you are comfortable with dynamically resizable 
arrays/lists in whatever language you will be working with. Note that the name of the data structure as well 
as the "resizing factor" (which is 2 in Java) can vary. 

## Linked Lists
A linked list is a data structure that represents a sequence of nodes. In a singly linked list, each node 
points to the next node in the linked list. A doubly linked list gives each node pointers to both the next 
node and the previous node. 
### Creating a Linked List
The code below implements a very basic singly linked list.

```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def is_empty(self):
        return self.head is None

    def append(self, data):
        new_node = Node(data)
        if self.is_empty():
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

    def prepend(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node

    def search(self, data):
        current = self.head
        while current:
            if current.data == data:
                return True
            current = current.next
        return False
```

We could, if we chose, implement a LinkedLis t class that wraps the Node class. This would essentially 
just have a single member variable: the head Node.This would largely resolve the earlier issue. 

Remember that when you're discussing a linked list in an interview, you must understand whether it is a 
singly linked list or a doubly linked list. 
### Singly and Doubly Linked List 
In a singly linked list, each node has a link only to the next node in the sequence. The last node in the list points to null, indicating the end of the list. Here's an example of a singly linked list:

>    Node1       Node2       Node3       Node4
>  +-------+   +-------+   +-------+   +-------+
>  |  5    |   |  10   |   |  15   |   |  20   |
>  | next -|--▶| next -|--▶| next -|--▶| null  |
>  +-------+   +-------+   +-------+   +-------+

In a doubly linked list, each node has links to both the next node and the previous node in the sequence. The first node's previous link and the last node's next link point to null. Here's an example of a doubly linked list:

>    Node1       Node2       Node3       Node4
>  +-------+   +-------+   +-------+   +-------+
>  |  5    |   |  10   |   |  15   |   |  20   |
>  | prev -|◀--| next -|--▶| next -|--▶| null  |
>  | next -|--▶| prev -|◀--| prev -|◀--|       |
>  +-------+   +-------+   +-------+   +-------+


### Deleting a Node from a Singly Linked List
Deleting a node from a linked list is fairly straightforward. Given a node n, we find the previous node pre v 
and set prev . nex t equal to n. next . If the list is doubly linked, we must also update n. nex t to set 
n .next . pre v equal to n. prev . The important things to remember are (1) to check for the null pointer 
and (2) to update the head or tail pointer as necessary. 
```
    def delete(self, data):
        if self.is_empty():
            return

        if self.head.data == data:
            self.head = self.head.next
            return

        current = self.head
        while current.next:
            if current.next.data == data:
                current.next = current.next.next
                return
            current = current.next
```

### The Runner Technique
**The "runner"** (or second pointer) technique is used in many linked list problems. The runner technique 
means that you iterate through the linked list with two pointers simultaneously, with one ahead of the 
other. The "fast" node might be ahead by a fixed amount, or it might be hopping multiple nodes for each 
one node that the "slow" node iterates through. 

For example, suppose you had a linked list a t ->a 2 ->. . .->a n ->b 1 ->b J ->. . .->b n and you wanted to 
rearrange it into a i ->b 1 ->a J ->b 7 - > . . . - >3^->bn. You do not know the length of the linked list (but you 
do know that the length is an even number). 

You could have one pointer pi (the fast pointer) move every two elements for every one move that p2 
makes. When pi hits the end of the linked list, p2 will be at the midpoint. Then, move pi back to the front 
and begin "weaving" the elements. On each iteration, p2 selects an element and inserts it after pi .

## Stacks and Queues
### Implementing a Stack
The stack data structure is precisely what it sounds like: a stack of data. In certain types of problems, it can 
be favorable to store data in a stack rather than in an array. 

A stack uses LIFO (last-in first-out) ordering. That is, as in a stack of dinner plates, the most recent item 
added to the stack is the first item to be removed. 

It uses the following operations: 
* pop(): Remove the top item from the stack. 
* push(item) : Add an item to the top of the stack. 
* peek(): Return the top of the stack. 
* is£mpty() : Return true if and only if the stack is empty. 

Unlike an array, a stack does not offer constant-time access to the it h item. However, it does allow constant￾time adds and removes, as it doesn't require shifting elements around. 

One case where stacks are often useful is in certain recursive algorithms. Sometimes you need to push 
temporary data onto a stack as you recurse, but then remove them as you backtrack (for example, because 
the recursive check failed). A stack offers an intuitive way to do this. 

A stack can also be used to implement a recursive algorithm iteratively. (This is a good exercise! Take a 
simple recursive algorithm and implement it iteratively.)
### Implementing a Queue
A queue implements FIFO (first-in first-out) ordering. As in a line or queue at a ticket stand, items are 
removed from the data structure in the same order that they are added.

It uses the operations: 
* add (item) : Add an item to the end of the list. 
* remove(): Remove the first item in the list. 
* peek(): Return the top of the queue. 
* isEmpty() : Return true if and only if the queue is empty. 

One place where queues are often used is in breadth-first search or in implementing a cache. 

## Trees and Graphs
### Types of Trees

A nice way to understand a tree is with a recursive explanation, A tree is a data structure composed of 
nodes:
* Each tree has a root node, (Actually, this isn't strictly necessary in graph theory, but it's usually how we 
use trees in programming, and especially programming interviews.) 
* The root node has zero or more child nodes. 
* Each child node has zero or more child nodes, and so on.

1. Binary Trees
    A binary tree is a tree in which each node has up to two children.
2. Binary Search Tree
    A binary search tree is a binary tree in which every node fits a specific ordering property: all left
    descendent s <= n < all right descendents. This must be true for each node n. 
3. Balanced and Unbalanced
    While many trees are balanced, not all are. Ask your interviewer for clarification here. Note that balancing a 
    tree does not mean the left and right subtrees are exactly the same size (like you see under "perfect binary 
    trees" in the following diagram).

    One way to think about it is that a "balanced" tree really means something more like "not terribly imbalanced."lt's balanced enough to ensure 0( lo g n) times for inser t and find , but it's not necessarily as 
    balanced as it could be. 
4. Complete Binary Trees
    A complete binary tree is a binary tree in which every level of the tree is fully filled, except for perhaps the 
    last level. To the extent that the last level is filled, it is filled left to right.
5. Full Binary Trees
    A full binary tree is a binary tree in which every node has either zero or two children. That is, no nodes have 
    only one child. 
6. Perfect Binary Trees
    A perfect binary tree is one that is both full and complete. All leaf nodes will be at the same level, and this 
    level has the maximum number of nodes.
7. In-Order Traversal
    In-order traversal means to "visit" (often, print) the left branch, then the current node, and finally, the right 
    branch. 
```
    def inorder_traversal(node):
        if node is None:
            return

        inorder_traversal(node.left)
        print(node.data, end=" ")
        inorder_traversal(node.right)
```
    When performed on a binary search tree, it visits the nodes in ascending order (hence the name "in-order").
8. Pre-Order Traversal
    Pre-order traversal visits the current node before its child nodes (hence the name "pre-order").
```
    def preorder_traversal(node):
        if node is None:
            return

        print(node.data, end=" ")
        preorder_traversal(node.left)
        preorder_traversal(node.right)
```
    In a pre-order traversal, the root is always the first node visited. 
9. Post-Order Traversal
    Post-order traversal visits the current node after its child nodes (hence the name "post-order").
```
    def postorder_traversal(node):
        if node is None:
            return

        postorder_traversal(node.left)
        postorder_traversal(node.right)
        print(node.data, end=" ")
```
    In a post-order traversal, the root is always the last node visited. 
### Binary Heaps (Min and Max Heaps)
A min-heap is a complete binary tree (that is, totally filled other than the rightmost elements on the last 
level) where each node is smaller than its children. The root, therefore, is the minimum element in the tree.
We have two key operations on a min-heap: inser t and extract_min . 

**Insert**
When we insert into a min-heap, we always start by inserting the element at the bottom. We insert at the 
rightmost spot so as to maintain the complete tree property. 
Then, we "fix" the tree by swapping the new element with its parent, until we find an appropriate spot for 
the element. We essentially bubble up the minimum element.

**Extract Min Element**
Finding the minimum element of a min-heap is easy: it's always at the top. The trickier part is how to remove 
it.

First, we remove the minimum element and swap it with the last element in the heap (the bottommost, 
rightmost element). Then, we bubble down this element, swapping it with one of its children until the min￾heap property is restored.

This algorithm will also take O( log_n) time. 

### Graphs
A graph is simply a collection of nodes with edges between (some of) them. 
* Graphs can be either directed (like the following graph) or undirected. While directed edges are like a 
one-way street, undirected edges are like a two-way street. 
* The graph might consist of multiple isolated subgraphs. If there is a path between every pair of vertices, 
it is called a "connected graph." 
* The graph can also have cycles (or not). An "acyclic graph" is one without cycles. 

**Adjacency List**
This is the most common way to represent a graph. Every vertex (or node) stores a list of adjacent vertices. 
In an undirected graph, an edge like (a , b) would be stored twice: once in a's adjacent vertices and once 
in b s adjacent vertices. 

**Adjacency Matrices**
An adjacency matrix is an NxN boolean matrix (where N is the number of nodes), where a true value at 
matrix[i][j] indicates an edge from node i to node j. (You can also use an integer matrix with Os and 
1s.) 

**Graph Search**
The two most common ways to search a graph are **depth-first search and breadth-first searc**h. 

In **depth-first search (DFS)**, we start at the root (or another arbitrarily selected node) and explore each 
branch completely before moving on to the next branch. That is, we go deep first (hence the name depth first search)
before we go wide.

In **breadth-first search (BFS)**, we start at the root (or another arbitrarily selected node) and explore each 
neighbor before going on to any of their children. That is, we go wide (hence breadth-first search) before 
we go deep. 
