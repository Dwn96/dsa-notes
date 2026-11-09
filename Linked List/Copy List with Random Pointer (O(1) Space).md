### Pass 1: Create and interweave copies

```js
let current = head;

while (current) {
    const copy = new Node(current.val);

    copy.next = current.next;
    current.next = copy;

    current = copy.next;
}
```

Original:

```
A → B → C → null
```

After interweaving:

```
A → A' → B → B' → C → C'
```

Key observation:

- `original.next` = its copy
    
- `copy.next` = next original node
    

### Pass 2: Assign random pointers

```js
current = head;

while (current) {
    if (current.random) {
        current.next.random = current.random.next;
    }

    current = current.next.next;
}
```

Why `current.random.next`?

Suppose `A.random = C`.

Since every original node is followed by its copy:

```
C → C'
```

Therefore:

```
A'.random = C';
```

We use `.next` to get the copied version of the random target.

Why `current.next.next`?

We only want to traverse original nodes, skipping their copies.

### Pass 3: Separate the two lists

```js
current = head;
const copyHead = head.next;

while (current) {
    const copy = current.next;

    // Restore original list
    current.next = copy.next;

    // Connect copied list
    copy.next = copy.next ? copy.next.next : null;

    // Move to next original node
    current = current.next;
}

return copyHead;
```

Before separation:

```
A → A' → B → B' → C → C'
```

After separation:

```
Original: A → B → C → null

Copy:     A' → B' → C' → null
```