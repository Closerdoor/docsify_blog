---
title: 链表
author: Closerdoor
date: '2023-05-11'
---

## 链表数据结构
```js
function ListNode(x){
  this.val = x;
  this.next = null;
}
ListNode {
  val: 1,
  next: ListNode {
    val: 2,
    next: ListNode {
      val: 3,
      next: null
    }
  }
}
```
### 查找节点
```js
function findNode(node,val) {
  let currNode = node;
  while(currNode.val !== val){
    currNode = currNode.next;
  }
  if(!currNode) return null
  return currNode;
}
```
### 从尾到头打印链表
```js
function deep(node,arr) {
  if(node != null) {
      deep(node.next,arr)
      arr.push(node.val)
  }
}
```

### 反转链表
```js
//解法一：双指针迭代
function ReverseList(pHead){
  if(!pHead || !pHead.next) return pHead
  let cur = pHead;//当前节点
  let pre = null;//上一个节点
  while(cur != null) {
      let temp = cur.next;
      cur.next = pre;
      pre = cur;
      cur = temp
  }
  return pre
}
//解法二：递归
function ReverseList(pHead){
  if(!pHead || !pHead.next) return pHead;
  let node = ReverseList(pHead.next);
  pHead.next.next = pHead
  pHead.next = null;
  return node
}
```

### 合并两个排序链表
```js
function Merge(pHead1, pHead2) {
  if (!pHead1) return pHead2;
  if (!pHead2) return pHead1;
  if (pHead1.val <= pHead2.val) {
      pHead1.next = Merge(pHead1.next, pHead2);
      return pHead1;
  } else {
      pHead2.next = Merge(pHead2.next, pHead1);
      return pHead2;
  }
}
```

### 删除链表节点
```js
function deleteNode(head, val) {
  if (head.val === val) return head.next;
  let cur = head;//当前节点
  let pre = null;//前序节点
  while (cur.val != val) {
      pre = cur;
      cur = cur.next;
  }
  //断开连接(删除当前节点)
  pre.next = cur.next
  return head 
}
```

### 删除链表中重复的节点
```js
function ListNode(x) {
    this.val = x;
    this.next = null;
}
//方法一——直接迭代比较
function deleteDuplication(pHead) {
  if (pHead == null) return pHead;
  let head = new ListNode(0);//给头部增加一个节点
  head.next = pHead;
  let cur = head;
  while (cur.next && cur.next.next) {
      if (cur.next.val == cur.next.next.val) {
          let temp = cur.next.val;
          while (cur.next != null && cur.next.val == temp) {
              cur.next = cur.next.next;
          }
      } else {
          cur = cur.next;
      }
  }
  return head.next;
}
//方法二——哈希表
function deleteDuplication(pHead) {
  if (pHead == null) return pHead;
  let obj = {};
  let cur = pHead;
  while(cur !=null){
    obj[cur.val] = obj[cur.val] ? obj[cur.val] + 1 : 1
    cur = cur.next
  }
  let head = new ListNode(0)
  head.next = pHead;
  cur = head;
  while(cur.next !=null){
    if(obj[cur.next.val] != 1){
        cur.next = cur.next.next
    }else {
        cur = cur.next
    }
  }
  return head.next
}
```