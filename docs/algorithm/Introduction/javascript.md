## null
instanceof 运算符是用来测试一个对象在其原型链构造函数上是否具有 prototype 属性，null 值并不是以 Object 原型创建出来的

## reduce
MDN文档中关于 Array.prototype.reduce()写得很清楚：

如果数组为空并且没有提供initialValue， 会抛出TypeError 。如果数组仅有一个元素（无论位置如何）并且没有提供initialValue， 或者有提供initialValue但是数组为空，那么此唯一值将被返回并且callback不会被执行。

## 运算符优先级
 + 的优先级比条件运算符 condition ? val1 : val2 的优先级高。
1 + 2 ? 4 : 5 => 4

## javascript最大数
在JavaScript中，2^53 是最大的值，没有比这更大的值了。所以 2^53 + 1 == 2^53

## 
-9 % 2 = -1 以及 Infinity % 2 = NaN，求余运算符会保留符号


## 强制数据类型转换
[0] 需要被强制转成 Boolean 的时候会被认为是 true;
== 相等中，如果有一个操作数是布尔类型，会先把他转成数字，所以比较变成了 [0] == 1；
规范指出如果其他类型和数字比较，会尝试把这个类型转成数字再进行宽松比较，而对象（数组也是对象）会先调用它的 toString() 方法，此时 [0] 会变成 "0"，然后将字符串 "0" 转成数字 0，而 0 == 1 的结果显然是 false。

## map
map 方法会给原数组中的每个元素都按顺序调用一次 callback 函数。callback 每次执行后的返回值组合起来形成一个新数组。 callback 函数只会在有值的索引上被调用；那些从来没被赋过值或者使用 delete 删除的索引则不会被调用。

## .小数点运算符
点运算符会被优先识别为数字常量的一部分，然后才是对象属性访问符。所以 3.toString() 实际上被JS引擎解析成 (3.)toString()，显然会出现语法错误。但是如果你这么写 (3).toString()，人为加上括号，这就是合法的。

3.toString(); =>(3.)toString()
3..toString(); =>(3.).toString()

## 正则表达式
每个字面的正则表达式都是一个单独的实例，即使它们的内容相同
var a = /123/;
var b = /123/;
a == b; false
a === b; false

```
var lowerCaseOnly = /^[a-z]+$/;
[lowerCaseOnly.test(null), lowerCaseOnly.test()] => [lowerCaseOnly.test('null'), lowerCaseOnly.test("undefined")]
```
test 方法的参数如果不是字符串，会经过抽象 ToString操作强制转成字符串，因此实际上测试的是字符串 "null" 和 "undefined"。

### 41. 警惕全局匹配
function captureOne(re, str) {
  var match = re.exec(str);
  return match && match[1];
}

var numRe = /num=(\d+)/ig,
      wordRe = /word=(\w+)/i,
      a1 = captureOne(numRe, "num=1"),
      a2 = captureOne(wordRe, "word=1"),
      a3 = captureOne(numRe, "NUM=1"),
      a4 = captureOne(wordRe, "WORD=1");

[a1 === a2, a3 === a4]

// A. [true, true]
// B. [false, false]
// C. [true, false]
// D. [false, true]
答案是C。看MDN关于 exec 方法的描述：

当正则表达式使用 "g" 标志时，可以多次执行 exec 方法来查找同一个字符串中的成功匹配。当你这样做时，查找将从正则表达式的 lastIndex 属性指定的位置开始。

所以a3的值为 null。

### 43. 匹配隐式转换
if("http://giftwrapped.com/picture.jpg".match(".gif")) {
  console.log("a gif file");
} else {
  console.log("not a gif file");
}

// A. "a gif file"
// B. "not a gif file"
// C. error
// D. other
答案是A。看MDN对 match 方法的描述：

如果传入一个非正则表达式对象，则会隐式地使用 new RegExp(obj)
将其转换为正则表达式对象。

所以我们的字符串 ".gif" 会被转换成正则对象 /.gif/，会匹配到 "/gif"。

## replace
replace 方法第二个参数是一个函数，则会在匹配的时候多次调用，第一个参数是匹配的字符串，第二个参数是匹配字符串的下标。所以变成了调用 parseInt(1, 0)、parseInt(2, 2)和parseInt(3, 4)，结果你就懂了。

## 函数
### 函数名无法修改
### 函数长度
Function构造器的属性：
Function 构造器本身也是个Function。他的 length 属性值为 1 。该属性 Writable: false, Enumerable: false, Configurable: true。

Function原型对象的属性：
Function原型对象的 length 属性值为 0 。

`Function.length === 1;
new Function().length === 0;`

## Date
常规调用时会返回一个字符串。`Date(0) => 'Thu Apr 06 2023 23:33:14 GMT+0800 (中国标准时间)'`
`new Date(0) => 返回的是起始日期1970`
`new Date() => 返回的是今天日期`

当Date作为构造函数调用并传入多个参数时，注意月份从0开始。
 new Date(2013, 13, 1)等于new Date(2014, 1, 1)，它们都表示日期2014-02-01（注意月份是从0开始的）
## Math
如果没有参数,Math.min() = Infinity;Math.max() = -Infinity