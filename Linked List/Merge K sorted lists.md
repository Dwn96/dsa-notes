**LeetCode:** Hard  
**Pattern:** Divide and Conquer  
**Related:** Merge Two Sorted Lists, Merge Sort

## Problem

Given an array of `k` sorted linked lists, merge them into one sorted linked list.

Example:

```text
Input:
[
  1 -> 4 -> 5,
  1 -> 3 -> 4,
  2 -> 6,
  0 -> 7
]

Output:
0 -> 1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6 -> 7
```

## Approach: Divide and Conquer

Instead of merging every list sequentially, merge them in pairs.

The idea is similar to Merge Sort. Each round combines smaller groups into progressively larger sorted lists.

### Example

Initial lists:

```text
L0: 1 -> 4 -> 5
L1: 1 -> 3 -> 4
L2: 2 -> 6
L3: 0 -> 7
```

**Round 1: interval = 1**

Merge adjacent lists:

```text
merge(L0, L1):
1 -> 1 -> 3 -> 4 -> 4 -> 5

merge(L2, L3):
0 -> 2 -> 6 -> 7
```

**Round 2: interval = 2**

Merge the two previously merged lists:

```text
merge(L0, L2):

0 -> 1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6 -> 7
```

We now have one sorted linked list.

## Implementation

```javascript
var mergeKLists = function(lists) {
    if (lists.length === 0) return null;

    // Merge two sorted linked lists
    const mergeTwoLists = (l1, l2) => {
        const dummy = new ListNode(0);
        let current = dummy;

        while (l1 && l2) {
            if (l1.val <= l2.val) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }

            current = current.next;
        }

        // Attach whichever list still has remaining nodes
        current.next = l1 || l2;

        return dummy.next;
    };

    let interval = 1;

    while (interval < lists.length) {
        for (let i = 0; i + interval < lists.length; i += interval * 2) {
            lists[i] = mergeTwoLists(lists[i], lists[i + interval]);
        }

        interval *= 2;
    }

    return lists[0];
};
```

## Understanding the Interval

The `interval` determines how far apart the lists being merged are.

It doubles after every round because we're merging progressively larger groups.

For 8 lists:

| Round | Interval | Pairs merged |
|---|---:|---|
| 1 | 1 | (0,1), (2,3), (4,5), (6,7) |
| 2 | 2 | (0,2), (4,6) |
| 3 | 4 | (0,4) |

### Why does i start at 0 again?

The `for` loop is inside the `while` loop.

Every time the outer `while` loop starts another iteration, the inner `for` loop is initialized again.

```javascript
for (let i = 0; ...)
```

Since `i` is declared inside the `for` loop, it gets reset to 0 every round.

Meanwhile, `interval` persists because it is declared outside both loops.

### Understanding the loop increment

```javascript
i += interval * 2
```

We skip two groups because each iteration merges the current group with the next group.

For example, when `interval = 1`:

- Merge index 0 with index 1.
- Move to index 2.
- Merge index 2 with index 3.

When `interval = 2`:

- Merge index 0 with index 2.
- Move to index 4.

## Complexity Analysis

Let:
- `N` = total number of nodes across all lists.
- `K` = number of linked lists.

**Time Complexity: O(N log K)**

- Each merging round processes all N nodes.
- Each round approximately halves the number of independent lists.
- There are O(log K) rounds.

Therefore:

```text
O(N) * O(log K) = O(N log K)
```

**Auxiliary Space: O(1)**

- Iterative implementation.
- Reuses existing linked list nodes.
- Only uses a temporary dummy node during each merge.
- No recursive call stack.
