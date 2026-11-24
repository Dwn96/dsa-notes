**Pattern:** Recursion / DFS

## **Approach**

Compare both trees node by node.

1. If both nodes are `null`, they match.    
2. If only one is `null`, they don't match.    
3. If their values differ, they don't match.    
4. Recursively compare their corresponding left and right children.
    

## **Solution**

```js
class Solution {
    isSameTree(p, q) {
        if (!p && !q) return true;

        if (!p || !q || p.val !== q.val) return false;

        return this.isSameTree(p.left, q.left) &&
               this.isSameTree(p.right, q.right);
    }
}
```

## **Key concept**

Compare matching sides:
- `p.left` with `q.left`    
- `p.right` with `q.right`
    

**Don't cross the sides.**

```js
// Correct: Same Tree
this.isSameTree(p.left, q.left);
this.isSameTree(p.right, q.right);

// Wrong for this problem: Mirror comparison (Symmetric tree LC-101)
this.isSameTree(p.left, q.right);
this.isSameTree(p.right, q.left);
```

The second version checks whether the trees are mirror images, which is the idea behind **Symmetric Tree (101)**.

`&&` ensures both subtrees must match. If either comparison returns `false`, the entire result is `false`.

## **Complexity**

- **Time:** O(n), each node is visited once.    
- **Space:** O(h), recursion stack where `h` is the tree height. O(n) worst case for a skewed tree.