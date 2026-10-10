Man todays questions is pretty dope. We have an array that's sorted in increasing order.
Lets init 2 pointers

```js
let left = 0
let right = arr.length - 1

```

This is quite similar to valid palindrome but we move the pointers in a pretty clever way

```js
while(left < right) {

const currentSum = arr[left] + arr[right]

if(currentSum === target) return [left + 1, right + 1] // our questions specifies that the arrr is 1 indexed


/*
we've overshot, lets move our right point back, remember this array is sorted in increasing order

*/
else if (currentSum > target) { 
	right--
} 
else { // currentSum is smaller than target, lets move left pointer to a bigger v
	left++
}

}

```

$O(N)$ runtime and $O(1)$ auxiliary space