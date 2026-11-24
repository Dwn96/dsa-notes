## **Approach: BFS with Path Tracking**

### **Problem**

A node is considered _good_ if no ancestor along the path from the root to that node has a value greater than its own.

In other words, a node is good if:

$$
\text{node.val} \geq \text{maxSoFar}
$$

Where `maxSoFar` is the maximum value encountered from the root to the current node.

## **Key insight**

Comparing a node only with its immediate parent is insufficient.

A node's validity depends on **all its ancestors**, not just its parent.

For example:

```
       3
      / \
     1   4
    /
   3
```

The bottom `3` is good because no ancestor has a value greater than `3`.

Even though its immediate parent is `1`, we must also consider the root (`3`).

**Solution:** Carry the maximum value encountered along the path when traversing the tree.

## **JavaScript solution (BFS)**

```js
class Solution {
    goodNodes(root) {
        const queue = [[root, -Infinity]];
        let head = 0;
        let count = 0;

        while (queue.length > head) {
            const [node, maxSoFar] = queue[head++];

            if (node.val >= maxSoFar) {
                count++;
            }

            const newMax = Math.max(maxSoFar, node.val);

            if (node.left) {
                queue.push([node.left, newMax]);
            }

            if (node.right) {
                queue.push([node.right, newMax]);
            }
        }

        return count;
    }
}
```

## **How it works**

### **1. Queue stores additional information**

Instead of storing just the node:

```
queue.push(node.left);
```

We store the node and the maximum value encountered along its path:

```
queue.push([node.left, newMax]);
```

This allows each node to know the relevant information about its ancestors.

### **2. Extract the node and its path maximum**

```
const [node, maxSoFar] = queue[head++];
```

We use destructuring to retrieve both values.

### **3. Check whether the node is good**

```
if (node.val >= maxSoFar) {
    count++;
}
```

If the current node is greater than or equal to every ancestor, it's good.

### **4. Update the maximum**

```
const newMax = Math.max(maxSoFar, node.val);
```

The maximum for the children must account for the current node.

### **5. Enqueue children**

```
if (node.left) {
    queue.push([node.left, newMax]);
}

if (node.right) {
    queue.push([node.right, newMax]);
}
```

Both children inherit the updated maximum.

## **Complexity analysis**

Let `n` be the number of nodes and `w` the maximum width of the tree.

|Complexity|Value|Explanation|
|---|---|---|
|Time|O(n)|Every node is visited exactly once|
|Space|O(w)|Queue holds nodes across the current level|