## 1>相关文章

- ### [日常工作中 @vue/cli 需要关注的一些配置](https://www.cnblogs.com/linjunfu/p/14469768.html)

- ### [Vue-cli卸载](https://blog.csdn.net/m0_58697127/article/details/122926870)

- ### [Vue Cli官网](https://cli.vuejs.org/)




## 2>常用命令

`npm install -g @vue/cli`

`npm uninstall -g @vue/cli`



`vue inspect > webpack.config.js`

导出 webpack 配置信息(导入到项目目录中)，webpack.config.js 可修改成自定义文件名



`vue inspect --mode <mode>`

输出 指定环境 的配置信息 mode：production、test、development



`vue inspect --rules`

查看所有已配置规则名称列表

`vue inspect --rule <ruleName>`

查看指定规则 ruleName： 上述数组选项



`vue inspect --plugins`

查看所有已配置插件列表

`vue inspect --plugin <pluginName>`

查看指定插件配置



`vue inspect -v`

`vue inspect --verbose`

显示完整webpack配置



vue inspect -h
vue inspect --help

`显示帮助信息`



`vue inspect --mode=production > webpack.config.js`

or `vue inspect --mode=production > webpack.config.json5`



`vue create 项目名称`

创建项目



