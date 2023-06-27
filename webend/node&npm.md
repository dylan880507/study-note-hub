## 1>相关文章

- ### [npm官网](https://www.npmjs.com/)

- ### [nodejs官网](https://nodejs.org/zh-cn/)

- ### [nvm介绍及使用](https://www.cnblogs.com/yeminglong/p/12971969.html)

- ### [发布一个npm包，构建自己的第三方库](https://www.jianshu.com/p/14e5b3917d19)

- ### [如何创建自己的npm包](https://www.52pojie.cn/thread-897339-1-1.html)

- ### [npm包的介绍、前端实现自己的包并上传到npm仓库的方法](https://blog.csdn.net/to_the_Future/article/details/122949610?utm_source=app&app_version=5.3.0)

- ### [上传npm包](https://www.cnblogs.com/xiaozhuangge/p/15799876.html)

- ### [使用webpack构建属于你自己的npm包](https://blog.csdn.net/fed_guanqi/article/details/122347287)

- ### [记npm包开发全过程](https://blog.csdn.net/white__cat/article/details/77051995)

- ### [创建自己的library类库包并使用webpack4.x打包发布到npm](https://www.cnblogs.com/weiqinl/p/9786966.html)

- ### [webpack4与babel配合使es6代码可运行于低版本浏览器](https://www.cnblogs.com/weiqinl/p/9773048.html)

- ### [webpack发布npm-package](https://www.bilibili.com/video/BV1YU4y1g745?p=85)

- ### [npm 发布如何忽略指定的文件](https://blog.csdn.net/terrychinaz/article/details/112976268)

- ### [element-ui组件库二次开发——打包、上传npm](https://www.cnblogs.com/tlsmile/p/13274162.html)

- ### [前端多个vue项目公共组件的三种方法（推荐npm file引入）](https://blog.csdn.net/milugloomy/article/details/103187370)

- ### [npm file方式引入公共包遇到的几个坑](https://blog.csdn.net/milugloomy/article/details/111461405)

## 2>常用命令

### `npm`

#### `npm install webpack webpack-cli --global` (全局安装插件)

=>`npm install webpack webpack-cli -g`

#### `npm ls element-ui`(查看某个包本地当前的版本)

#### `npm view element-ui versions`(查看包所有版本)

#### `npm view element-ui version`(查看包的最新版本)

#### `npm info element-ui`(查看包的更多版本信息)

#### `npm install calc-common` (在dependencies, devDependencies安装)

#### `npm install --save calc-common` (在dependencies, devDependencies安装)

#### `npm install --save-dev calc-common` (只在devDependencies安装)

=>`npm install -D`

#### `npm i --save-dev mini-css-extract-plugin@1.0.0`(安装指定版本的包)

#### `npm i xxx@latest --save-dev`(安装指定的包最新的版本)

#### `npm uninstall calc-common`(卸载包)

`npm uninstall jquery bootstrap babel` (卸载多个包)

#### `npm update xxx -D`(升级指定包)

#### `npm view autoprefixer versions`(查看指定包可用的版本)

#### 删除 node_modules 依赖

#### `npm install rimraf -g
rimraf node_modules`

#### `npm init` (初始化自定义包的环境)

#### `npm config get registry` (查看镜像地址)

#### `npm config set registry URL` (设置镜像地址)

#### `npm config set registry https://registry.npm.taobao.org` (设置淘宝镜像源)

#### `npm config set registry https://registry.npmjs.org` (设置npm官方像源)

#### `npm login`(登录npm账号)

#### `npm adduser`(创建npm账号)

#### `npm publish` (上传发布)

#### `npm version patch` (更新版本)

#### `npm unpublish 包名@版本号` (删除指定的版本)

#### `npm unpublish 包名 --force` (删除整个包, 会有警告提示, 删除后该包名24小时之内不可再用)

#### `npm audit --json` (查看需要手动更新的漏洞)

#### `npm prune`(清理不必要的软件包)

#### `npm config set proxy null` (取消代理)

`npm config set https-proxy null` (取消https代理)

`npm install -g cnpm` (全局安装cnpm)

`npm cache clear --force` (强制刷新npm缓存)

`npm cache dir` (查看npm缓存的位置)

### `nvm`

#### `nvm list available`：列出所有可以安装的node版本号

#### `nvm ls`：列出所有已经安装的node版本

#### `nvm install v10.4.0`：安装指定版本号的node

#### `nvm uninstall v10.4.0`：删除指定版本号的node

#### `nvm current`：当前node版本

#### `nvm use v10.3.0`：切换node的版本，这个是全局的

### `nrm`

#### `npm i -g nrm open@8.4.2` 全局安装npm的镜像源管理工具, open包必须制定8.4.2, 不然nrm使用会报错

#### `nrm ls` 查看所有可用的镜像

#### `nrm use` 镜像名称

#### `nrm current` 查看当前所用镜像

#### `nrm add taobao2 https://registry.npm.taobao.org` 添加镜像地址

## 3>其他知识点

### *`dependencies`(生产依赖): 如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。

### *`devDependencies`(开发依赖): 如果某些包只在项目开发阶段会用到，在项目上线之后不会用到，则建议把这些包记录到devDependencies 节点中。

### *`如何仅仅安装生产依赖?`

默认npm install 会安装所有依赖（开发和生产依赖都安装）

通过–production 选项可以仅仅安装生产依赖

```shell
npm install --production
```

### *自定义.env, 及.env文件讲解

若需要自定义.env文件, 文件名称必须是.env`.自定义名称`, 如.env.report, 文件内容如下

另, 根目录下可以创建.env文件, 该文件内的配置优先级低于指定环境的配置文件

```ini
# NODE_ENV 将决定您的应用运行的模式，是开发，生产还是测试，因此也决定了创建哪种 webpack 配置，如果文件内部不包含 NODE_ENV 变量，它的值将取决于模式，例如，在 production 模式下被设置为 "production"，在 test 模式下被设置为 "test"，默认是 "development"。
NODE_ENV = production
BABEL_ENV = production

# 环境变量必须是 VUE_APP_ 开头
VUE_APP_ENV = 'report'

#项目中读取方式
process.env.VUE_APP_ENV
```

### *dial tcp 104.20.22.46:443 timeout

```bash
nvm node_mirror https://npm.taobao.org/mirrors/node/
```

