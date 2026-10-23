To do this at constant time, we want to maintain both a stack and a minstack that keeps track of the current smallest. 

```js

class MinStack {
    constructor() {
        this.stack = [];
        this.minStack = [];
    }

    push(value) {
        this.stack.push(value);

        // Check if minStack is empty, or if value is less than or equal to current minimum
        if (this.minStack.length === 0 || value <= this.getMin()) {
            this.minStack.push(value);
        }
    }

    pop() {
        const popped = this.stack.pop();

        // If the popped element matches the current minimum, pop it from minStack too
        if (popped === this.getMin()) {
            this.minStack.pop();
        }
    }

    top() {
        return this.stack[this.stack.length - 1];
    }

    getMin() {
        return this.minStack[this.minStack.length - 1];
    }
}

```