## DFS
### 从数组中随机选取任意个，输出所有可能的方案(指数型排列)
```js
let arr = [1, 3, 5, 7, 9];
let result = [];
dfs(0,[])
console.log(result)
// x 表示当前枚举到了哪个位置
function dfs(x,path) {
  if (x >= arr.length) {
    result.push([...path])
    return
  }
  //选
  path.push(arr[x])
  dfs(x + 1, path)
  path.pop()
  //不选
  dfs(x + 1, path)
}
```
### 按照字典序输出一个数组所有不重复的排列(全排列)
```js
let arr = [1, 3, 5, 7, 9];
let used = [false, false, false, false, false]
let result = []

dfs(0, [])
console.log(result)
// x 表示当前枚举到了哪个位置
function dfs(x,path) {
  if (x >= arr.length) {
    result.push([...path])
    return
  }
  //第一个位置
  for (let i = 0; i < arr.length; i++) {
    if (!used[i]) {
      used[i] = true;
      path.push(arr[i])
      dfs(x + 1, path)
      used[i] = false;
      path.pop()
    }
  }
}
```
### 从数组中抽出r个元素，求出其所有的组合
```js
let arr = [1, 3, 5, 7, 9];
let r = 4;
let result = []
function dfs(x,start,path){
  if (x >= n) {
    result.push([...path])
    return
  }
  for (let i = start; i < arr.length; i++) {
    path.push(arr[start])
    dfs(x + 1, i + 1,path)
    path.pop()
  }
}
```
### dfs区间搜索
```js
//让开始点直接定位
for (let i = 1; i <= n; i++) {
  if (count == 0) {
    i = ~~String(start)[x - 1];
  }
  if (!used[i]) {
    used[i] = true;
    path.push(i)
    dfs(x + 1, path)
    used[i] = false
    path.pop()
  }
}
```

### 最简单的全排列
给一个没有重复数字的序列，返回所有可能的全排列
```js
let arr = [1, 2, 3, 4];
let result = [];
dps(arr)
console.log(result)

function dps(arr, path = []) {
  if (path.length === arr.length) {
    result.push([...path]);
    return;
  }
  for (let i = 0; i < arr.length; i++) {
    path.push(arr[i]);
    dps(arr, path);
    path.pop();
  }
}
```
### 全排列变种——每个数字只能使用一次
```js
let arr = [1, 2, 3, 4];
let result = [];
dps(arr,[],used = new Array(arr.length).fill(false))

function dps(arr, path = [],used) {
  if (path.length === arr.length) {
    result.push([...path]);
    return;
  }
  for (let i = 0; i < arr.length; i++) {
    //剪枝结构1——发现重复的数字，跳过它继续循环
    if(used[i] === true){
      continue;
    }
    used[i] = true;
    path.push(arr[i]);
    dps(arr, path,used);
    path.pop();
    used[i] = false;
  }
}
```
### 全排列变种——给定一个有重复数字的序列，进行全排列
```js
let arr = [1, 2, 1, 4];
//先对数组进行排序
arr.sort()
let result = [];
dps(arr,[],used = new Array(arr.length).fill(false))
console.log(result)
function dps(arr, path = [],used) {
  if (path.length === arr.length) {
    result.push([...path]);
    return;
  }
  for (let i = 0; i < arr.length; i++) {
    //剪枝结构1——发现重复的数字，跳过它继续循环
    if(used[i] === true){
      continue;
    }
    //剪枝结构2——发现数字与同层的重复，则结果一样，跳过它继续循环
    if(i > 0 && arr[i] === arr[i-1] && used[i-1]===false){
      continue;
    }
    used[i] = true;
    path.push(arr[i]);
    dps(arr, path,used);
    path.pop();
    used[i] = false;
  }
}
```
### 全排列变种——给定一个无重复数字的数组arr和一个目标数target，找出arr中使数字和为target的组合
```js
let arr = [1, 2, 3, 4];
let target = 5;
arr.sort()
let result = [];
dps(arr)
console.log(result)
function dps(arr, path = [],total = 0,start = 0) {
  //如果path是引用数据结构，要做深拷贝，否则回溯的时候会影响结果
  if (total === target) {
    result.push([...path]);
    return;
  }
  //剪枝结构3——当总和大于指定值时，不进入循环
  //剪枝结构4——让i从start处开始，跳过之前已经循环过的值
  for (let i = start; (i < arr.length && total + arr[i] <=target); i++) {
    path.push(arr[i]);
    total = total + arr[i];
    dps(arr, path,total,i);
    total = total - arr[i];
    path.pop();
  }
}
```

### 取出数组中所有排列组合
```js
/**
 * 
 * @param {*} source 源数组
 * @param {*} count 要取出多少项
 * @param {*} isPermutation 是否使用排列的方式
 * @return {any[]} 所有排列组合,格式为 [ [1,2], [1,3]] ...
 */
function getPC(source, count, isPermutation = true) {
  //如果只取一位，返回数组中的所有项，例如 [ [1], [2], [3] ]
  let currentList = source.map((item) => [item]);
  if (count === 1) {
    return currentList;
  }
  let result = [];
  //取出第一项后，再取出后面count - 1 项的排列组合，并把第一项的所有可能（currentList）和 后面count-1项所有可能交叉组合
  for (let i = 0; i < currentList.length; i++) {
    let current = currentList[i];
    //如果是排列的方式，在取count-1时，源数组中排除当前项
    let children = [];
    if (isPermutation) {
      children = getPC(source.filter(item => item !== current[0]), count - 1, isPermutation);
    }
    //如果是组合的方法，在取count-1时，源数组只使用当前项之后的
    else {
      children = getPC(source.slice(i + 1), count - 1, isPermutation);
    }
    for (let child of children) {
      result.push([...current, ...child]);
    }
  }
  return result;
}

let arr = [1, 2, 3];

const result = getPC(arr, 2, false);
console.log(result);
//[ [ 1, 2 ], [ 1, 3 ], [ 2, 3 ] ]

const result2 = getPC(arr, 2);
console.log(result2);
//[ [ 1, 2 ], [ 1, 3 ], [ 2, 1 ], [ 2, 3 ], [ 3, 1 ], [ 3, 2 ] ]
```