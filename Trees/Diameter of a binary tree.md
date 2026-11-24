## **Approach**

The diameter is the longest path between any two nodes, measured in **edges**, not nodes.

At each node:

1. Calculate the depth of its left subtree.    
2. Calculate the depth of its right subtree.    
3. Add both depths to get the diameter passing through the current node.    
4. Update the maximum diameter found so far.    
5. Return the maximum subtree depth to the parent.
    

## **Solution**

```js
class Solution {
    diameterOfBinaryTree(root) {
        let diameter = 0;

        const dfs = (node) => {
            if (!node) return 0;
            
            const leftDepth = dfs(node.left);
            const rightDepth = dfs(node.right);

            diameter = Math.max(diameter, leftDepth + rightDepth);

            return 1 + Math.max(leftDepth, rightDepth);
        };

        dfs(root);

        return diameter;
    }
}
```

## **Key concepts**

**1. Why add leftDepth + rightDepth?**

We want the longest path passing through the current node.

Example:

```
      2
     / \
    4   5
```

- Left depth = 1    
- Right depth = 1    
- Diameter = 1 + 1 = 2 edges    

Path: `4 → 2 → 5`

**2. Why return 1 + Math.max()?**

The parent needs the maximum depth of this subtree.

We only take the larger depth because a path extending through the parent can only use one branch.

```
return 1 + Math.max(leftDepth, rightDepth);
```