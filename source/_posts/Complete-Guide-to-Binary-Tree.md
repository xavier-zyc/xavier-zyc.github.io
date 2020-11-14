---
title: Complete Guide to Binary Tree
date: 2020-11-08 22:34:08
tags:
  - Binary Tree
  - Algorithm
  - Data Structure
  - Interview
category: Interview
author: xavier
summary: 二叉树完全指南
---
# 二叉树完全指南

## 构造二叉树

### 二叉树节点类

```java
class TreeNode {
  int val;
  TreeNode left;
  TreeNode right;
  TreeNode () {}
  TreeNode (int val, TreeNode left, TreeNode right) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}
```

### 构造二叉树

> 利用完全二叉树数组构造二叉树

```java
TreeNode createTreeNode(int[] __data, int start) {
  // -1 here means null
  if (start > __data.length -1 || -1 == __data[start]) {
    return null;
  }
  TreeNode root = new TreeNode(__data[start]);
  root.left = createTreeNode(__data, 2 * start + 1);
  root.right = createTreeNode(__data, 2 * start + 2);
  return root;
}
```

## 二叉树遍历

### 常用的三种遍历方式

1. 前序遍历 (根左右) - Pre-order traversal (Root Left Right)
2. 中序遍历 (左根右) - In-order traversal (Left Root Right)
3. 后序遍历 (左右根) - Post-order traversal (Left Right Root)

#### 递归方法 - Recursive Approach

```java
void traverse(TreeNode root, List<Integer> result) {
  if (root!= null){
    result.add(root.val);// Pre-order
    traverse(root.left, result);
    // result.add(root.val);// In-order
    traverse(root.right, result);`
    // result.add(root.val);// Post-order
  }
}
```

#### 非递归方法 - Iterative Approach

```java
List<Integer> traverse(TreeNode root) {
  //
}
```