## 贪心算法

有一群孩子和一堆饼干，每个孩子有一个饥饿度，每个饼干有一个大小。每个孩子最多只能吃一个饼干，当饼干大小大于等于孩子饥饿度时，孩子吃饱。求最多有多少个孩子能吃饱。

```
输入
1 2
1 2 3
输出
2
```

```js
let childArr = [1, 2];
let cookieArr = [1, 2, 3];
childArr.sort();
cookieArr.sort();
let sum = 0;
let index = 0;
while (sum < childArr.length && index < cookieArr.length) {
  if (childArr[sum] <= cookieArr[index]) {
    sum++;
  }
  index++;
}
console.log(sum);
```

## 区间问题

给点多个区间，计算让这些区间互不重叠需要移除的区间最少个数。起止相连不算重叠

```
输入
[1,2][2,4][1,3]
输出
1
```

思路:先按照结尾的大小进行排序，每次选择结尾最小且和前一个选择不重叠的区间

```js
let arr = [
  [1, 2],
  [2, 4],
  [1, 3],
];
arr.sort((a, b) => {
  return a[1] - b[1];
});
let count = 1;
let last = arr[0][1];
for (let i = 1; i < arr.length; i++) {
  if (arr[i][0] >= last) {
    last = arr[i][1];
    count++;
  }
}
console.log(arr.length - count);
```

### 买卖股票的最佳时机

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格
思路:如果股票能在下一天卖出，则尽可能多的进行交易

```js
let arr = [7, 1, 5, 3, 6, 4];
```

## 滑动窗口

### 尺取法

### 对撞指针

### 快慢指针

## 二分法(Binary Search)

### 二分法标准模板

```js
let left = -1,right = n
while(left + 1 !==right){
  let mid = (right + left) / 2;
  if(isBlue(mid)){
    left = mid
  }else {
    right = mid
  }
  return left or mid
}
```

## 二维数组的查找

在二维数组 array 中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

```js
//方法一——线性搜索
function Find(target, array) {
  //线性搜索
  /* 
      由于行列递增，可以得出：
      a.在一列中的某个数字，其上的数字都比它小
      b.在一行中的某个数字，其右的数字都比它大
      搜索流程：
      a.首先从 数组左下角 搜索.
      b.如果当前数字大于target,那么查找往上移一位,如果当前数字小于target,那么查找往右移一位。
      c.查找到target,返回true; 如果越界，返回false;
    */
  if (array.length == 0) return false;
  let m = array.length - 1, //行
    n = array[0].length - 1; //列
  let i = 0;
  let j = m;
  while (i <= n && j >= 0) {
    let curr = array[j][i];
    if (curr === target) return true;
    if (curr > target) {
      j--;
    } else {
      i++;
    }
  }
  return false;
}
//方法二——双二分搜索
function Find(target, array) {
  if (array.length == 0) return false;
  return double_binary(array, target, 0, 0, array.length, array[0].length);
}
function double_binary(array, target, x1, y1, x2, y2) {
  if (x1 == x2 || y1 == y2) return false;
  let midX = Math.floor((x1 + x2) / 2);
  let midY = Math.floor((y1 + y2) / 2);
  let curr = array[midX][midY];
  if (curr === target) return true;
  if (curr > target) {
    if (double_binary(array, target, x1, y1, midX, y2)) return true;
    if (double_binary(array, target, midX, y1, x2, midY)) return true;
  } else {
    if (double_binary(array, target, midX + 1, y1, x2, y2)) return true;
    if (double_binary(array, target, x1, midY + 1, midX + 1, y2)) return true;
  }
  return false;
}
```

## 指派问题（匈牙利算法）

匈牙利算法基本思想：先配对的先得，后配对的能让就让，让不了时就是最大配对数

### 素数伴侣

```js
//匈牙利算法
function findArr(oddNum, evenArr, used, matchArr) {
  //循环偶数数组，与传入的奇数配对
  for (let j = 0; j < evenArr.length; j++) {
    //判断该偶数是否配对过
    if (isPrime(oddNum + evenArr[j]) && used[j] === false) {
      used[j] = true;
      //如果该偶数没有其它配对对象，或该偶数的已有配对对象有其它值能配对
      //则将其设置为该奇数的伴侣
      if (matchArr[i] == 0 || find(matchArr[i], evenArr, used, matchArr)) {
        matchArr[i] = oddNum;
        return true;
      }
    }
  }
  //遍历完偶数数组后发现没有能和该奇数配对的，返回false
  return false;
}
```
