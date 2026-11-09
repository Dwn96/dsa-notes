## 1. Find the middle

Use slow and fast pointers. `slow` moves one step while `fast` moves two.

```js
let slow = head;
let fast = head;

while (fast.next && fast.next.next) {
    slow = slow.next;
    fast = fast.next.next;
}
```

## 2. Split the list

Save a reference to the second half then disconnect the two halves.

```js
let second = slow.next;
slow.next = null;
```

```
1 → 2 → 3 → null

4 → 5
```

`second` retains its reference to node 4 even after disconnecting the lists.

## 3. Reverse the second half

Use iterative linked-list reversal.

```js
let prev = null;
let current = second;

while (current) {
    let next = current.next;
    current.next = prev;
    prev = current;
    current = next;
}
```

`prev` becomes the head of the reversed list.

## 4. Merge alternately

Insert each node from the reversed second half between nodes in the first half.

```js
let first = head;
second = prev; //prev now points to the head of the 2nd half (after reversal)

while (second) {
    let firstNext = first.next;
    let secondNext = second.next;

    first.next = second;
    second.next = firstNext;

    first = firstNext;
    second = secondNext;
}
```

Why save `firstNext` and `secondNext`?

We're modifying `next` pointers. Saving the references prevents us from losing access to the remaining nodes.

Why `while (second)`?

The first half can have one extra node when the list has an odd length. That node is already in the correct position.

## Complexity

- Time: O(n)    
- Space: O(1)