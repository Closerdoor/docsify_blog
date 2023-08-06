## 选择排序

每一轮寻找到 0 ~ n-1 中最小值的下标，放到最前面，循环遍历

- 时间复杂度：O(n²)

```js
function selectionSort(arr) {
  if (arr == null || arr.length < 2) return arr;
  for (let i = 0; i < arr.length - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < arr.length; j++) {
      minIndex = arr[j] < arr[minIndex] ? j : minIndex;
    }
    swap(arr, minIndex, i);
  }
}
function swap(arr, i, j) {
  let temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}
```

## 冒泡排序

每一轮只把一个元素冒泡到数列的一端，依次循环遍历，直到所有元素循环一遍。

- 平均时间复杂度：O(n²)
- 最好情况：O(n)
- 最坏情况：O(n²)

```js
/**
 * 冒泡排序
 * @param { Array } arr
 */
function bubbleSort(arr) {
  if (arr == null || arr.length < 2) return arr;
  //0 ~ n
  for (let n = arr.length - 1; n > 0; n--) {
    for (let i = 0; i < n; i++) {
      if (arr[i] > arr[i + 1]) {
        // 元素两两比较大的值放在右边
        swap(arr, i, i + 1);
      }
    }
  }
  return arr;
}
function swap(arr, i, j) {
  arr[i] = arr[i] ^ arr[j];
  arr[j] = arr[i] ^ arr[j];
  arr[i] = arr[i] ^ arr[j];
}
const arr = [2, 5, 1, 7, 4, 9, 6];
console.log(bubbleSort(arr)); // [ 1, 2, 4, 5, 6, 7, 9]
```

## 插入排序

- 平均时间复杂度：O(n²)
- 最好情况：O(n)
- 最坏情况：O(n²)

```js
function insertionSort(arr) {
  if (arr == null || arr.length < 2) return arr;
  for (let i = 1; i < arr.length; i++) {
    for (let j = i - 1; j >= 0; j--) {
      if (arr[j] > arr[j + 1]) {
        swap(arr, j, j + 1);
      } else {
        break;
      }
    }
  }
}
function swap(arr, i, j) {
  arr[i] = arr[i] ^ arr[j];
  arr[j] = arr[i] ^ arr[j];
  arr[i] = arr[i] ^ arr[j];
}
```

### 简单排序

```js
var arr = [8, 4, 6, 3, 10, 2, 7, 9, 11, 1];

//排序3
for (let i = 0; i < arr.length; i++) {
  let key = arr[i],
    j = i - 1;
  while (arr[j] > key) {
    arr[j + 1] = arr[j];
    j--;
  }
  arr[j + 1] = key;
}
console.log(arr);
```
