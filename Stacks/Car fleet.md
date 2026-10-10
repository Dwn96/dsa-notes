```
class Solution {

carFleet(target, position, speed) {

const cars = position.map((pos, i) => [pos, speed[i]])

  

/*
Here we sort cars by descending position. We want cars
with bigger pos (closer to target T) starting.

*/

const sorted = cars.sort((a,b) => b[0] - a[0])

  

const stack = []
  

for(const [pos, speed] of sorted) {

const time = (target - pos) / speed  

stack.push(time)

/*
We compare arrival time of the current car and the one from a prev iteration (closer to target T)

If this "current one" has a smaller arrival time we essentially "collapse"
the two times simple because there's no overtaking, they'll merge into a single fleet at some point

*/  

if(stack.length >= 2 && stack[stack.length - 1] <= stack[stack.length - 2] ) {

stack.pop()

}

}

  

return stack.length

}

}
```