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

##### 前序遍历 + 中序遍历

```java
List<Integer> traverse(TreeNode root) {
  // Pre-order and In-order
  Stack<TreeNode> sk = new Stack<>();
  TreeNode node = root;
  while (!sk.isEmpty() || node != null) {
    while (node != null) {
      sk.push(node);
      result.add(node.val);// Pre-order
      node = node.left;
    }
    if (!sk.isEmpty()) {
      node = sk.pop();
      // result.add(node.val);//In-order
      node = node.right;
    }
  }
  return result;
}
```

##### 后序遍历

```java
List<Integer> traverse(TreeNode root) {
  // Pre-order and In-order
  Stack<TreeNode> sk = new Stack<>();
  TreeNode node = root;
  TreeNode lastVisit = root;
  while (!sk.isEmpty() || node != null) {
    while (node != null) {
      sk.push(node);
      node = node.left;
    }
    node = sk.peek();
    if (node.right == null || node.right == lastVisit) {
      result.add(node.val);
      sk.pop();
      node = null;
    } else {
      node = node.right;
    }
  }
  return result;
}
```

## 反转二叉树

原二叉树

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

反转后的二叉树

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

### 递归思路： 

1. 判断根是否为空，为空直接返回根，否则继续
2. 递归反转根子树

```java
TreeNode invertNode(TreeNode root) {
  if (null == root) return root;
  TreeNode left = root.left;
  root.left = invertNode(root.right);
  root.right = invertNode(left);
  return root;
}
```

### 非递归思路：

1. 判断根是否为空，根为空直接返回根，否则继续
2. 交换根节点的左右子节点
3. 交换第二层的左右子树
4. 重复下去，直到最后一个节点

```java
TreeNode invertNode(TreeNode root) {
  if (null == root) return root;
  Queue<TreeNode> queue = new LinkedList<TreeNode>();
  queue.add(root);
  while(queue != null) {
    TreeNode current = queue.poll();
    TreeNode __left = current.left;
    current.left = current.right;
    current.right = __left;
    while (null !== current.left) {
      queue.add(current.left);
    }
    while (null !== current.right) {
      queue.add(current.right);
    }
  }
  return root;
}
```