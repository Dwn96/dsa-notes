```js
class Solution {
    /**
     * @param {ListNode} head
     * @return {ListNode}
     */
    reverseList(head) {
        let prev = null
        let current = head

        while (current !== null) {
            // Save the next node before reversing the link
            const next = current.next

            // Reverse the current node's link
            current.next = prev

            // Move prev and current one step forward
            prev = current
            current = next
        }

        // prev now points to the new head
        return prev
    }
}

```