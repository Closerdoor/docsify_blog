## 对数器

算法自测:

1. 有一个你想要测的方法 a；
2. 实现一个绝对正确的方法 b(暴力穷举)；
3. 实现一个随机样本生成器；
4. 实现对比算法 a 和 b 的方法；
5. 把方法 a 和方法 b 比对多次来验证方法 a 是否正确；
6. 如果有一个样本使得比对出错，打印样本分析是哪个方法出错；
7. 当样本数量很多时比对测试依然正确，可以确定方法 a 已经正确。

```js
class Solution {
  constructor(maxSize, maxVal) {
    this.maxSize = maxSize;
    this.maxVal = maxVal;
  }
  main() {
    let testTime = 500000;
    let maxSize = 100;
    let maxVal = 100;
    let succeed = true;
    for (let i = 0; i < testTime; i++) {
      //生成随机数组，并克隆一份
      let arr1 = generate_random_array();
      let arr2 = deepClone(arr1);
      //得到2种方法执行后的结果
      let res1 = correct(arr1);
      let res2 = test(arr2);
      //对比两份结果，如果不一样，打印问题数据
      if (!isEqual(res1, res2)) {
        console.log(arr1, arr2);
        succeed = false;
        break;
      }
    }
    console.log("All Clear");
  }
  deepClone() {}
  generate_random_array() {
    let len = Math.floor(Math.random() * this.maxSize);
    const arr = new Array(len);
    for (let i = 0; i < len; i++) {
      arr[i] =
        Math.floor((this.maxVal + 1) * Math.random()) -
        Math.floor(this.maxVal * Math.random());
    }
    return arr;
  }
  correct() {}
  test() {}
  //判断两个结果是否相等
  isEqual(a, b) {
    if (a == null && b != null) return false;
    if (b == null && a != null) return false;
    if (a === b) return true;
    if (Array.isArray(a) && Array.isArray(b)) {
      if (a.length != b.length) return false;
      for (let i = 0; i < a.length; i++) {
        if (a[i] != b[i]) return false;
      }
    }
    return true;
  }
}
```
