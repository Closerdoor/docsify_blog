---
title: 基础数学
author: Closerdoor
date: "2023-04-23"
---

### 求两个数的最小公因数

```js
function getFactor(a, b) {
  if (b == 0) {
    return a;
  }
  let c = a % b;
  return getFactor(b, c);
}
```

### 求两个数的最小公倍数

```js
function getMultiple(a, b) {
  return (a * b) / getFactor(a, b);
}
```

### 求是否为素数(质数)

```js
function isPrime(num) {
  if (num < 2) return false;
  if (num === 2) return true;
  for (let i = 0; i <= Math.sqrt(num); i++) {
    if (num % i === 0) return false;
  }
  return true;
}
```

### 取余递推公式

题目:
给你一个下标从 0 开始的字符串 word ，长度为 n ，由从 0 到 9 的数字组成。另给你一个正整数 m 。

word 的 可整除数组 div  是一个长度为 n 的整数数组，并满足：

如果 word[0,...,i] 所表示的 数值 能被 m 整除，div[i] = 1
否则，div[i] = 0
返回 word 的可整除数组。

示例 1：
```
输入：word = "998244353", m = 3
输出：[1,1,0,0,0,1,1,0,0]
解释：仅有 4 个前缀可以被 3 整除："9"、"99"、"998244" 和 "9982443" 。
```

示例 2：
```
输入：word = "1010", m = 10
输出：[0,1,0,1]
解释：仅有 2 个前缀可以被 10 整除："10" 和 "1010" 。
```

```js
/**
 * @param {string} word
 * @param {number} m
 * @return {number[]}
 */
var divisibilityArray = function (word, m) {
  const n = word.length;
  const div = new Array(n).fill(0);
  let prev = 0;
  for (let i = 0; i < n; i++) {
    const curr = Number(word[i]);
    prev = (prev * 10 + curr) % m;
    if (prev === 0) {
      div[i] = 1;
    }
  }
  return div;
};
```
