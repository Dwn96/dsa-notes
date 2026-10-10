Uses a  Decreasing [[Monotonic Stack]]
We want our stack to always have warmer temperatures than our current position in the loop.
Remember our stack stores **indices** so be careful when running checks!!!!

**Steps**
Initialize our stack and our  output arr
```js
const res = []
const stack = []
```

We want to iterate from the back and at every step, lets check if the value at the top of our stack is  <=  to our current temp.
If it smaller, we want to pop continuously (while loop!) until we find one that is.

We calculate the difference in days with `stack[stack.length - 1] - i`
because remember we're iterating from the back so indices from a prev iteration held in the stack will always be bigger than our current i

```js

for(let i = temps.length - 1; i >-1; i --) {
	
	while(stack.length && temps[i] >= temps[stack[stack.length - 1]]) {
		stack.pop()
	}
	
	if(stack.length > 0) {
		
		res[i] = stack[stack.length - 1] - i
		
	}
	else {
		res[i] = 0
	}

}

```
