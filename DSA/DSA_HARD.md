# 💡 DSA - Hard Interview Questions & Solutions

---

### Q1: Trapping Rain Water (Two Pointers $O(N)$ Time, $O(1)$ Space)
**Problem:** Given $N$ non-negative integers representing an elevation map where width of each bar is 1, compute how much water it can trap after raining.

```javascript
function trapRainWater(height) {
  if (!height || height.length === 0) return 0;

  let left = 0, right = height.length - 1;
  let leftMax = 0, rightMax = 0;
  let trappedWater = 0;

  while (left < right) {
    if (height[left] < height[right]) {
      if (height[left] >= leftMax) {
        leftMax = height[left];
      } else {
        trappedWater += leftMax - height[left];
      }
      left++;
    } else {
      if (height[right] >= rightMax) {
        rightMax = height[right];
      } else {
        trappedWater += rightMax - height[right];
      }
      right--;
    }
  }

  return trappedWater;
}

console.log(trapRainWater([0,1,0,2,1,0,1,3,2,1,2,1])); // 6
```

---

### Q2: LRU (Least Recently Used) Cache Implementation ($O(1)$ Get & Put)
**Problem:** Design a data structure that follows the constraints of a Least Recently Used (LRU) cache with $O(1)$ time complexity for both `get` and `put`.

```javascript
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
    this.map = new Map(); // key -> Node
    this.head = new Node(0, 0); // Dummy Head
    this.tail = new Node(0, 0); // Dummy Tail
    this.head.next = this.tail;
    this.tail.prev = this.head;
  }

  _remove(node) {
    node.prev.next = node.next;
    node.next.prev = node.prev;
  }

  _add(node) {
    node.next = this.head.next;
    node.next.prev = node;
    node.prev = this.head;
    this.head.next = node;
  }

  get(key) {
    if (!this.map.has(key)) return -1;
    const node = this.map.get(key);
    this._remove(node);
    this._add(node); // Move to most recently used (head)
    return node.value;
  }

  put(key, value) {
    if (this.map.has(key)) {
      this._remove(this.map.get(key));
    }
    const newNode = new Node(key, value);
    this._add(newNode);
    this.map.set(key, newNode);

    if (this.map.size > this.capacity) {
      const lruNode = this.tail.prev;
      this._remove(lruNode);
      this.map.delete(lruNode.key);
    }
  }
}
```
