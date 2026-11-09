Solved using Floyd's cycle-finding algorithm which is commonly known as the tortoise and hare approach.

Instead of using extra memory to track visited nodes with a set we use two pointers that traverse the list at different speeds. 
A slow pointer moves one step at a time while a fast pointer moves two steps at a time. If a cycle exists the fast pointer will eventually loop around and catch up to the slow pointer. If there is no cycle the fast pointer will safely reach the end of the list and return false.

```js

var hasCycle = function(head) {
    let slow = head;
    let fast = head;

    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow === fast) {
            return true;
        }
    }

    return false;
};

```