Uses stacks (implemented with an array)
So what we're essentially doing is when you encounter an opening bracket like `(`, you immediately push its expected partner `)` onto the stack.
When you encounter a closing bracket in the string, you just pop from the stack and verify that it matches the current character.

```js
function isValid(s) {
    const stack = [];
    const map = {
        '(': ')',
        '{': '}',
        '[': ']'
    };

    for (const char of s) {
        // If it's an opening bracket, push its expected closing partner onto the stack
        if (char in map) {
            stack.push(map[char]);
        } else {
            // It's a closing bracket: check if it matches the top of the stack
            const topElement = stack.pop();
            if (char !== topElement) {
                return false;
            }
        }
    }

    // If the stack is empty, all brackets matched correctly
    return stack.length === 0;
};

```