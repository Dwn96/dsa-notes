This algo basically initializes two arrays that we'll use to keep track of occurences of chars of s1 and s2
```js
	const s1Count = new Array(26).fill(0)
	const windowCount = new Array(26).fill(0)
```

Then we'll check our initial substring of length s1 if it has an equal number of occurences of chars
```js
const aCharCode = 'a'.charCodeAt(0) // a - 97, b - 98, c-99 and so on
for(let i=0; i<s1.length;i++) {	
	s1Count[s1.charCodeAt(i) - aCharCode] ++
	windowCount[s2.charCodeAt(i) - aCharCode] ++
}
```

Then we'll deploy our helper function to check if both arrays are equal. If they are, we can immediately return true 
```js
if(this.arraysEqual(s1Count,windowCount)) return true

```

Then we can start sliding our window, since we've already checks the first s1.length chars our 2nd pass needs to start from index s1.length

```js

	for(let i = s1.length; i<s2.length; i++) {
		
		windowCount[s.charCodeAt(i) - aCharCode] ++
		/*
			since we've shrunk our window, we need to remove
			the count of s2.charAt(n - i) e.g our starting position
			is 3 (since s1 is of length 3) the character to be deleted
			is charAt(0)
		*/
		windowCount[s.charCodeAt(i-n) - aCharCode] --
		
		// Then we run our check after adjusting the window
		if(this.arraysEqual(s1Count, windowCount)) return true
		
	}
	
	return false

```

Full algo:
```js
	
	class Solution {

/**

* @param {string} s1

* @param {string} s2

* @return {boolean}

*/

	arraysEqual(arr1, arr2) {	
		for(let i = 0; i<26; i++) {		
			if(arr1[i] !== arr2[i]) return false	
		}		
		return true
	}

	checkInclusion(s1, s2) {
	
		if(s1.length > s2.length) return false
		
		const s1Count = new Array(26).fill(0)
		
		const windowCount = new Array(26).fill(0)
		
		const aCharCode = 'a'.charCodeAt(0)
		
		  
		
		for(let i = 0; i<s1.length; i++) {		
			s1Count[s1.charCodeAt(i) - aCharCode]++			
			windowCount[s2.charCodeAt(i) - aCharCode]++			
		}
		
		if(this.arraysEqual(s1Count, windowCount)) return true		
		  
		
		for(let i=s1.length; i<s2.length; i++) {		
			windowCount[s2.charCodeAt(i) - aCharCode]++		
			windowCount[s2.charCodeAt(i-s1.length) - aCharCode]--		
			if(this.arraysEqual(s1Count, windowCount)) return true
		
		}		  
		
			return false
		
		}

}

```