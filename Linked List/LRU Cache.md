Uses a doubly linked list
```js
class Node {
    constructor(key, value) {
        this.key = key;
        this.value = value;
        this.prev = null;
        this.next = null;
    }
}

class LRUCache {
    constructor(capacity) {
        this.capacity = capacity;
        this.cache = new Map();

        // Dummy nodes
        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);

        this.head.next = this.tail;
        this.tail.prev = this.head;
    }

    // Remove a node from the linked list
    remove(node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    // Insert a node immediately after head (MRU)
    insert(node) {
        const next = this.head.next;

        this.head.next = node;
        node.prev = this.head;

        node.next = next;
        next.prev = node;
    }

    get(key) {
        if (!this.cache.has(key)) return -1;

        const node = this.cache.get(key);

        // Accessing a node makes it recently used
        this.remove(node);
        this.insert(node);

        return node.value;
    }

    put(key, value) {
        // If key already exists, remove its old node
        if (this.cache.has(key)) {
            this.remove(this.cache.get(key));
        }

        const node = new Node(key, value);

        // Add new/updated node as most recently used
        this.cache.set(key, node);
        this.insert(node);

        // Evict LRU if capacity is exceeded
        if (this.cache.size > this.capacity) {
            const lru = this.tail.prev;

            this.remove(lru);
            this.cache.delete(lru.key);
        }
    }
}

```