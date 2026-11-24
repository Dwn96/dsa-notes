Builds up on [[Binary Search Tree]]

```js
var lowestCommonAncestor = function(root, p, q) {
    let curr = root;

    while(curr) {
        if(p.val < curr.val && q.val < curr.val) {
            curr = curr.left;
        }
        else if(p.val > curr.val && q.val > curr.val) {
            curr = curr.right;
        }
        else {
            return curr;
        }
    }
};

```

##  **Complexity**

- **Time:** O(h), where h is the height of the tree.
    
- **Space:** O(1), because we're using an iterative approach without recursion.    

For a balanced BST, time is O(log n). For a skewed BST, it can be O(n).
