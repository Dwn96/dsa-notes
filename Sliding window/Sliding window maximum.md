So this question isnt really as hard as you think, similar to how we used [[Monotonic Stack]], we use a double ended queue (deque) to solve this.

The deque stores indices of elements in decreasing order of their values (largest value at the top(index 0).

Instead of physically removing elements from the front, which would require an expensive `shift()` operation, we maintain a `head` pointer to track the front of the deque. When an index expires, we simply advance `head`. To remove elements from the back, we use `pop()`.

```js
class Solution {
    /**
     * @param {number[]} nums
     * @param {number} k
     * @return {number[]}
     */
    maxSlidingWindow(nums, k) {
        // Stores indices in decreasing order of their values
        const dq = []
        const res = []

        // Tracks the front of the deque without using shift()
        let head = 0

        for (let i = 0; i < nums.length; i++) {

            // Remove the front index if it has expired
            // i - k is the last index outside the current window
            // e.g at index 3 and k 3, k - 3 = 0 i.e index 0 has expired
            if (dq.length > head && dq[head] <= i - k) {
                head++
            }

            // Remove smaller or equal values from the back
            // They can never be the maximum while the current
            // element remains in the window
            while (
                dq.length > head &&
                nums[dq[dq.length - 1]] <= nums[i]
            ) {
                dq.pop()
            }

            // Add the current index to the back of the deque
            dq.push(i)

            // Start recording maximums once the first window
            // of size k is complete
            if (i >= k - 1) {
                // The front index points to the maximum element
                res.push(nums[dq[head]])
            }
        }

        return res
    }
}

```