## 字符串

### 计算字符串中某个字符出现的次数

```js
let str = "ABCabc",
  target = "A";
//数组化，过滤，然后计算长度差
str.toLowerCase().split(key.toLowerCase()).length - 1;
//正则表达式
let reg = new RegExp(`${target}`, "gi");
let res = str.match(reg) || [];
console.log(res.length);
//转化成哈希结构
let obj = str
  .toLowerCase()
  .split("")
  .reduce((total, curr) => {
    if (total[curr]) {
      total[curr] = total[curr] + 1;
    } else {
      total[curr] = 1;
    }
    return total;
  }, {});
console.log(obj[target.toLowerCase()] || 0);
```

### 字符串颠倒问题

```js
let str = "1516000";
let head = 0,
  tail = str.length - 1;
let headStr = "",
  tailStr = "";
while (head < tail) {
  tailStr += str.charAt(tail);
  headStr = str.charAt(head) + headStr;
  head++;
  tail--;
}

if (head > tail) {
  console.log(`${tailStr}${headStr}`);
} else {
  console.log(`${tailStr}${str.charAt(head)}${headStr}`);
}
```
