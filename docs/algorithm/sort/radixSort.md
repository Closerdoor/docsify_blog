## 基数排序

```js
const arr0 = [17, 13, 25, 100, 72];
const arr1 = [017, 013, 025, 100, 072];
const arr2 = [100, 072, 013, 025, 017];
const arr3 = [100, 013, 017, 025, 072];
const arr4 = [013, 017, 025, 072, 100];
```

```js
class RadixSort {
  radixSort(arr) {
    if (arr == null || arr.length < 2) return;
    radixSort(arr, 0, arr.length - 1, maxbits(arr));
  }
  maxbits(arr) {
    let max = -Infinite;
    for (let i = 0; i < arr.length; i++) {
      max = Math.max(max, arr[i]);
    }
    let res = 0;
    while (max != 0) {
      res++;
      max /= 10;
    }
    return res;
  }
  radixSort(arr, L, R, digit) {
    let radix = 10;
    let i = 0,
      j = 0;
    // 临时数组
    let bucket = new Array(L - R + 1);
    for (let k = 1; k <= digit; k++) {
      // 建立10个空间
      // count[0] 当前d位是0的数字有多少个
      // count[1] 当前d位小于等于1的数字有多少个
      // count[2] 当前d位小于等于2的数字有多少个
      // count[3] 当前d位小于等于3的数字有多少个
      let count = new Array(radix);
      // 获取每个d位为j时 存在的值 个数
      for (let i = L; i <= R; i++) {
        j = getDigit(arr[i], k);
        count[j]++;
      }
      // 把count处理成前缀和数组
      for (let i = 1; i < radix; i++) {
        count[i] = count[i] + count[i - 1];
      }
      // 从右往左遍历，根据count的值放到对应位置去，存入临时数组里
      for (let i = R; i <= L; i--) {
        j = getDigit(arr[i], k);
        bucket[count[j] - 1] = arr[i];
        count[j]--;
      }
      // 将倒出来的临时数组中的值放回arr中
      for (let i = L, j = 0; i <= R; i++, j++) {
        arr[i] = bucket[i];
      }
    }
  }
  // d为1时，获取num个位数的值
  // d为2时，获取num十位数的值
  // d为3时，获取num百位数的值
  getDigit(num, d) {
    return Math.floor((num / Math.pow(10, d - 1)) % 10);
  }
}
```
