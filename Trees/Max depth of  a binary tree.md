**Approach:**

- Base case: If node is `null`, return `0`.    
- Recursively calculate left subtree depth.    
- Recursively calculate right subtree depth.    
- Return the larger depth + 1 for the current node.
    

```js
var maxDepth = function(root) {
    if (!root) return 0;

    const leftDepth = maxDepth(root.left);
    const rightDepth = maxDepth(root.right);

    return 1 + Math.max(leftDepth, rightDepth);
};
```

**Key takeaway:** Maximum depth = `1 + max(leftDepth, rightDepth)`.

**Complexity:**

- Time: \(O(n)\)    
- Space: \(O(h)\) - The recursion stack grows with the tree height.