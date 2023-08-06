## 堆

```js
const arr = [3, 5, 2, 7, 1, 9, 6];
const size = arr.length;
// 取一个下标i
// 他的左孩子是 2*i+1
// 他的右孩子是 2*i+2
// 他的父亲是 (i - 1) / 2
```

## 堆排序

```js
function heapSort(arr) {
  if(arr == null || arr.length < 2) return;
  //堆排序两种方法
  for(let i=0;i<arr.length;i++){
    headpInsert(arr,i);
  }
  // for(let i=arr.length-1;i>=0;i--){
  //   heapify(arr,i,arr.length)
  // }
  let heapSize = arr.length;
  heapSize--;
  swap(arr,0,heapSize);
  while(heapSize > 0) {
    heapify(arr,0,heapSize);
    heapSize--;
    swap(arr,0,heapSize);
  }
}
// 新增子节点时，通过 headInsert 不断和父节点比较，交换位置，保持大根堆
function heapInsert(arr, index) {
  while (arr[index] > arr[~~((index - 1) / 2)]) {
    swap(arr, index, ~~((index - 1) / 2));
    index = ~~((index - 1) / 2));
  }
}

// 去除根节点时，将index位置的值与孩子比较，保持大根堆
function heapify(arr, index, heapSize) {
  let left = 2 * index + 1;
  while(left < heapSize) {
    // 比较左右孩子哪个更大
    let big = left + 1 < heapSize && arr[left + 1] > arr[left] ? left + 1 : left;
    // 父亲和大孩子比较
    big = arr[big] > arr[index] ? big : index;
    if(big === index) {
      break;
    }
    swap(arr,big,index);
    index = big;
    left = 2 * index + 1;
  }
}
```
