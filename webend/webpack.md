## 1>相关文章 

### [Webpack官网](https://webpack.docschina.org)

### [尚硅谷新版Webpack5实战教程(从入门到精通)](https://www.bilibili.com/video/BV1e7411j7T5)

### [Webpack v4.44.1 中文文档](https://www.bookstack.cn/books/webpack-v4.44.1-zh)

### [webpack externals详解](https://www.tangshuang.net/3343.html)

### [output.filename](https://blog.csdn.net/frontendchen/article/details/110439964)

### [浅谈JSON5](https://www.cnblogs.com/cy0628/p/15179838.html)

### [core-js](https://www.cnblogs.com/sefaultment/p/11631314.html)

### [懒加载](https://www.bilibili.com/video/BV1YU4y1g745?p=44)

### [预获取和预加载](https://www.bilibili.com/video/BV1YU4y1g745?p=45)

### [模块解析(resolve) - 三种路径(绝对路径, 相对路径, 模块路径)讲解](https://www.bilibili.com/video/BV1YU4y1g745?p=64)

### [webpack打包进度展示以及美化教程](https://www.jb51.net/article/235720.htm)

### [babel.config.js 和 .babelrc区别](https://blog.csdn.net/weixin_42622328/article/details/109485207)

### [webpack之externals](https://www.jianshu.com/p/e4f2c985f84a)

### [『Webpack系列』—— externals用法详解](https://blog.csdn.net/Amnesiac666/article/details/121075114)

### [webpack-chain 速查手册之 ChainedSet](https://www.jianshu.com/p/0078e3e2dbf5)

### [webpack-chain 速查手册之 ChainedMap](https://www.jianshu.com/p/620dc8ef3772)

### [webpack高手秘籍（一）](https://www.jianshu.com/p/48fe97716c1e)

### [webpack高手秘籍（二）](https://www.jianshu.com/p/00af97a9845d)

### [webpack高手秘籍（三）](https://www.jianshu.com/p/85c0eb8f3b0f)

### [webpack高手秘籍（四）](https://www.jianshu.com/p/8b55ca0d054a)

### [webpack高手秘籍（五）](https://www.jianshu.com/p/43328baea699)

### [webpack高手秘籍（六）](https://www.jianshu.com/p/bf4547cb197a)

## 2>使用

### *`Webpack的安装和使用`

npm install --save-dev webpack webpack-cli webpack-dev-server

npx webpack (打包)

npx webpack-dev-server (启动node本地服务器)

=>npx webpack serve





## 3>其他知识

### *`3-1>npx的作用: 在当前文件夹及子文件夹中查询指定的插件, 若查询不到, 则往上一层文件夹做相同动作`

### *`3-2>配置 webpack.ProvidePlugin - 全局声明一个包对象, 在需要使用的地方直接使用`

https://webpack.docschina.org/plugins/provide-plugin/#root

https://www.cnblogs.com/moqiutao/p/14379648.html

```js
//1>在webpack.config.js - plugins配置插件
//对于 ES2015 模块的 export default, 必须指定模块的 default 属性
new webpack.ProvidePlugin({
    jsCookie: ["js-cookie", "default"]
});
//或者
new webpack.ProvidePlugin({
    jsCookie: ["js-cookie"]
});
//或者引用本地项目的对象
new webpack.ProvidePlugin({ // 页面中使用jQuery就不需要
    webpack_extend: path.resolve(__dirname, './src/normal_frame_extend.js'),  // 如果你想全局注册你自己模块下的某个文件,你可以这样注册
    $calc: path.resolve(path.join(__dirname, 'src/utils/common.js')),
}),

//2>在package.json - eslintConfig, 配置globals
"eslintConfig": {
	"globals":{
		"jsCookie": "readonly", //也可以是true, readonly表示只读
        "$calc": "readonly",
	}
},

//3>在需要使用的地方直接使用jsCookie对象
jsCookie.set("test-key", "test-val", {
  expires: 1,
  path: "",
  secure: false
});
```

### *`3-3>配置 externals - 包对象使用CDN的方式`

```js
//1>webpack.config.js配置
externalsType: "script",
externals: {
	_lodash: [
		"https://cdn.bootcdn.net/ajax/libs/lodash.js/4.17.21/lodash.core.min.js",
		"_"
	]
},
//2>在需要使用_lodash的地方导入
import _ from "_lodash";
console.log(_);
```

### *`3-4>三种路径解析(绝对路径, 相对路径, 模块路径)`

```js
//1>绝对路径 - 相对于根目录文件夹的路径
/src/index.js
//2>相对路径 - 相对于当前文件的路径
./match.js
//或在webpack.config.js - resolve - alias 配置 { "@": path.resolve(__dirname, "./src") }, 就可如下使用相对路径
@/match.js

//3>模块路径 - import的时候, 对于第三方包, 直接使用包名即可
import _ from 'lodash'
```

### *`3-5>在js文件里引用scss模块文件的几种方式`

```js
// 1.scss文件的名称必须为 *.module.scss, 在js导入才能以模块的形式导入文件
<script>
    import variables from "calc-common/src/styles/variables.scss";
</script>

//variables.scss
:export {
  theme: $--color-primary;
}



// 2.动态为需要模块化的scss文件添加模块化标识
const styleExts = ["scss", "sass", "less"];
const packageCfg = require("./package.json");
let styleModules = [];
const regExp = new RegExp("/", "ig"); //创建正则RegExp对象
if(packageCfg["calc-common"] && packageCfg["calc-common"]["style-modules"]){
  styleModules = packageCfg["calc-common"]["style-modules"]??[];
  styleModules = styleModules.map((mo, index)=>{
    return mo.replace(regExp, path.sep);
  })??[];
}

/**
 * 是否将当前样式文件设置为模块
 * @param {string} filePath 文件路径
 * @return {boolean}
 */
function isStyleModule(filePath){
  try{
    if(!styleModules || styleModules.length<=0){
      return false;
    }
    if(!filePath){
      return false;
    }
    const ext = filePath.split(".")[1]??"";
    if(!ext){
      return false;
    }
  
    if(!styleExts.includes(ext)){
      return false;
    }
  
    return styleModules.some((mo, indx)=>{
      return filePath.indexOf(mo)>=0;
    });
    // return false;
  }catch(err){
    console.log("error...", filePath);
    return false;
  }
}


css: {
    // extract: false, //使用ICSS(行内样式)模式
    // 将css打包成独立文件
    extract: {
      filename: `css/[name].${version}.css`,
      // chunkFilename: `css/chunk.[id].${version}.css`
      chunkFilename: `css/chunk.[name].[contenthash].css`
    },
    sourceMap: !isEnvProd,
    loaderOptions: {
      // https://www.npmjs.com/package/css-loader#modules
      css: {
        modules: {
          auto(resourcePath){
            return isStyleModule(resourcePath);
          },
        },
      //   modules: false, // 默认情况下，只有 *.module.[ext] 结尾的文件才会被视作 CSS Modules 模块。设置为 false 后你就可以去掉文件名中的 .module 并将所有的 *.(css|scss|sass|less|styl(us)?) 文件视为 CSS Modules 模块。
      },
      sass: {
        // sassOptions: {
        //   outputStyle: 'expanded'
        // }
      },
    },
  },
```

