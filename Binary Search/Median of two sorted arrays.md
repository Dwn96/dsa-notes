### 1. Array Preparation

- **Ensure Smaller Search Space:** Swap `nums1` and `nums2` if `nums1` is longer so binary search always runs on the smaller array.
    
- **Calculate Left Half Size:** 
	`const leftHalfSize = Math.floor((length1 + length2 + 1) / 2);` 
	Ensures the left partition gets the extra element when the total length is odd.
    

### 2. Binary Search Initialization

- **Pointers:** `low` starts at `0` and `high` starts at `length1`. We search for the optimal cut position in the smaller array.
- Remember that these are not indices, they represent partition boundaries from 0 (no elements chosen in nums1 to nums1.length being all the elements)
    

### 3. Calculating Cuts and Boundaries

- **Cut 1:** `const cut1 = Math.floor((low + high) / 2);` represents elements taken from the first array.
    
- **Cut 2:** `const cut2 = leftHalfSize - cut1;` represents the remaining elements needed from the second array to fill the left side.
    
- **Boundary Values:** Extract elements immediately beside each cut. Use `-Infinity` and `Infinity` when a cut lands at the start or end of an array.
    

### 4. Validation Logic

- **Check Condition:** If `left1 <= right2` and `left2 <= right1` the partition is valid. All left side elements are smaller than or equal to all right side elements.
    

### 5. Returning the Median

- **Odd Total Length:** Return `Math.max(left1, left2)` because the middle element lives at the rightmost boundary of the left partition.
    
- **Even Total Length:** Average the largest left value and smallest right value using `(Math.max(left1, left2) + Math.min(right1, right2)) / 2`.
    

### 6. Adjusting Search Pointers

- **Too Many Elements:** If `left1 > right2` we took too many elements from the first array so move `high` down to `cut1 - 1`.
    
- **Too Few Elements:** Otherwise we took too few elements so move `low` up to `cut1 + 1`.

```js

/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function(nums1, nums2) {

    // Always binary search the smaller array.
    // Swap the arrays if nums1 is longer.
    if (nums1.length > nums2.length) {
        [nums1, nums2] = [nums2, nums1];
    }

    const length1 = nums1.length;
    const length2 = nums2.length;

    // Number of elements required on the left side.
    // Adding 1 ensures the left side gets the extra element
    // when the total length is odd.
    const leftHalfSize = Math.floor((length1 + length2 + 1) / 2);

    /**
    Binary search for the cut position in nums1.
    Important!: These are not indices, they represent partition boundaries 
    **/
    let low = 0;
    let high = length1;

    while (low <= high) {

        // Number of elements taken from nums1 for the left half.
        const cut1 = Math.floor((low + high) / 2);

        // Calculate the cut in nums2 to get the required left half size.
        const cut2 = leftHalfSize - cut1;

        // Get the values immediately beside each cut.
        // Infinities handle cuts at the beginning or end of an array.
        const left1 = cut1 === 0 ? -Infinity : nums1[cut1 - 1];
        const right1 = cut1 === length1 ? Infinity : nums1[cut1];

        const left2 = cut2 === 0 ? -Infinity : nums2[cut2 - 1];
        const right2 = cut2 === length2 ? Infinity : nums2[cut2];

        // Check whether the partition is valid.
        if (left1 <= right2 && left2 <= right1) {

            // Odd total: the median is the largest value on the left.
            if ((length1 + length2) % 2 === 1) {
                return Math.max(left1, left2);
            }

            // Even total: average the largest left and smallest right values.
            const largestLeft = Math.max(left1, left2);
            const smallestRight = Math.min(right1, right2);

            return (largestLeft + smallestRight) / 2;
        }

        // Too many elements taken from nums1.
        if (left1 > right2) {
            high = cut1 - 1;
        } else {
            // Too few elements taken from nums1.
            low = cut1 + 1;
        }
    }
};

```

- **Time Complexity**: $O(\log(\min(m, n)))$ 
    
- **Space Complexity**: $O(1)$