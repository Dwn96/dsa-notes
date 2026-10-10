The trick is to iterate over the tokens while pushing Numbers into the stack.
Create a map of operators
```
const operands = {

'-' : (num1,num2) => (num1 - num2),

'+' : (num1,num2) => (num1 + num2),

'*' : (num1,num2) => (num1 * num2),

'/' : (num1,num2) => Math.trunc((num1 / num2))

}
```

Btw ensure that we maintain the commutativeness of operations like this. Since a stack is LIFO, the right hand operand will be the first to be popped, then the right hand
```
const num2 = stack.pop()

const num1 = stack.pop()
```

Full code:

```
class Solution {

/**

* @param {string[]} tokens

* @return {number}

*/

evalRPN(tokens) {

const stack = []

const operands = {

'-' : (num1,num2) => (num1 - num2),

'+' : (num1,num2) => (num1 + num2),

'*' : (num1,num2) => (num1 * num2),

'/' : (num1,num2) => Math.trunc((num1 / num2))

}

  

for(const token of tokens) {

if(operands[token]) {

const num2 = stack.pop()

const num1 = stack.pop()

  

const res = operands[token](num1, num2)

  

stack.push(res)

  

} else {

stack.push(Number(token))

}

}

  

return stack[0]

}

}
```