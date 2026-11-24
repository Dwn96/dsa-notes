## **Problem**

Given the root of a binary tree, return the values of the nodes visible when looking at the tree from the right side, ordered from top to bottom.

The key idea is to capture the **last node at each level**.

## **Approach: BFS (Level-Order Traversal)**

Use BFS to traverse the tree level by level.

Since we process nodes from left to right, the last node processed at each level is the rightmost visible node.
```js
var rightSideView = function(root) {
    if (!root) return [];

    const result = [];
    const queue = [root];

    let head = 0;

    while (head < queue.length) {
        const levelSize = queue.length - head;

        for (let i = 0; i < levelSize; i++) {
            const node = queue[head++];

            // Capture the last node at this level
            if (i === levelSize - 1) {
                result.push(node.val);
            }

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
    }

    return result;
};

```