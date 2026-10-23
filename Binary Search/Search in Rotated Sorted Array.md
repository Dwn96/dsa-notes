Standard binary search.
We check a coupe of things
-  If `nums[left] <== nums[mid]` we can safely assume that the left potion of our array
	sorted then we can do binary search on the left for our target
- Else we know that the right potion of our array is sorted and we reduce our search space to that half
```js
search(nums, target) {

        let left = 0
        let right = nums.length - 1


        while(left <= right) {

            let mid = Math.floor((left+right)/2)

            if(nums[mid] === target) return mid

			/*
			 If this is true, it implies the left half
			 is sorted
			*/
            if(nums[left] <= nums[mid]) {
                if(target >= nums[left] && target < nums[mid]) {
                /*
                If the target is between left and just before mid
                lets move our right pointer to the index right before mid
                
                */
                    right = mid - 1
                }else {
                /*
                 Else we know our target is in the 2nd half - right after mid
                */
                    left = mid + 1
                }
            } 

            else {
	            /*
	            If the 1st condition failed, it implies that the right half
	            is the sorted one.
	            
	            So we check if our target is between right and just after mid
	            
	            */

                if(target <= nums[right] && target > nums[mid]) {
                    left = mid + 1
                } else {
                    right = mid - 1
                }
            }
        }

        return -1
    }

```