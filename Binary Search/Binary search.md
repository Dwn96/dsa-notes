Looks pretty similar to [[Two Integer Sum II]] but instead of moving the left and right pointers  by 1 or - 1 consistently,  we move it by the array mid that we calculate.

Important difference:  We use `while(i <= j)`  because when `i` and `j` eventually point to the exact same index (`left === right`), **there is still one valid element left to check**.

If you use `i < j`, the loop will terminate before checking that final single-element window. This means if your target happens to be at that exact last index, the algorithm will skip it and incorrectly return that the element was not found.

```js
const binarySearch = (arr, target) => {
	let i = 0
	let j = arr.length - 1
	
	while(i <= j) {
		const mid = Math.floor((i + j) / 2)
		
		if(arr[mid] === target) return mid
		if(arr[mid] < target) {
			i = mid + 1
		} else {
			j = mid - 1
		}
	}
	
	return -1

}

```
