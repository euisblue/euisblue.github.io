---
layout: post
title:  "二分木（Binary Tree）"
subtitle: "二分木の特性やタイプそしてツリーの巡回について知る。"
date:   2021-07-18 07:00:00 +1400
header-img: "img/post-bg-ds-algo.jpg"
header-mask: 0.6
catalog: true
lang: "ja"
korean: true
english: true

published: true
hidden: false

permalink: /ja/ds/binary-tree/
tags:
  - data structure  
  - binary tree
  - tree
---

<style>
    img {
        margin: 1em 0 !important;
    }
</style>

# 二分木とは
二分木（英: Binary Tree）は木構造の一つで、全ての親ノードが二つまたはその以下の子ノード持つ構造です。

![BST Node](/img/in-post/ds-algo/tree/bst-node.svg)

[ツリー](/ja/ds/tree)と同じく二分木にもサイクルないです。

## 特性

> 根ノードとレベルと高さは両方０から始まります。

1. レベル`i`の二分木は最大`2^(i+1) - 1`のノードを持つ。
2. Total number of leaf node is equal to the total number of parents with two child nodes + 1.
3. 高さ`h`の二分木は最大`2^(h+1) - 1`のノードを持つ。
4. `n`個のノードを持つ二分木の高さは最初`log_2(n)`、そして最大`n-1`になる。
5. `n`個のノードを持つ二分木はちょど`n+1`個の`null`を指す。

## 二分木のタイプ
### 二分探索木 
- 英: Binary Search Tree, BST
+ 左子のデータが親ノードより小さい。
+ 右子のデータは親ノードより大きい。
![BST](/img/in-post/ds-algo/tree/bst.svg)

### Full/Strict 二分木
- 英: Full/Strict Binary Tree
+ Nodes are filled in order from left to right.
+ Every internal node has exactly 2 child nodes.
+ The bottom level does not have to be full.
![Full 二分木](/img/in-post/ds-algo/tree/fullbt.svg)

### Complete 二分木
- 英: Complete Binary Tree
+ Every internal node has either 0 or 2 child nodes.
![Complete 二分木](/img/in-post/ds-algo/tree/completebt.svg)

### Perfect 二分木
- 英: Perfect Binary Tree
+ A 二分木 that is both Complete and Full.
+ There are exactly `2^(h+1) - 1` nodes.
![Perfect 二分木](/img/in-post/ds-algo/tree/perfectbt.svg)

## ツリーの巡回

![二分木 Traversals](/img/in-post/ds-algo/tree/traversal.svg)

### Inorder
```cpp
void BinaryTree::inorder(Node *node) {
  if(node) {
    inorder(node->left);
    cout << node->data << ' ';
    inorder(node->right);
  }
}
```

### Preorder
```cpp
void BinaryTree::preorder(Node *node) {
  if(node) {
    cout << node->data << ' ';
    preorder(node->left);
    preorder(node->right);
  }
}
```

### Postorder
```cpp
void BinaryTree::postorder(Node *node) {
  if(node) {
    postorder(node->left);
    postorder(node->right);
    cout << node->data << ' ';
  }
}
```

## ノードの追加

This function basically creates a Full 二分木 where nodes are filled from left to right.

<br>

Steps:
1. If `root` is empty, let new node be the `root`.
2. Use *queue* to explore the tree in level order. <br>
    2-1) Insert the new node at current node's left if it's empty, else enqueue the node. <br>
    2-2) Insert the new node at current node's right if it's empty, else enqueue the node.<br>
3. Repeat the step #2 until *queue* is empty.

```cpp
void BinaryTree::insertNode(int data) {
  if(!root) root = new Node(data);
  else {
    queue<Node *> q;

    q.push(root);

    while(!q.empty()) {
      Node *temp = q.front();
      q.pop();

      if(temp->left) {
        q.push(temp->left);
      } else {
        temp->left = new Node(data);
        ++size;
        return;
      }

      if(temp->right) {
        q.push(temp->right);
      } else {
        temp->right = new Node(data);
        ++size;
        return;
      }
    }
  }
}
```

## ノードの除去

Find the leaf node (the right-most node at the bottom level), and delete it.

<br>

```cpp
void BinaryTree::deleteNode(void) {
  if(!root) return;

  if(root->left == nullptr && root->right == nullptr) {
    delete root;
    root = nullptr;
    return;
  }

  Node *lastLevelLevelOrder = nullptr;
  Node *parentOfLastNode = nullptr;
  queue<Node *> q;
  q.push(root);

  while(!q.empty()) {
    Node *temp = q.front();
    q.pop();

    if(temp->left) {
      q.push(temp->left);

      if(temp->left->left == nullptr && temp->left->right == nullptr) {
        lastLevelLevelOrder = temp->left;
        parentOfLastNode = temp;
      }
    }

    if(temp->right) {
      q.push(temp->right);
      if(temp->right->left == nullptr && temp->right->right == nullptr) {
        lastLevelLevelOrder = temp->right;
        parentOfLastNode = temp;
      }
    }
  }

  if(lastLevelLevelOrder && parentOfLastNode) {
    if(parentOfLastNode->right) {
      delete parentOfLastNode->right;
      parentOfLastNode->right = nullptr;
    } else {
      delete parentOfLastNode->left;
      parentOfLastNode->left = nullptr;
    }
  } else {
    cout << "Empty Tree" << endl;
  }
}
```

## 練習問題
- [617. Merge Two 二分木s](https://leetcode.com/problems/merge-two-binary-trees/) ([solution](https://github.com/euisblue/cp/tree/leetcode/easy/617/617.cpp))

--- 

### 参考したサイト
- [https://www.tutorialspoint.com/data_structures_algorithms/tree_data_structure.htm](https://www.tutorialspoint.com/data_structures_algorithms/tree_data_structure.htm)
- [https://fe-churi.tistory.com/16](https://fe-churi.tistory.com/16)
- [https://www.baeldung.com/cs/binary-tree-intro](https://www.baeldung.com/cs/binary-tree-intro)
- [https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)
- [https://www.geeksforgeeks.org/delete-the-last-leaf-node-in-a-binary-tree/](https://www.geeksforgeeks.org/delete-the-last-leaf-node-in-a-binary-tree/)
