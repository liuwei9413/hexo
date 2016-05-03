title: Hexo命令总结
date: { { date } }
categories: blog
tags: [Hexo]
---

## 命令总结

### 1.常用命令

`hexo new "postName"` #新建文章
`hexo new page "pageName"` #新建页面
`hexo generate` #生成静态页面至public目录
`hexo server` #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
`hexo deploy` #将.deploy目录部署到GitHub
`hexo help`  # 查看帮助
`hexo version`  #查看Hexo的版本

### 2.复合命令

`hexo deploy -g`  #生成加部署
`hexo server -g`  #生成加预览

命令的简写为：

`hexo n == hexo new`
`hexo g == hexo generate`
`hexo s == hexo server`
`hexo d == hexo deploy`

### 部署步骤

每次部署都可以按照下面的步骤，或者用上面的**复合命令**

`hexo clean`
`hexo generate`
`hexo deploy`

### 本地测试

1.执行下面的命令

`$ hexo g` #生成
`$ hexo s` #启动本地服务，进行文章预览调试

浏览器输入[http://localhost:4000](http://localhost:4000)，查看搭建效果。此后的每次变更_config.yml 文件或者新建文件都可以先用此命令调试，尤其是当你想调试新添加的主题时。

2.可以用一条简化的命令

`$ hexo s -g`

### 结束语

以上是一些Hexo常用的一些操作命令，再次记录下来方便查找。
	