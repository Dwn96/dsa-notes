Standard binary search. 
Here want to constanstly update our search space by checking the median then
comparing it against the **right**.

- **`nums[mid] > nums[right]`**: This tells us that the inflection point (where the drop occurs) is to the right of `mid`, so we can safely move `left` to `mid + 1`.
		e.g [3,4,5,6,1,2]
    
- **`nums[mid] <= nums[right]`**: This tells us that the right half is sorted normally, meaning the minimum must be at `mid` or somewhere to the left, so we move `right` to `mid`. e.g [0,1,2,3,4,5,6]

```js
const minFind = (arr) => {	
	const left = 0
	const right = arr.length -1
	
	while(left < right) {
	
		const mid = Math.floor((left + right)/2)
		
		if(nums[mid] > right) {
			left = mid + 1 		
		} 
		else {
			right = mid
		}
	
	}
	
	return nums[left]
}

```