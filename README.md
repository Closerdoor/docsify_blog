## 目录结构
- docs
    - en  => 英文版目录
    - imgs  => 图片目录
    - user  => 文档目录 user/README.md就是对应user的主页
    - .nojekyll => 阻止 GitHub Pages 会忽略掉下划线开头的文件
    - _coverpage.md => 封面编写(设置了coverpage为true后有效)
    - _sidebar.md => 左侧目录
    - index.html  => 入口文件，进行docsify的各项配置
    - README.md => 默认展示的首页对应界面

## 运行
```
docsify serve docs(文件夹目录)
```