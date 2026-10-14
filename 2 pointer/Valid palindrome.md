This one is pretty straight forward. 
We essentially use some regex to sanitize the string and remove any non-alphanumeric bits
```js
s = s.toLowerCase().replace(/[^a-z0-9]/g, '')
```
Then we initialize 2 pointers left and right to traverse the string
```js
let left = 0

let right = s.length -1

  

while(left < right) {

if(s.charAt(left) !== s.charAt(right)) return false

	left ++
	
	right --

}

  

return true
```

**Regex breakdown**
```regex
/[^a-z0-9]/g
```
- `/ ... /` : Delimiters that tell JavaScript "this is a regular expression pattern".
    
- `[...]` : A character set. It means "match any single character inside these brackets".
    
- `^` : Inside brackets, this flips the logic to **NOT**. Instead of matching these characters, match everything _except_ them.
    
- `a-z` : Any lowercase letter from a through z.
    
- `0-9` : Any digit from 0 through 9.
    
- `g` : The "global" flag. Without this, `.replace()` stops after replacing the very first match it finds.