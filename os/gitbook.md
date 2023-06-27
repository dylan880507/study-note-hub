## I>相关文章

[Dylan学习笔记](https://dylan880507.github.io/study-note-hub/)

[GitBook 使用教程](https://blog.csdn.net/raspi_fans/article/details/129570510)

[GitBook讲解](https://blog.csdn.net/qq_41809023/article/details/127514108)

[GitBook - 快速打造可留言的博客](https://juejin.cn/post/6844903848914452488)

[gitbook 入门教程之使用 gitbook-cli 开发电子书](https://juejin.cn/post/6844903812369481741)

[搭建Gitbook并通过Git推送部署](https://www.eula.club/blogs/%E6%90%AD%E5%BB%BAGitbook%E5%B9%B6%E9%80%9A%E8%BF%87Git%E6%8E%A8%E9%80%81%E9%83%A8%E7%BD%B2.html#_1-gitbook-%E7%AE%80%E4%BB%8B)

[发布到Gitee Pages](https://jiangminggithub.github.io/gitbook/chapter-publish-book/2-publish-gitee-pages.html)

[打造完美写作系统：Gitbook+Github Pages+Github Actions](https://blog.csdn.net/qq_40889820/article/details/110013310)

[Linux or Mac 安装 gitbook 3.2.3 失败解决方案](https://xmuli.tech/posts/d7327716/)

[gitbook超全配置](https://www.mapull.com/gitbook/comscore/config/basic.html)

## II>常用命令

```bash
# 全局安装 gitbook-cli, node版本必须是v10.23.0
npm i -g gitbook-cli

# 查看版本
gitbook -V
# 自动创建 README.md 和 SUMMARY.md
gitbook init 

# 全局安装 gitbook-summary
npm install -g gitbook-summary
# 动态生成左侧目录
book sm

# 生成本地web项目
gitbook serve
# 创建prod文件, 可将_book目录内的文件推送到github page, 每次推送后, github page会自动执行work flow, 更新页面内容。
gitbook build
```
