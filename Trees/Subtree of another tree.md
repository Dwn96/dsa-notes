**Pattern:** Recursion / DFS
### **Approach**

We need two recursive functions:
1. `isSameTree(p, q)` checks whether two trees are identical.    
2. `isSubtree(root, subRoot)` checks every node in the main tree as a potential starting point.
    

At each node in `root`:

- Check if the tree starting at this node matches `subRoot`.    
- If not, search the left subtree.    
- If still not found, search the right subtree.    

### **Solution**

```js
var isSubtree = function(root, subRoot) {
    if (!root) return false;

    if (isSameTree(root, subRoot)) return true;

    return isSubtree(root.left, subRoot) ||
           isSubtree(root.right, subRoot);
};

var isSameTree = function(p, q) {
    if (!p && !q) return true;

    if (!p || !q || p.val !== q.val) return false;

    return isSameTree(p.left, q.left) &&
           isSameTree(p.right, q.right);
};
```

### **Complexity**

Let `n` be the number of nodes in `root` and `m` the number in `subRoot`.

- **Time:** O(n × m) worst case. Each node in `root` may trigger a full comparison.    
- **Space:** O(h), where `h` is the height of `root` plus the recursion depth of the tree comparison. Worst case O(n + m).