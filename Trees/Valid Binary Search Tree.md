## Core Insight

A BST must satisfy a **global ordering constraint**, not just immediate parent-child comparisons.

- Every node in the left subtree must be smaller than the current node.
- Every node in the right subtree must be greater than the current node.
- Duplicate values are not allowed.

Checking only immediate children is insufficient because a node can satisfy its parent's constraint while violating an ancestor's constraint.

## Range Validation

Track the minimum and maximum values each node is allowed to have.

Every node must satisfy:

$$
min < node.val < max
$$

If either boundary is violated, the tree is invalid.

```javascript
if (node.val <= min || node.val >= max) {
    return false
}
````

Initialize the root with unrestricted boundaries:

$$  
-\infty < root.val < +\infty  
$$

## **Boundary Propagation**

Each node inherits the constraints imposed by its ancestors.

**Moving LEFT:**

- Preserve the existing minimum.    
- Update the maximum to the current node's value.    

```
min: min,
max: node.val
```

**Moving RIGHT:**

- Update the minimum to the current node's value.    
- Preserve the existing maximum.
    

```
min: node.val,
max: max
```

The reasoning:

- Moving left introduces a new upper boundary.    
- Moving right introduces a new lower boundary.    
- Existing boundaries must be preserved because ancestor constraints still apply.
    

### **Example**

```
          10
         /  \
        5    15
       / \
      3   7
```

|Node|Min|Max|
|---|---|---|
|10|-∞|+∞|
|5|-∞|10|
|15|10|+∞|
|3|-∞|5|
|7|5|10|

Node `7` must be greater than `5` and smaller than `10`, even though its immediate parent is only `5`.

## **BFS Solution**

```js
class Solution {
    isValidBST(root) {
        if (!root) return true

        const queue = [{
            node: root,
            min: -Infinity,
            max: Infinity
        }]

        let head = 0

        while (head < queue.length) {
            const { node, min, max } = queue[head++]

            if (node.val <= min || node.val >= max) {
                return false
            }

            if (node.left) {
                queue.push({
                    node: node.left,
                    min,
                    max: node.val
                })
            }

            if (node.right) {
                queue.push({
                    node: node.right,
                    min: node.val,
                    max
                })
            }
        }

        return true
    }
}
```

## **Complexity Analysis**

Let `n` be the number of nodes.

|Complexity|Cost|
|---|---|
|Time|O(n)|
|Space|O(n) worst case|

Each node is visited exactly once.