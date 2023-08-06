## 快速排序

### 荷兰国旗问题

题目一：给定一个数组 arr，和一个数 num，把小于等于 num 的数放在左边，把大于 num 的数放在右边。

思路:
两个指针，一个表示左侧区域，一个表示当前下标。

- 当前值[i]小于等于 num 时，[i]与左侧区域的下一个值交换位置,左侧区域右移,i++;
- [i] > num,i++;

题目二：给定一个数组 arr，和一个数 num，把小于 num 的数放在左边，等于 num 的数放中间，大于 num 的数放在右边。

思路:
三个指针，一个表示左侧区域，一个表示当前下标，一个表示右侧区域

- 当前值[i]小于 num 时，[i]与左侧区域的下一个值交换位置,左侧区域右移,i++;
- 当前值[i]等于 num 时,i++;
- 当前值[i]大于 num 时,[i]与右侧区域的前一个值交换位置，右侧区域左移;

```js
const arr = [3, 5, 6, 3, 4, 5, 2, 6, 9, 0];
const num = 5;
function partition1(arr) {
  let left = -1;
  let i = 0;
  while (i < arr.length) {
    let curr = arr[i];
    if (curr <= num) {
      swap(arr, i, left + 1);
      left++;
    }
    i++;
    console.log(arr);
  }
}
function swap(arr, i, j) {
  let temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}
function partition2(arr) {
  let left = -1;
  let right = arr.length;
  let i = 0;
  while (i < arr.length && i < right) {
    let curr = arr[i];
    if (curr < num) {
      swap(arr, i, left + 1);
      left++;
      i++;
    } else if (curr === num) {
      i++;
    } else {
      swap(arr, i, right - 1);
      right--;
    }
    console.log(arr);
  }
}
```

### 快速排序 1.0

### 快速排序 2.0

### 快速排序 3.0

- 时间复杂度：概率上达到 O(nlogn)

```js
function quickSort(arr, l, r) {
  if (l < r) {
    swap(arr, l + Math.floor(Math.random() * (r - l + 1)), r);
    let temp = partition(arr);
    quickSort(arr, l, temp[0] - 1);
    quickSort(arr, temp[0] + 1, r);
  }
}
function partition(arr, l, r) {
  let less = l - 1; //<区右边界
  let more = r; //>区左边界
  while (l < more) {
    if (arr[l] < arr[r]) {
      swap(arr, less + 1, l);
      l++;
    } else if (arr[l] > arr[r]) {
      swap(arr, more - 1, l);
      more--;
    } else {
      l++;
    }
  }
  swap(arr, more, r);
  return [less + 1, more];
}
function swap(arr, i, j) {
  let temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}
```
