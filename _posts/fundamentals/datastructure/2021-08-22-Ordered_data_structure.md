---
the valayout: post
title: <ACSF> [Week2 - Binary Trees] Ordered Data Structures
subtitle : Accelerated Computer Science Fundamentals Specialization course from Coursera
tags: [datastructure, coursera]
author: Leena Kim
comments : true
---



< Coursera Ordered Data Structures >



# Tree Terminology

- A tree is a linked structure with a sense of ancestry (parents, children, siblings, and more)!
- Each element in our tree is a **node**
- Each connection between two nodes is an **edge**
- Tree must always contain a **root node** that has no incoming edges.



![ACSF22](/assets/img/post_img/ACSF/ACSF22.png)

- Nodes that contain no outgoing edges are called **leaf nodes.**



![ACSF23](/assets/img/post_img/ACSF/ACSF23.png)

- In a tree, the nodes will store data and amy be labeled.
- Edges do not have names, but are referred to by the nodes they connect.

- Every node, except the root node, has exactly **one parent node.**
- A node's **children** are the nodes with that node as it's parent. (It's possible to have anywhere from 0 to infinite children..)

- Most ancestry terms apply as expected:
  - Sibling : B and D are siblings
  - Ancestor : M, L, and D share A as a common ancestor
  - Grandchild / grandchildren : M is a D's grandchild
  - Grandparent : D is M's grandparent
- Finally, to be a **tree**, tree conditions **must** be true:
  - Must have a root
  - Must have directed edges
  - **Must not have a cycle** (never have a loop)
  - => We say a tree is a "**rooted, directed,** and **acyclic**" structure.



## Summary of Tree

- Trees formed with nodes and edges
- Trees must be rooted, directed, and acyclic
- The relationship between nodes in a tree follow classical ancestry terms (parent, child, etc)



# Binary Trees

![ACSF24](/assets/img/post_img/ACSF/ACSF24.png)

- A binary tree is a tree where every node has at most two children (maximum 2 children)



![ACSF25](/assets/img/post_img/ACSF/ACSF25.png)

- In binary trees, we will label every child as either the **"left child"** or **"right child"** of its parent



```c++
#pragma once

template <typename T>
class BinaryTree {
  public:
    // ...

  private:
    class TreeNode {
      public:
        T & data;
        TreeNode* left;
        TreeNode* right;
        TreeNode(T & data) : data(data), left(nullptr), right(nullptr) { }
    };

    TreeNode *root_;
};
```





## Binary Tree Property: Height

- The **height** of a binary tree is the number of <u>edges</u> in the longest path from the root to a leaf.

![ACSF26](/assets/img/post_img/ACSF/ACSF26.png)



## Binary Tree Property: Full

- A binary tree is **full** if and only if every node has either zero children or two children.

![ACSF27](/assets/img/post_img/ACSF/ACSF27.png)



## Binary Tree Property: Perfect

- A binary tree is **perfect** if and only if all interior nodes have two children and leaves are at the same level.

![ACSF28](/assets/img/post_img/ACSF/ACSF28.png)



## Binary Tree Property: Complete

- A binary tree is **complete** if and only if the tree is perfect up until the last level and all leaf nodes on the last level are pushed to the left.

![ACSF29](/assets/img/post_img/ACSF/ACSF29.png)

## Puzzle:

- Is a **full** tree **complete**?
  - NO.
  - full tree is the tree that has only one or two children
  - complete tree is the tree that is perfect and left biased
  - If a full tree's last right-node has two children, it is not a complete tree because it's right biased.
- Is a **complete** tree **full**?
  - NO.
  - If a complete tree's last node is left biased but has only left node, it's not a full tree.
  - ![ACSF30](/assets/img/post_img/ACSF/ACSF30.png)



## Summary of Binary Trees

- Binary Trees are a special case of a tree where each node has at most two children.
- The children of binary trees are referred to as the "left child" and "right child".