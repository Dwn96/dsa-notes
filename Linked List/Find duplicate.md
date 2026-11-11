### Approach 1 : Negative marking 
Space - O(1)
Time - O(n)
Okay approach but it modifies original array

```js
var findDuplicate = function(nums) {
    for (let i = 0; i < nums.length; i++) {
        // Get the original value since we may have negated it
        const index = Math.abs(nums[i]);

        // If the value at this index is already negative,
        // we've visited this index before.
        // The current number is our duplicate.
        if (nums[index] < 0) {
            return index;
        }

        // Mark this index as visited by negating its value
        nums[index] *= -1;
    }
};

```

### Approach 2: Floyd's Cycle Detection (Most optimal)
Space - O(1)
Time - O(n)
### Steps

Phase 1: Find the intersection

1. Initialize slow and fast at `nums[0]`.    
2. Move slow one step and fast two steps.    
3. Repeat until they meet inside the cycle.
    

Phase 2: Find the cycle entrance

1. Reset slow to `nums[0]`.    
2. Keep fast at the intersection.    
3. Move both pointers one step at a time.    
4. They meet at the cycle entrance, which is the duplicate.

```js
var findDuplicate = function(nums) {
    // Phase 1: Find intersection inside the cycle
    let slow = nums[0];
    let fast = nums[0];

    do {
        slow = nums[slow];           // Move 1 step
        fast = nums[nums[fast]];     // Move 2 steps
    } while (slow !== fast);

    // Phase 2: Find cycle entrance
    slow = nums[0];

    while (slow !== fast) {
        slow = nums[slow];  // Move 1 step
        fast = nums[fast];  // Move 1 step
    }

    return slow;
};

```