
<h2>Longest consecutive sequence</h2>
Use a hashset(set) - Look ups are constant O(1). Duplicates are deleted!

`const nums = [1,2,3,4,5]`
`const set = new Set(nums)`

Code
```js
longestConsecutive(nums) {
  

const set = new Set(nums) // creating a set from array is O(n)

let max = 0  


/*
Remember to iterate over the set or else
we'll be doing uneccessary duplicate iterations!!!!!
*/
for (const num of set) { 

if(set.has(num - 1))  
/*
if we have a number n - 1 that exists in the set we're sure we not at
the start of the sequence so continue until we're at one of the potential starts

*/

continue
}

  

let curr = num

let currMax = 1

  

while(set.has(curr + 1)) {
/*
if we're found a potential sequence start k, lets see if k+1 exists 
in the set, then increment until we've found all of them

*/

currMax ++

curr ++

}

  
// Here we're essentially constanstly comparing the currMax and the max so we find the biggest one
max = Math.max(max, currMax)

}

  

return max

}



```