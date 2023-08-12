## leetcode 刷题指南

### leetcode 中可用的第三方库

- LinkedList
- lodash
- PriorityQueue

### 优先级队列 PriorityQueue

介绍：https://www.heibaimeng.com/post/89.html
leecode 引用版本(5.3.0)：https://github.com/datastructures-js/priority-queue/tree/v5.3.0
npm 仓库地址：https://www.npmjs.com/package/@datastructures-js/priority-queue

```js
const queue = new PriorityQueue({ compare: (a, b) => a - b }); // 小根堆
const queue = new PriorityQueue({ compare: (a, b) => b - a }); // 大根堆

queue.enqueue(9); // 增加数据
queue.dequeue(); // 取出顶部的值
queue.size(); // 长度
queue.isEmpty(); // true|false

queue.toArray(); // 把堆中数据转换成数组，小根堆从小到大排序，大根堆相反
queue.front(); // 读取顶部的值(不改变原数据)
queue.back(); // 读取底部的值(不改变原数据)
queue.clear(); // 清空堆
```
