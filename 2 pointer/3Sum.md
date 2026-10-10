
Here we basically initialise 3 pointers: i,j,k
i  = fixed pointer. increments once for every loop
j  = i + 1 (goes forwards)
k = nums.length - 1 (this one basically goes backward)

Hardest part here is basically duplicate avoidance, but straightforward question overall

We want to start by [[JS Array.sort function]] in place in incrementing order. 
`nums = nums.sort((a,b) => a - b)`

Notice how our i runs from i to nums.length -2 coz need room for at least two elements after nums[i]
A valid triplet requires **three distinct indices**: `i`, `j`, and `k`, where:

$$i < j < k$$

```js
threeSum(nums) {

if(!nums.length) return []

  

let res = []
 
nums = nums.sort((a,b) => a-b)  // start by sorting

/*
notice how our I runs from i to nums.length -2 coz need room for at least two elements after nums[i]
A valid triplet requires **three distinct indices**: `i`, `j`, and `k`, where:

$$i < j < k$$

*/

for(let i = 0; i < nums.length -2; i++) {

let j = i + 1

let k = nums.length - 1

/* 
 dedeuplication logic, no need to go over the same value we did
on the prev iteration, just continue 
*/

if(i > 0 && nums[i] === nums[i - 1]) continue

  

while(j < k) {

const sum = nums[i] + nums[j] + nums[k]

  

if(sum === 0 ) {

res.push([nums[i], nums[j], nums[k]])

  

while(nums[j] === nums[j+1]) j++  // more dedupes

while(nums[k] === nums[k-1]) k-- // more dedupes

  

j++

k--

}

/*
if sum < 0 it means we've undershot our target  so lets increment
our j to a bigger value and re-evaluate

*/

else if ( sum < 0) {

j++  

} else { // overshot, lets  move to a smaller value

k--

}

  

}

}

  

return res

}
```