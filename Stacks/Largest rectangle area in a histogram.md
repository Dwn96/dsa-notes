So what we're essentially doing is performing 2 passes and computing **Nearest Smallest Number to the left **  then  **Nearest Smallest Number to the right**

Initialize 2 arrays
```
const n = heights.length
const left = new Array(n)
const right = new Array(n)
```

Then perform the first pass. We want to pop pop continuosly until we arrive at an index that maps to a value that's SMALLER than our current point in the loop.
If the stack is empty at the point we exit our while loop we can safely assume that we're at index 0 and the next nearest smallest number is -1 because our outer boundaries are between -1 and n. 

A normal array is between 0 and n-1
```js
for(let i = 0; i < n; i++) {
	
	if(stack.length && heights[stack[stack.length - 1] >=  heights[i]]) {		
		pop()
	}
	
	if(stack.length) {
		left[i] = stack[stack.length - 1]
	} 
	else {
	
		left[i] = -1
	}
	
	stack.push(i)
	
}

stack.length= 0
```

Then we do our right pass. Notice how we set the right[i] value to n if the stack  is empty 
```js
for(let i = n-1; i > -1; i--) {
	
	if(stack.length && heights[stack[stack.length - 1] >=  heights[i]]) {		
		pop()
	}
	
	if(stack.length) {
		right [i] = stack[stack.length - 1]
	} 
	else {
	
		right[i] = n
	}
	
	stack.push(i)


}


```

Then we compute our areas
```js
let maxArea = 0
for(let i = 0; i < n; i++) {

	const width = right - left - 1
	const currentArea = width * heights[i]
	
	maxArea = Math.max(currentArea, maxArea)

}

return maxArea

```

Note that width is right-left-1 because whenever you want to count integers strictly between two numbers $L$ and $R$ where neither $L$ nor $R$ is included, the count is always:

$$\text{count} = R - L - 1$$

### Quick Examples to See Why

1. **Inside the array:**
    
    - Suppose blockers are at index $2$ and index $6$.
        
    - The valid indices in between are $3, 4$ and $5$.
        
    - That is $3$ items.
        
    - Formula: $6 - 2 - 1 = 3$.
