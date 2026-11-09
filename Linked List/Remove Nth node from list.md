### Algorithm

1. Create a dummy node pointing to `head`. This handles edge cases where we need to remove the head.    
2. Initialise `fast` and `slow` at the dummy node.    
3. Move `fast` forward `n` steps to establish a gap.    
4. Move both pointers one step at a time until `fast.next === null`.    
5. `slow` is now immediately before the node to remove.    
6. Skip the target node using `slow.next = slow.next.next`.    
7. Return `dummy.next`.

```js
var removeNthFromEnd = function(head, n) {
    const dummy = new ListNode(0, head);

    let fast = dummy;
    let slow = dummy;

    // Create a gap of n nodes
    for (let i = 0; i < n; i++) {
        fast = fast.next;
    }

    // Move both pointers until fast reaches the last node
    while (fast.next !== null) {
        fast = fast.next;
        slow = slow.next;
    }

    // Remove the target node
    slow.next = slow.next.next;

    return dummy.next;
};

```

### Complexity

| Complexity | Cost | Reason                                       |
| ---------- | ---- | -------------------------------------------- |
| Time       | O(L) | Each pointer traverses at most the list once |
| Space      | O(1) | Only two pointers and a dummy node           |