So the trick here is that we ALWAYS want to use the maximum height.
We declare to pointers i and j


```js

function maxArea(heights) {

	let i = 0
	let j = heights.length - 1
	let area = 0
	
	while(i < j) {
	
		/*
			We always choose the smaller height
			because if you think about it, choosing a longer
			one will cause an overflow of the water.
			Like if i = 2 and j = 3, we'd def use 2
			to calc our container height
			|
			|  |
			|  |
		
		
		*/
		let height = Math.min(heights[i], heights[j]) 
		let width = j - i
		
		area = Math.max(area, height * width)
		
		/*
			Here's the clever part we add so this algo doesnt
			end up being O(n2) by going thru every element
			We essentially want to be greedy with how we move our pointers		
		
		*/
		
		if(heights[i] < heights[j]) {
			i++
		} else {
			j--
		}
		
	
	}
	
	return area

}


```