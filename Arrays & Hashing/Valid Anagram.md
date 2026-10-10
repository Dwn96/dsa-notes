Here we  basically create a frequency map. We then do a first pass over the first string while storing occurences. 
Then a pass of the 2nd string while  checking the freq map. for every iteration we ask ourselves: 'This is already at 0, and we havent decremented it yet? - Not an anagram':
```js


var isAnagram = function(s, t) {
  

if(s.length !== t.length) return false  

const sCount = {}  

for(const char of s) {

if(!sCount[char]) sCount[char] = 0

sCount[char] += 1

}

  

for(const char of t) {

if(!sCount[char]) return false

sCount[char] --

}  

return true
  

};

```