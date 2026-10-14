There exists an approach that uses str.charCodeAt(i) but I don't like it


```js
var groupAnagrams = function(strs) {

  

const map = {}

  

for(const str of strs) {

  

const sortedKey = str.split('').sort().join()

  

if(!map[sortedKey]) map[sortedKey] = []

  

map[sortedKey].push(str)

}

  

return Object.values(map)

};
```


Time Complexity: N K Log(K)  - Because of the sorting
Space:  $O(N \cdot K)$

- The hash map stores all original strings and computed keys.