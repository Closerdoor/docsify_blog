## 归并排序

- 时间复杂度：O(nlogn)

```js
function merge(left, right) {
  const result = [];
  while (left.length && right.length) {
    if (left[0] <= right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
  while (left.length) result.push(left.shift());
  while (right.length) result.push(right.shift());
  return result;
}
function mergeSort(arr) {
  if (arr.length < 2) {
    return arr;
  }
  const mid = Math.floor(arr.length / 2);
  const left = arr.slice(0, mid);
  const right = arr.slice(mid);
  return merge(mergeSort(left), mergeSort(right));
}
```

```js
function process(arr, left, right) {
  if (left === right) return;
  let mid = left + ((right - left) >> 1);
  process(arr, left, mid);
  process(arr, mid + 1, right);
  merge(arr, left, mid, right);
}
function merge(arr, left, mid, right) {
  let temp = new Array(right - left + 1);
  let i = 0;
  let p1 = left;
  let p2 = mid + 1;
  while (p1 <= mid && p2 <= right) {
    temp[i++] = arr[p1] < arr[p2] ? arr[p1++] : arr[p2++];
  }
  while (p1 <= mid) {
    temp[i++] = arr[p1++];
  }
  while (p2 <= right) {
    temp[i++] = arr[p2++];
  }
  for (let i = 0; i < temp.length; i++) {
    arr[left + i] = temp[i];
  }
}
```

## 经典例题
### 小和问题
题目:在一个数组中，每一个数左边比当前数小的数累加起来，叫做这个数组的小和。
求解数组[1,3,4,2,5]的小和：
`1 + 1+3 + 1 + 1+3+4+2 =16`
思路:计算每一个数左边比它小的数之和，相当于计算每个数右边有几个数比它大
`1 * 4 + 3 * 2 + 4 * 1 + 2 * 1 = 16` 
利用归并排序时，每一次左右数组merge的时候，因为左右数组都已经是有序的，当左边的数小于右边的数时，说明右边的所有数都比左边数要大，此时就可记录下次数。
### 逆序对问题
思路同上：只是找右边比当前数小的数