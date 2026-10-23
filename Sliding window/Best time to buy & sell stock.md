Uses 2 pointers - l which is the buy day and r the sell day

```js

var maxProfit = function(prices) {
	let l = 0  // buy day
	let r = 1	// sell day
	let maxProfit = 0
	while(r<prices.length) {
		/*
		are prices on the sell day greater than prices on the sell day?
		*/
		if(prices[r] > prices[l]) {
			let curr = prices[r] - prices[l]
			maxProfit = Math.max(curr, maxProfit)
		}
		else {
			/*
			prices on sell day are actually lower than buy day
			so we've found a new buy day
			*/
			l = r
		
		}
		
		r++
	
	}
	
	return maxProfit

}

```