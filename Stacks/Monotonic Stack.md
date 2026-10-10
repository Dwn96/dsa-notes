A ***monotonic stack*** is a special type of stack data structure where elements are kept in either **increasing** or **decreasing** order.
### Monotonic Increasing Stack

- Elements inside the stack are always in increasing order.
- While inserting a new element, all greater elements are popped.
- ****Example:****

For arr[] = [1, 7, 9, 5]:

- Push 1 → [1]
- Push 7 → [1, 7] (since 7 > 1, order holds)
- Push 9 → [1, 7, 9] (since 9 > 7, order holds)
- Push 5 → pop 9, pop 7, then push 5 → [1, 5]

### Monotonic Decreasing Stack

- Elements inside the stack are always in decreasing order.
- While inserting a new element, all smaller elements are popped.

****Example:****

For arr[] = [1, 7, 9, 5]:

- Push 1 → [1]
- Push 7 → pop 1, then push 7 → [7]
- Push 9 → pop 7, then push 9 → [9]
- Push 5 → [9, 5] (since 5 < 9, order holds)