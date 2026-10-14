We need to think of the 2D array as being "flat" and the rest is just standard binary search
IMO the only tricky bit is calculating the col and row given the mid

### Mental Model
Treat the 2D matrix as a flattened 1D array grouped into chunks of `cols`.
### Formulas

- **Row:** `Math.floor(mid / cols)` (Finds which chunk/row the index belongs to)    
- **Column:** `mid % cols` (Finds the exact offset inside that row)


Whole thing:

```js
searchMatrix(matrix, target) {

	let cols = matrix[0].length	
	let rows = matrix.length	
	let left = 0	
	let right = (rows * cols) - 1
	
	  
	
	while(left <= right) {	  
	
		let mid = Math.floor((left + right) / 2)		
		let row = Math.floor(mid / cols)		
		let col = Math.floor(mid % cols)
		
		  
		
		const found = matrix[row][col]		
		  
		
		if(found === target) {		
			return true		
		}
		
		if(found < target) {		
			left = mid + 1		
		}
		
		else {		
			right = mid - 1		
		} 
	
	}
	  
	
	return false  

}

```