**Pattern:** DFS / Recursion

**Approach:**

- Base case: If node is `null`, return `null`.    
- Swap the current node's left and right children.    
- Recursively invert both subtrees.    
- Return the original root.
    

```js
var invertTree = function(root) {
    if (!root) return null;

    [root.left, root.right] = [root.right, root.left];

    invertTree(root.left);
    invertTree(root.right);

    return root;
};
```

**Key takeaway:** Invert every node by swapping its children. Modify the existing tree rather than creating a new one.

**Complexity:**

- Time: \(O(n)\)    
- Space: \(O(h)\) recursion stack.