---
title: 二叉树
author: Closerdoor
date: '2023-05-11'
---

## 二叉树数据结构
```js
function TreeNode(x) {
  this.val = x;
  this.left = null;
  this.right = null;
}

TreeNode {
  val: 1,
  left: TreeNode {
    val: 2,
    left: TreeNode { val: 4, left: null, right: null },
    right: TreeNode { val: 5, left: [TreeNode], right: null }
  },
  right: TreeNode {
    val: 3,
    left: null,
    right: TreeNode { val: 6, left: null, right: null }
  }
}
```
## 前序、中序、后序遍历
二叉搜索树的性质，左子树的元素都小于根节点，右子树的元素都大于根节点。因此它的中序遍历（左中右）序列正好是由小到大的次序。
```js
function traverse(root) {
  if(!root) return;
  //前序遍历
  traverse(root.left)
  //中序遍历
  travserse(root.right)
  //后序遍历
}
```
## 重建二叉树
```js
//方法一——二叉树递归
//pre表示前序遍历数组，vin表示中序遍历数组，拆分成左右子树递归
function reConstructBinaryTree(pre, vin) {
  // write code here
  let p = pre.length;
  let v = vin.length;
  if (p == 0 || v == 0) return null;
  let root = new TreeNode(pre[0]);
  for (let i = 0; i < v; i++) {
      if (pre[0] == vin[i]) {
          root.left = reConstructBinaryTree(
              pre.slice(1, i + 1),
              vin.slice(0, i)
          );
          root.right = reConstructBinaryTree(
              pre.slice(i + 1, p),
              vin.slice(i + 1, v)
          );
      }
  }
  return root;
}
//方法二——栈
function reConstructBinaryTree(pre, vin) {
  // write code here
  let p = pre.length;
  let v = vin.length;
  if (p == 0 || v == 0) return null;
  let root = new TreeNode(pre[0]);
  let stack = [];
  let curr = root;
  //遍历前序数组，将值与中序数组一一比对
  for (let i = 1, j = 0; i < p; i++) {
      //当前节点为左节点
      if(curr.val != vin[j]){
          curr.left = new TreeNode(pre[i])
          stack.push(curr);
          curr = curr.left;
      }else {//比对成功，说明左子树已经到根部，往上回溯出栈，遍历右子树
          j++;
          while(stack.length > 0 && stack[stack.length - 1].val === vin[j]){
              curr = stack.pop();
              j++;
          }
          //添加右节点
          curr.right = new TreeNode(pre[i]);
          curr = curr.right;
      }
  }
  return root;
}
```
### 二叉树的深度
```js
//递归
function TreeDepth(pRoot) {
  if (pRoot == null) return 0;
  return Math.max(TreeDepth(pRoot.left),TreeDepth(pRoot.right)) + 1
}
//层序遍历
function TreeDepth(pRoot) {
  let res = 0;
  if (pRoot == null) return res;
  let queue = [pRoot];
  while (queue.length) {
    let len = queue.length;
    for (let i = 0; i < len; i++) {
        let node = queue.shift();
        node.left ? queue.push(node.left) : null;
        node.right ? queue.push(node.right) : null;
    }
    res++;
  }
  return res;
}
```