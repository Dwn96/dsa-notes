Uses stacks (implemented with an array)
So what we essentially need to do is iterate over the string. If the curr is an opening bracket, we push it into the stack. 
Then if we encounter a closing bracket, we pop from the stack and try to see if the current closing matches the popped opening, if not return false.
Also add an edge case for when the string is purely opening brackets so the stack will be empty and will pop undefined.
At the end, if stack is empty we know that the parentheses match