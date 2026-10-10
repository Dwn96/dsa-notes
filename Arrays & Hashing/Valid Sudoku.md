
Essentially use string literals to check for duplicates
Good vid: https://www.youtube.com/watch?v=sQK8ASBWIYI

Calc boxNumber using : 

``const boxNumber = 3 * Math.floor(i/3) + Math.floor(j/3)``

```js
-- essentially do a nested loop, but it is fine since this is only 9x9 elements

const seen = new Set()
for(let i = 0; i < 9; i++) {
	
	for(let j = 0; j<9; j++) {
	
	const val = board [i][j]
	
	if(val === '.') contine // remember to skip empty cells!
	
	// build string literals
	
	const row= `row${i}val${val}`
	const col = `col{j}val${val}`
	
	// alg for calculating current box
	const boxNumber = 3 * Math.floor(i/3) + Math.floor(j/3) 
	
	const box = `${boxNumber}val${val}`
	
	if(seen.has(row) || seen.has(col) || seen.has(box)) {
		return false
	}
	 seen.add(row).add(col).add(box)
	
	}

}
return true

```
