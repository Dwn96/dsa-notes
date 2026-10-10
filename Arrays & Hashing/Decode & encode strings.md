Here, we essentially want to encoded strings in the form `{length}#{string}` e.g
[['Hello', 'world'] ] will be encoded to `5#Hello3#World`

## Encoding
```js

const encode = (strs) => {
	
	let encoded = ''
	
	for(const str of strs) {
		
		encoded += `${str.length}#${str}`
		
	}
	
	return encoded

}

```

## Decoding
Decoding involves moving our pointer in a clever way. 
We first find the hash postion. Using the hashposition we can conclude that  the word length is between i and hashpos.

```js
const decode = (str) => {
	
	let res = []
	let i = 0
	
	while(i , str.length) {
		let hashPos = str.indexOf('#', i)
		
		let len = Number(str.slice(i, hashPos))
		
		i = hashPos + 1 // move pointer to start of the word
		
		const word = str.slice(i, i+len)
		
		res.push(word)
		
		i+=len
	
	}
	
	return res

}


```