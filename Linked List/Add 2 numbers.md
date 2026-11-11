```js
var addTwoNumbers = function(l1, l2) {
    let carry = 0

    // Dummy node to simplify building the result linked list
    const dummy = new ListNode(0)
    let current = dummy

    // Continue while either list has nodes or there's a remaining carry
    while(l1 || l2 || carry) {
        let sum = carry

        // Add the current digit from the first list
        if(l1) {
            sum += l1.val
            l1 = l1.next
        }

        // Add the current digit from the second list
        if(l2) {
            sum += l2.val
            l2 = l2.next
        }

        // Calculate the carry for the next position
        carry = Math.floor(sum / 10)

        // Get the digit to store in the current result node
        const digit = sum % 10

        // Append the new digit to the result list
        current.next = new ListNode(digit)
        current = current.next
    }

    // Return the actual head, skipping the dummy node
    return dummy.next
};

```