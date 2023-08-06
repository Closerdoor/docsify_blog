---
title: 栈
author: Closerdoor
date: '2023-04-23'
---

### 表达式问题-四则运算
双栈解法：
对于「任何表达式」而言，我们都使用两个栈 nums 和 ops：
nums ： 存放所有的数字
ops ：存放所有的数字以外的操作

然后从前往后做，对遍历到的字符做分情况讨论：

- 空格 : 跳过
- ( : 直接加入 ops 中，等待与之匹配的 )
- ) : 使用现有的 nums 和 ops 进行计算，直到遇到左边最近的一个左括号为止，计算结果放到 nums
- 数字 : 从当前位置开始继续往后取，将整一个连续数字整体取出，加入 nums
- + - * / ^ % : 需要将操作放入 ops 中。在放入之前先把栈内可以算的都算掉（只有「栈内运算符」比「当前运算符」优先级高/同等，才进行运算），使用现有的 nums 和 ops 进行计算，直到没有操作或者遇到左括号，计算结果放到 nums

```js
//给定一个字符串，求助其值
//带括号的四则运算
// -400+5*3+(-5*6-9/3)/2-6*3-4/2+1+(-5*6-9/3)
let str = '400+5*3+(-5*6-9/3)/1-6*3-4/2+1+(-5*6-9/3)';
let nums = [0];
let ops = [];
let opsMap = {
  '+': 1,
  '-': 1,
  '*': 2,
  '/': 2,
}
for (let i = 0; i < str.length; i++) {
  let curr = str[i];
  if (curr === '(') {
    ops.push(curr)
  } else if (curr === ')') {
    //开始计算到左边最近的一个'('
    while (ops.length > 0) {
      if (ops[ops.length - 1] !== '(') {
        calc(nums, ops)
      } else {
        ops.pop()
        break;
      }
    }
  } else {
    if (/\d/.test(curr)) { //数字
      while (i + 1 < str.length && /\d/.test(str[i + 1])) {
        curr = curr + str[i + 1];
        i++;
      }
      nums.push(curr);
    } else { //运算符
      if (i > 0 && (str[i - 1] == '(' || str[i - 1] == '+' || str[i - 1] == '-')) {
        nums.push(0);
      }
      while (ops.length > 0 && ops[ops.length - 1] !== '(') {
        //判断优先级，如果优先级不够则跳出循环
        let last = ops[ops.length - 1];
        if (opsMap[last] >= opsMap[curr]) {
          calc(nums, ops)
        } else {
          break;
        }
      }
      ops.push(curr);
    }
  }
}
while (ops.length > 0) {
  calc(nums, ops)
}
console.log(nums[nums.length - 1])
console.log(eval(str))

function calc(nums, ops) {
  if (nums.length < 2 || ops.length === 0) return;
  let op = ops.pop();
  let b = Number(nums.pop());
  let a = Number(nums.pop());
  switch (op) {
    case "+":
      nums.push(a + b);
      break;
    case "-":
      nums.push(a - b);
      break;
    case "*":
      nums.push(a * b);
      break;
    default:
      nums.push(a / b);
  }
}
```
### 火车进站
描述
给定一个正整数N代表火车数量，0<N<10，接下来输入火车入站的序列，一共N辆火车，每辆火车以数字1-9编号，火车站只有一个方向进出，同时停靠在火车站的列车中，只有后进站的出站了，先进站的才能出站。
要求输出所有火车出站的方案，以字典序排序输出。
 
输入描述：
第一行输入一个正整数N（0 < N <= 10），第二行包括N个正整数，范围为1到10。
输出描述：
输出以字典序从小到大排序的火车出站序列号，每个编号以空格隔开，每个输出序列换行，具体见sample。
```
示例1
输入：
3
1 2 3
复制
输出：
1 2 3
1 3 2
2 1 3
2 3 1
3 2 1
复制
说明：
第一种方案：1进、1出、2进、2出、3进、3出
第二种方案：1进、1出、2进、3进、3出、2出
第三种方案：1进、2进、2出、1出、3进、3出
第四种方案：1进、2进、2出、3进、3出、1出
第五种方案：1进、2进、3进、3出、2出、1出
请注意，[3,1,2]这个序列是不可能实现的。     
```
```js
let n = 3;
let arr = [1,2,3,4]
let result = [];
let inArr = [];
let outArr = [];
dfs(arr,inArr,outArr)
result.sort()
result.forEach(item=>{
    console.log(item)
})
function dfs(arr,inArr,outArr){
    if(outArr.length === n){
        result.push(outArr.join(' '))
        return
    }
    if(arr.length){
        inArr.push(arr.shift())
        dfs(arr,inArr,outArr);
        arr.unshift(inArr.pop())
    }
    if(inArr.length){
        outArr.push(inArr.pop())
        dfs(arr,inArr,outArr);
        inArr.push(outArr.pop())
    }
}
```
## 区间问题
### 区间交叠问题
题目：给定坐标轴上的一组线段，线段的起点和终点均为整数并且长度不小于1，请你从中找到最少数量的线段，这些线段可以覆盖住所有线段。
```
输入
3
1,4
2,5
3,6
输出
2
```
思路：
先将所有线段按起点从小到大排序。
逐个选取每一个线段，将其作为开始的线段，再找出剩余的线段中左端点小于等于开始线段的右端点中（若没有则无解），找出右端点最大的一个线段，起始就是贪心算法。其右端点越大，其右端覆盖到的地方也就最优。反复重复上一步，直到覆盖完整个长度为m的区间，就能得到最少的线段数。

```js
let arr = [
  [1, 4]
  [2, 5]
  [3, 6]
]
arr.sort((a, b) => {
  if (a[0] === b[0]) return a[1] - b[1]
  return a[0] - b[0]
})
console.log(arr)
let stack = [arr[0]]
for (let i = 1; i < arr.length; i++) {
  let curr = arr[i]
  while (true) {
    if (stack.length == 0) {
      stack.push(curr)
      break;
    }
    let [lastStart, lastEnd] = stack[stack.length - 1]
    let [currStart, currEnd] = curr
    if (currStart >= lastEnd) {
      stack.push(arr[i])
      break;
    } else if (currStart <= lastStart) {
      if (currEnd <= lastStart) break;
      if (currEnd <= lastEnd) break;
      stack.pop()
    } else if (currStart < lastEnd) {
      if (currEnd <= lastEnd) break;
      stack.push([lastEnd, currEnd])
      break;
    }
  }
}
```