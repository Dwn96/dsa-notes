**Pattern:** DFS / Recursion

## **Approach**

A binary tree is height-balanced if the left and right subtree heights of **every node** differ by no more than 1.

We can reuse the Maximum Depth approach with one modification.

1. Calculate the left subtree height.    
2. Calculate the right subtree height.    
3. Check whether their height difference exceeds 1.    
4. If unbalanced, return `-1`.    
5. Otherwise, return the height of the current subtree.
    

## **Solution**

```js
class Solution {
    isBalanced(root) {
        const dfs = (node) => {
            if (!node) return 0;

            const left = dfs(node.left);
            if (left === -1) return -1;

            const right = dfs(node.right);
            if (right === -1) return -1;

            if (Math.abs(left - right) > 1) return -1;

            return 1 + Math.max(left, right);
        };

        return dfs(root) !== -1;
    }
}
```