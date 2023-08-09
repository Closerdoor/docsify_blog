## 优先级队列

### LeetCode中javascript自带的优先级队列库

介绍：https://www.heibaimeng.com/post/89.html
npm仓库地址：https://www.npmjs.com/package/@datastructures-js/priority-queue
```js
const queue = new PriorityQueue({compare: (a, b) => a - b}) // 小根堆
const queue = new PriorityQueue({compare: (a, b) => b - a}) // 大根堆

const numbers = [3, -2, 5, 0, -1, -5, 4];
const pq = PriorityQueue.fromArray(numbers, (a, b) => a - b); // 小根堆
console.log(numbers); // [-5, -1, -2, 3, 0, 5, 4]
pq.dequeue(); // -5
pq.dequeue(); // -2
pq.dequeue(); // -1
console.log(numbers); // [ 0, 3, 4, 5 ]

pq.enqueue(9);
pq.enqueue(6);

console.log(numbersQueue.front()); 
console.log(bidsQueue.back());

numbersQueue.remove((n) => n === 4); // [4]
console.log(bidsQueue.isEmpty()); 
console.log(bidsQueue.size()); // 3

numbersQueue.toArray()
carsQueue.clear();
```
