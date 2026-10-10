Pretty cool. 
So the whole algo is pretty much calculating the compliment of each of our num in our nums array
```js
var twoSum = function(nums, target) {

  

const seen = {}

  

for(let i = 0; i< nums.length; i++) {  

const compliment = target - nums[i]  

if(seen[compliment] !== undefined) {

	return [ i , seen[compliment]]

}

  

seen[nums[i]] = i // this needs to happen at the end to prevent overwrites!!

  

}

};

```