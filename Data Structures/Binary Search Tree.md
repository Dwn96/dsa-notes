# **Binary Search Tree (BST)**

## **1. What is a BST?**

A Binary Search Tree is a binary tree that follows a specific ordering rule:

- **Left subtree:** All values are smaller than the current node.    
- **Right subtree:** All values are greater than the current node.    
- **Duplicates:** Typically not allowed in standard BST problems unless explicitly specified.
    

This rule applies to every node in the tree, not just the root.

Example:

```
        8
       / \
      3   10
     / \    \
    1   6    14
       / \   /
      4   7 13
```

## **2. How BSTs work**

The ordering property makes searching much faster than searching an ordinary binary tree.

At every node:

- If the target is smaller, go left.    
- If the target is greater, go right.    
- If the target equals the current node, you've found it.
    

**Example: Search for 7**

```
        8
       /
      3
       \
        6
         \
          7
```

1. 7 is smaller than 8. Go left.    
2. 7 is greater than 3. Go right.    
3. 7 is greater than 6. Go right.    
4. Found 7!
    

We never needed to visit the entire tree.

## **3. Common BST operations**

### **Searching**

```js
function searchBST(root, val) {
    let curr = root;

    while(curr) {
        if(val < curr.val) {
            curr = curr.left;
        }
        else if(val > curr.val) {
            curr = curr.right;
        }
        else {
            return curr;
        }
    }

    return null;
}
```

### **Insertion**

The idea is to find the correct empty position while maintaining the BST ordering property.

```js
function insertIntoBST(root, val) {
    if(!root) return new TreeNode(val);

    if(val < root.val) {
        root.left = insertIntoBST(root.left, val);
    }
    else {
        root.right = insertIntoBST(root.right, val);
    }

    return root;
}
```

### **Finding the Minimum**

The smallest value is always the leftmost node.

```js
function findMin(root) {
    while(root.left) {
        root = root.left;
    }

    return root;
}
```

### **Finding the Maximum**

The largest value is always the rightmost node.

```js
function findMax(root) {
    while(root.right) {
        root = root.right;
    }

    return root;
}
```

## **4. BST traversal**

One particularly interesting property of BSTs is that **inorder traversal produces values in ascending sorted order.**

Inorder traversal follows:

1. Visit left subtree.    
2. Visit current node.    
3. Visit right subtree.
    

Example:

```
        5
       / \
      3   8
     / \ / \
    1  4 7  9
```

Inorder result:

```
[1, 3, 4, 5, 7, 8, 9]
```

This is useful for problems involving sorted values, finding the kth smallest element and validating BSTs.

## **5. Time complexity**

The time complexity of BST operations depends on the tree's height.

|Operation|Average (balanced)|Worst case|
|---|---|---|
|Search|O(log n)|O(n)|
|Insert|O(log n)|O(n)|
|Find min/max|O(log n)|O(n)|
|Delete|O(log n)|O(n)|