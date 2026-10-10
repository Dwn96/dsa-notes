To do this at constant time, we want to maintain both a stack and a minstack that keeps track of the current smallest. 

```
constructor () // i had forgotten how to do this lmao
{
	this.minStack = []
	this.stack = []
}
```

getMin is just an index into the minStack: 
```
getMin() {
	return this.minStack(this.minStack[this.minStack.length -1])
}
```

pop removes elements from both the minstack and the stack
```
pop() {

	if(this.stack.length === 0) return null
	
	this.minStack.pop()
	
	return this.stack.pop()

}
```

push pushes  (lol) the value  into both minstack and stack

```
push (val) {

	if(this.stack.length === 0) {	
		this.stack.push(val)
		this.minStack.push(val)		
	}
	else {
		this.stack.push(val)
		this.minStack.push(Math.min(val, this.getMin()))
		
	}

}

```