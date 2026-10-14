This one pretty much uses bucket sort.
We first start by iterating over the array and creating a frequency map.
Then we iterate over the freq map using `Object.entries(freqMap)` while
writing to the bucket where i is the freq and each i has a set of all the elements that have that frequency.

#### Important
When you use `Object.entries(freqMap)`, JavaScript converts object keys into strings. This means your bucket sets store string values and your final result returns strings instead of numbers.  We fix this by wrapping the key in `Number()`.


```js

/**

* @param {number[]} nums

* @param {number} k

* @return {number[]}

*/

var topKFrequent = function (nums, k) {

  

const bucket = []

const freqMap = {}

  

for (const num of nums) {

if (!freqMap[num]) freqMap[num] = 0

freqMap[num]++

}

  

for (const [num, freq] of Object.entries(freqMap)) {

  

if (!bucket[freq]) {

bucket[freq] = new Set()

}

  

bucket[freq].add(Number(num)) // cast to number because object keys are strings!

  

}

  

let res = []

  

for (let i = bucket.length - 1; i > -1; i--) {

if (bucket[i]) {

res.push(...bucket[i])

}

if (res.length === k) break

  

}

  

return res

  

};

```

Time Complexity: O(n)
Space complexity: O(n)