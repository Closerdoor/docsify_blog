## 各排序算法的优劣
| 特殊字符 | 时间复杂度 | 空间复杂度|稳定性|
| -------- | -------- | -------- |------|
| 选择排序  | O(n²)   | O(1)      |  ×   |
| 冒泡排序  | O(n²)   | O(1)      |  √   |
| 插入排序  | O(n²)   | O(1)      |  √   |
| 归并排序  | O(n㏒n) | O(n)      |  √   |
| 快速排序  | O(n㏒n) | O(㏒n)    |  ×   |
| 堆排序    | O(n㏒n) | O(1)      |  ×   |

## 快排优化
在样本量比较大的时候，用快排的方式调度。
当样本量变小时，用插入排序