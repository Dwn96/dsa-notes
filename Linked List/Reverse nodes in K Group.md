
## **Approach**

Reverse the linked list in groups of `k` nodes. Leave any remaining nodes untouched if fewer than `k` remain.

1. Use a dummy node to handle head changes.    
2. Find the node immediately after the current group (`groupNext`).    
3. If fewer than `k` nodes remain, stop.    
4. Reverse the group.    
5. Reconnect the reversed group to the rest of the list.    
6. Move to the next group.

## **Solution**

```js
var reverseKGroup = function(head, k) {
    // Dummy node simplifies reconnecting groups
    const dummy = new ListNode(0, head);
    let groupPrev = dummy;

    while (true) {
        // Find the kth node in the current group
        let kth = groupPrev;

        for (let i = 0; i < k && kth; i++) {
            kth = kth.next;
        }

        // Not enough nodes remaining
        if (!kth) break;

        // Save the node immediately after this group
        const groupNext = kth.next;

        // Reverse the current group
        let prev = groupNext;
        let curr = groupPrev.next;

		// reverse until right before groupNext
        while (curr !== groupNext) {
            const next = curr.next;

            curr.next = prev;
            prev = curr;
            curr = next;
        }

        // Reconnect the reversed group
        const oldGroupStart = groupPrev.next;

        groupPrev.next = kth;

        // Original first node is now the last node
        groupPrev = oldGroupStart;
    }

    return dummy.next;
};
```

## **1. Understanding the pointers**

We use five important pointers:

|Pointer|Purpose|
|---|---|
|`dummy`|Provides a node before the actual head|
|`groupPrev`|Node immediately before the current group|
|`kth`|Last node in the current group|
|`groupNext`|Node immediately after the current group|
|`prev` / `curr`|Used to reverse the group|

The most important relationship:

```
groupPrev → [Nodes to reverse] → groupNext
```

We reverse only the nodes between `groupPrev` and `groupNext`.

## **2. Why initialize** `prev = groupNext`**?**

This is the most important concept in this problem.

Consider:
```
1 → 2 → 3 → 4 → 5
```

We want to reverse the first two nodes:
```
2 → 1 → 3 → 4 → 5
```

Notice that node `1` needs to point to node `3` after reversal.

Instead of reversing the group with `prev = null` and reconnecting it afterwards, we initialize:

```
let prev = groupNext;
```

Since `groupNext` is node `3`, we effectively tell the reversal:

**When you reverse the first node, make it point to node 3.**

Initial state:

```js
prev = 3
curr = 1
```

The normal reversal operation:
```js
const next = curr.next;
curr.next = prev;
prev = curr;
curr = next;
```

Automatically connects the reversed group to the remaining list.

### **Why not** `prev = null`**?**

Normal linked list reversal:

```
let prev = null;
```

We use `null` because we're reversing the entire list. The original head becomes the tail and should point to `null`.

Partial linked list reversal:

```
let prev = groupNext;
```

We use `groupNext` because the original head of the group must point to the remaining list.

**Remember:**

- Entire list reversal: `prev = null`
    
- Partial list reversal: `prev = nodeAfterSection`
    

## **3. Understanding the reversal loop**

```
let prev = groupNext;
let curr = groupPrev.next;

while (curr !== groupNext) {
    const next = curr.next;

    curr.next = prev;
    prev = curr;
    curr = next;
}
```

Each iteration performs four operations:

1. Save the next node before changing any pointers.
    
2. Reverse the current node's pointer.
    
3. Move `prev` forward.
    
4. Move `curr` forward.
    

Example with `k = 2`:

Initial:

```
1 → 2 → 3 → 4 → 5

prev = 3
curr = 1
```

After iteration 1:

```
1 → 3 → 4 → 5
2 → 3 → 4 → 5

prev = 1
curr = 2
```

After iteration 2:

```
2 → 1 → 3 → 4 → 5

prev = 2
curr = 3
```

We stop because `curr === groupNext`.

## **4. Reconnecting the groups**

After reversing a group, we need to connect the previous group to the newly reversed group.

```js
const oldGroupStart = groupPrev.next;

groupPrev.next = kth;

groupPrev = oldGroupStart;
```

Why?

Before reversal:

```
groupPrev → 1 → 2 → 3
```

After reversal:

```
groupPrev → 2 → 1 → 3
```

The original first node (`1`) is now the last node.

Therefore:

- `groupPrev.next = kth` connects the previous group to the new first node.
    
- `groupPrev = oldGroupStart` moves our boundary to the end of the reversed group.    

This prepares us for the next group.

## **6. Complexity analysis**

| Complexity | Value    | Reason                                           |
| ---------- | -------- | ------------------------------------------------ |
| Time       | \(O(n)\) | Every node is visited a constant number of times |
| Space      | \(O(1)\) | Reversal happens in place using pointers         |