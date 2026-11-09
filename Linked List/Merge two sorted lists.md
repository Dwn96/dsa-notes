```js
/**
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function(list1, list2) {
    // Starting node to simplify building the merged list.
    const dummy = new ListNode(-1)

    // Points to the last node in our merged list.
    let current = dummy

    // Compare nodes until one list runs out.
    while (list1 !== null && list2 !== null) {
        if (list1.val <= list2.val) {
            // Attach list1's node to the merged list.
            current.next = list1

            // Advance list1 to its next node.
            list1 = list1.next
        } else {
            // Attach list2's node to the merged list.
            current.next = list2

            // Advance list2 to its next node.
            list2 = list2.next
        }

        // Advance the end of the merged list.
        current = current.next
    }

    // Attach whichever list still has nodes.
    current.next = list1 !== null ? list1 : list2

    // The first real node is after the dummy node.
    return dummy.next
};

```