Approach is basically to use a set to store unique characters in our iteration.
If we encounter a char that's already in the set(not unique), we shrink the window from the left and delete the char associated with the left index

```js

/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {

    // Set to keep track of unique characters in the current window
    const set = new Set()

    // Start of the sliding window
    let start = 0

    // Length of the longest substring found so far
    let maxLen = 0

    // Expand the window by moving the end pointer
    for(let end = 0; end < s.length; end++) {
        const char = s[end]

        // If the current character already exists in the window,
        // shrink the window from the left until it becomes unique
        while(set.has(char)) {
            // Remove the leftmost character from the window
            set.delete(s[start])

            // Move the start pointer forward
            start++
        }

        // Add the current character to the set
        set.add(char)

        // Calculate the current window length and update maxLen
        maxLen = Math.max(maxLen, end - start + 1)
    }

    // Return the length of the longest substring without repeating characters
    return maxLen
};

```