
## Problem

Given a binary tree, return its level order traversal as a nested array.

Each inner array contains the values of nodes at the same depth, ordered from left to right.

Example:

```text
        3
       / \
      9   20
         /  \
        15   7
```

Output:

```javascript
[[3], [9, 20], [15, 7]]
```

## Approach: Breadth-First Search (BFS)

BFS explores a tree level by level rather than going as deep as possible.

We use a **FIFO queue** (First In, First Out) to keep track of nodes waiting to be processed.

### Algorithm

1. Initialize a queue with the root node.
2. While the queue isn't empty:
   - Capture the number of nodes currently in the queue (`levelSize`).
   - Create an array for the current level.
   - Process exactly `levelSize` nodes.
   - Add each node's value to the current level.
   - Add its left and right children to the queue if they exist.
   - Add the completed level to the result.
3. Return the result.

## JavaScript Solution

```javascript
var levelOrder = function(root) {
    if (!root) return [];

    const result = [];
    const queue = [root];
    let head = 0;

    while (head < queue.length) {
        // Number of unprocessed nodes at the current level
        const levelSize = queue.length - head;
        const currentLevel = [];

        for (let i = 0; i < levelSize; i++) {
            const node = queue[head];

            currentLevel.push(node.val);

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);

            // Move to the next node
            head++;
        }

        result.push(currentLevel);
    }

    return result;
};
```


## Complexity Analysis

Let `n` be the total number of nodes in the tree.

| Operation | Complexity |
|---|---|
| Visit each node | O(n) |
| Enqueue each node | O(1) amortized |
| Dequeue using head pointer | O(1) |
| Total time | O(n) |
| Auxiliary space | O(n) |




