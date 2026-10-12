Here, we really want to calculate the  left and right for any point of our height array.
We want to be continuously updating the maxLeft and the maxRight at every point.
We're essentially doing this:
```js
let maxLeft = 0

maxLeft = Math.max(maxLeft, height[i])
```

Then with the maxLeft / maxRight we can calculate how much water can be stored at any point with:
```js
let cap = maxLeft - height

```

Full algo:
```js

const trap = (heights) => {

	let i = 0
	let j = heights.length - 1
	let maxLeft = 0
	let maxRight = 0
	let sum = 0
	
	while( i < j) {
		
		/*
			We always take the smaller height because it determines
			the maximum water level, taking the big one will cause an overflow
		*/
		if(heights[i] < heights[j]) { 
			/*
				We want to keep track of the max height
				we've encountered thus far			
			*/
			
			if(heights[i] > maxLeft) { 
				maxLeft = heights[i]
			} else {
				sum += (maxLeft - height[i])
			}
			
			i++
		} 
		else {
			
			if(heights[j] > maxRight) {
				maxRight = heights[j]
			}
			else {
				sum += (maxRight - height[j])
			}
			
			j--
			
		}
	
	}
	
	return sum

}


```

Space - O(1)
Time - O(n)

Reference video: https://www.youtube.com/watch?v=KFdHpOlz8hs