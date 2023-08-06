## 并查集
### 并查集模板
```js
class UnionFind {
  constructor(n) {
    this.count = n;
    this.parent = new Array(n);
    for (let i = 0; i < n; i++) {
      this.parent[i] = i;
    }
  }
  //找到节点x的连通分量
  find(x) {
    if (x !== this.parent[x]) {
      this.parent[x] = this.find(this.parent[x])
    }
    return this.parent[x];
  }
  //将x,y两个节点连接起来
  union(x, y) {
    let rootX = this.find(x);
    let rootY = this.find(y);
    if (rootX === rootY) return
    this.parent[rootY] = rootX
    this.count--
  }
  //判断x,y两个节点是否连通
  isLink(x, y) {
    let rootX = this.find(x);
    let rootY = this.find(y);
    return rootX === rootY
  }
}
```
