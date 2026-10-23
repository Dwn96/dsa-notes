set() uses a simple hashMap
get() uses binary search to find values such that prevTimestamp <= timestamp

```js
class TimeMap {
    constructor() {
        this.keyStore = new Map();
    }

    /**
     * @param {string} key
     * @param {string} value
     * @param {number} timestamp
     * @return {void}
     */
    set(key, value, timestamp) {
        if(!this.keyStore.get(key)) {
            this.keyStore.set(key, [])
        }
        this.keyStore.get(key).push([timestamp, value])
    }

    /**
     * @param {string} key
     * @param {number} timestamp
     * @return {string}
     */
    get(key, timestamp) {
        const values = this.keyStore.get(key)
        if(!values) return ''

        let i = 0
        let j = values.length - 1
        let result = ''

        while(i <= j) {
            let mid = Math.floor((i+j)/2)


            if(values[mid][0] <= timestamp) {
                result = values[mid][1]
                i = mid + 1
            }
            else {
                j = mid - 1
            }
        }

        return result
    }
}

```