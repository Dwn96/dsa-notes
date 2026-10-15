This is a pretty straightforward binary search question. 
We initialise two variables left = 1 and right = Math.max(...piles) which represent the minimum and the maximum "speeds" Koko can eat bananas.
Then we find the mid of these. 

```js
minEatingSpeed(piles, h) {
	let left = 1
	let right = Math.max(...piles)
	
	while(left < right) {
	
		let mid = Math.floor((left+right)/2)
		
		// lets see how long it will take to eat at speed mid
		
		let hrs = 0
		
		for(const pile of piles) {
			hrs += Math.ceil(pile / mid)
		}
		
		if(hrs <= h) {
			right = mid
		}
		else {
			/*
				if the hrs it takes to eat at speed mid is greater
				than h, lets increase speed slightly
			
			*/
			left = mid + 1 
		}
	
	}
	
	return left
	
}

```