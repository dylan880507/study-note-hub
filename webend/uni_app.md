## I>相关文章

###### [uniapp-微信小程序关于禁止ios自带的下拉上拉（橡皮筋回弹）](https://blog.csdn.net/m0_61702149/article/details/126547969)

###### [HbuilderX使用教程](https://hx.dcloud.net.cn/README)

###### [HbuilderX插件市场](https://ext.dcloud.net.cn/?cat1=1&cat2=11&orderBy=FreeHot)

###### [uni-app教程](https://uniapp.dcloud.net.cn/)

###### [uni-app UI框架 - uView](https://www.uviewui.com/)

###### [uni-app 国际化](https://uniapp.dcloud.net.cn/tutorial/i18n.html)

###### [shopro商城使用vue-i18n国际化](https://segmentfault.com/a/1190000041138464)

###### [uni-app 国际化开发](https://blog.csdn.net/wwt4007253/article/details/118400225)

###### [h5+ API](https://www.html5plus.org/doc/zh_cn/accelerometer.html)

###### [5+ App开发Native.js入门指南](https://ask.dcloud.net.cn/docs/#//ask.dcloud.net.cn/article/88)

###### [苹果开发者网站](https://developer.apple.com/account)

###### [创建苹果P12证书和描述文件](https://ask.dcloud.net.cn/article/40301)

###### [真机运行常见问题](https://uniapp.dcloud.net.cn/tutorial/run/run-app-faq.html)

###### [使用Apple证书签名iOS标准基座](https://uniapp.dcloud.net.cn/tutorial/run/ios-apple-certificate-signature.html)

###### [uni-app导航栏开发指南](https://ask.dcloud.net.cn/article/34921)

###### [导航栏示例应用](https://ext.dcloud.net.cn/plugin?id=1765)

[uni-app subNVue 原生子窗体开发指南](https://ask.dcloud.net.cn/article/35948)

###### [uni-app 怎么实现路由拦截](https://blog.csdn.net/web2022050903/article/details/127105362)

###### [拦截器应用示例 — 图片选择](https://ext.dcloud.net.cn/plugin?id=5095)

###### [App权限判断和提示](https://ext.dcloud.net.cn/plugin?id=594)

[系统剪贴板](https://ext.dcloud.net.cn/plugin?id=2875)



## II>uni-app教程

### `1. uni-app工程目录`

┌─uniCloud              云空间目录，阿里云为uniCloud-aliyun,腾讯云为uniCloud-tcb（详见[uniCloud](https://uniapp.dcloud.net.cn/uniCloud/quickstart.html#structure)）
│─components            符合vue组件规范的uni-app组件目录
│  └─comp-a.vue         可复用的a组件
├─utssdk                存放uts文件
├─pages                 业务页面文件存放的目录
│  ├─index
│  │  └─index.vue       index页面
│  └─list
│     └─list.vue        list页面
├─static                存放应用引用的本地静态资源（如图片、视频等）的目录，注意：静态资源只能存放于此
├─uni_modules           存放[uni_module](/uni_modules)。
├─platforms             存放各平台专用页面的目录，[详见](https://uniapp.dcloud.net.cn/tutorial/platform.html#%E6%95%B4%E4%BD%93%E7%9B%AE%E5%BD%95%E6%9D%A1%E4%BB%B6%E7%BC%96%E8%AF%91)
├─nativeplugins         App原生语言插件 [详见](https://nativesupport.dcloud.net.cn/NativePlugin/#)
├─nativeResources       App端原生资源目录
│  └─android            Android原生资源目录 [详见](https://uniapp.dcloud.net.cn/tutorial/app-nativeresource-android.html#)
├─hybrid                App端存放本地html文件的目录，[详见](https://uniapp.dcloud.net.cn/component/web-view.html#)
├─wxcomponents          存放小程序组件的目录，[详见](https://uniapp.dcloud.net.cn/tutorial/miniprogram-subject.html#%E5%B0%8F%E7%A8%8B%E5%BA%8F%E7%BB%84%E4%BB%B6%E6%94%AF%E6%8C%81)
├─unpackage             非工程代码，一般存放运行或发行的编译结果
├─AndroidManifest.xml   Android原生应用清单文件 [详见](https://uniapp.dcloud.net.cn/tutorial/app-nativeresource-android.html#)
├─main.js               Vue初始化入口文件
├─App.vue               应用配置，用来配置App全局样式以及监听 [应用生命周期](https://uniapp.dcloud.net.cn/collocation/App.html#%E5%BA%94%E7%94%A8%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
├─manifest.json         配置应用名称、appid、logo、版本等打包信息，[详见](https://uniapp.dcloud.net.cn/collocation/manifest.html#)
├─pages.json            配置页面路由、导航条、选项卡等页面类信息，[详见](https://uniapp.dcloud.net.cn/collocation/pages.html#)
└─uni.scss              这里是uni-app内置的常用样式变量



`static目录` 使用注意

- 编译到任意平台时，`static` 目录下除不满足[条件编译](https://uniapp.dcloud.net.cn/tutorial/platform.html#static-目录的条件编译)的文件，会直接复制到最终的打包目录，不会打包编译。非 `static` 目录下的文件（vue、js、css 等）只有被引用时，才会被打包编译。
- `css`、`less/scss` 等资源不要放在 `static` 目录下，建议这些公用的资源放在自建的 `common` 目录下。



### `2. 页面`

#### `2.1 Note`

* 指符合`Vue SFC规范`的`.vue`文件或`.nvue`文件。

* `.vue`页面和`.nvue`页面，均全平台支持，差异在于当uni-app发行到App平台时，`.vue`文件会使用webview进行渲染，`.nvue`会使用原生进行渲染。

* 在工程根目录下的`pages`目录下。

* 每次新建页面，均需在`pages.json`中配置`pages`列表；未在`pages.json -> pages` 中配置的页面，`uni-app`会在编译阶段进行忽略。

* 删除页面时，需做两件工作：1. 删除`.vue`文件或`.nvue`文件; 2. 删除`pages.json -> pages`列表项中的配置。

* `pages.json -> pages`配置项中的第一个页面，作为当前工程的首页（启动页）。

* [页面生命周期](https://uniapp.dcloud.net.cn/tutorial/page.html#lifecycle)

  1. 支持 Vue 组件生命周期

  2. onInit: 监听页面初始化，其参数同 onLoad 参数，为上个页面传递的数据，参数类型为 Object（用于页面传参），触发时机早于 onLoad => 百度小程序

     - 仅百度小程序基础库 3.260 以上支持 onInit 生命周期
     - 其他版本或平台可以同时使用 onLoad 生命周期进行兼容，注意避免重复执行相同逻辑
     - 不依赖页面传参的逻辑可以直接使用 created 生命周期替代

  3. onLoad: 监听页面加载，其参数为上个页面传递的数据，参数类型为 Object（用于页面传参），参考[示例](https://uniapp.dcloud.net.cn/api/router#navigateto)

  4. onShow: 监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面

  5. onReady: 监听页面初次渲染完成。注意如果渲染速度快，会在页面进入动画完成前触发

  6. onHide: 监听页面隐藏

  7. onUnload: 监听页面卸载

  8. onResize: 监听窗口尺寸变化 => App、微信小程序、快手小程序

  9. onPullDownRefresh: 监听用户下拉动作，一般用于下拉刷新，参考[示例](https://uniapp.dcloud.net.cn/api/ui/pulldown)

  10. onReachBottom: 页面滚动到底部的事件（不是scroll-view滚到底），常用于下拉下一页数据。具体见下方注意事项

      * 使用注意 可在pages.json里定义具体页面底部的触发距离[onReachBottomDistance](https://uniapp.dcloud.net.cn/collocation/pages#globalstyle)，比如设为50，那么滚动页面到距离底部50px时，就会触发onReachBottom事件。如使用scroll-view导致页面没有滚动，则触底事件不会被触发。

  11. onTabItemTap: 点击 tab 时触发，参数为Object，具体见下方注意事项 => 微信小程序、QQ小程序、支付宝小程序、百度小程序、H5、App、快手小程序、京东小程序

      * onTabItemTap常用于点击当前tabitem，滚动或刷新当前页面。如果是点击不同的tabitem，一定会触发页面切换。

      * 如果想在App端实现点击某个tabitem不跳转页面，不能使用onTabItemTap，可以使用[plus.nativeObj.view](http://www.html5plus.org/doc/zh_cn/nativeobj.html)放一个区块盖住原先的tabitem，并拦截点击事件。

      * 支付宝小程序平台onTabItemTap表现为点击非当前tabitem后触发，因此不能用于实现点击返回顶部这种操作

        ```javascript
        onTabItemTap : function(e) {
        	console.log(e);
        	// e的返回格式为json对象： {"index":0,"text":"首页","pagePath":"pages/index/index"}
        },
        ```
  
  12. onShareAppMessage: 用户点击右上角分享 => 微信小程序、QQ小程序、支付宝小程序、字节小程序、飞书小程序、快手小程序、京东小程序
  
  13. onPageScroll: 监听页面滚动，参数为Object => nvue暂不支持
  
      * 如果想实现滚动时标题栏透明渐变，在App和H5下，可在pages.json中配置titleNView下的type为transparent，[参考](https://uniapp.dcloud.io/collocation/pages?id=app-titlenview)。
  
      * 在App、微信小程序、H5中，也可以使用wxs监听滚动，[参考](https://uniapp.dcloud.io/tutorial/miniprogram-subject#wxs)；在app-nvue中，可以使用bindingx监听滚动，[参考](https://uniapp.dcloud.io/tutorial/nvue-api#nvue-里使用-bindingx)。
  
        ```javascript
        onPageScroll : function(e) { //nvue暂不支持滚动监听，可用bindingx代替
        	console.log("滚动距离为：" + e.scrollTop);
        },
        ```
  
        
  
  14. onNavigationBarButtonTap: 监听原生标题栏按钮点击事件，参数为Object => App、H5
  
      ```javascript
      onNavigationBarButtonTap : function (e) {
      	console.log(e);
      	// e的返回格式为json对象：{"text":"测试","index":0}
      }
      ```
  
  15. onBackPress: 监听页面返回，返回 event = {from:backbutton、 navigateBack} ，backbutton 表示来源是左上角返回按钮或 android 返回键；navigateBack表示来源是 uni.navigateBack ；详细说明及使用：[onBackPress 详解](http://ask.dcloud.net.cn/article/35120)。支付宝小程序只有真机能触发，只能监听非navigateBack引起的返回，不可阻止默认行为。 => app、H5、支付宝小程序
  
      * from: 触发返回行为的来源：'backbutton'——左上角导航栏按钮及安卓返回键；'navigateBack'——uni.navigateBack() 方法。**支付宝小程序端不支持返回此字段**
  
        ```javascript
        export default {
        	data() {
        		return {};
        	},
        	onBackPress(options) {
        		console.log('from:' + options.from)
        	}
        }
        ```
  
  16. onNavigationBarSearchInputChanged: 监听原生标题栏搜索输入框输入内容变化事件 => App、H5
  
  17. onNavigationBarSearchInputConfirmed: 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。 => App、H5
  
  18. onNavigationBarSearchInputClicked: 监听原生标题栏搜索输入框点击事件（pages.json 中的 searchInput 配置 disabled 为 true 时才会触发） => App、H5
  
  19. onShareTimeline: 监听用户点击右上角转发到朋友圈 => 微信小程序
  
  20. onAddToFavorites: 监听用户点击右上角收藏 => 微信小程序、QQ小程序
  

#### `2.2 (自定义)组件声明周期`

* 组件支持的生命周期，与vue标准组件的生命周期相同。
* beforeCreate: 在实例初始化之前被调用。
* created: 在实例创建完成后被立即调用。
* beforeMount: 在挂载开始之前被调用。
* mounted: 挂载到实例上去之后调用。[详见](https://v2.cn.vuejs.org/v2/api/#mounted) 注意：此处并不能确定子组件被全部挂载，如果需要子组件完全挂载之后在执行操作可以使用`$nextTick`[Vue官方文档](https://v2.cn.vuejs.org/v2/api/#vm-nextTick)
* beforeUpdate: 数据更新时调用，发生在虚拟 DOM 打补丁之前。
* updated: 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。[详见](https://v2.cn.vuejs.org/v2/api/#updated)
* beforeDestroy: 实例销毁之前调用。在这一步，实例仍然完全可用。[详见](https://v2.cn.vuejs.org/v2/api/#beforeDestroy)
* destroyed: Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。[详见](https://v2.cn.vuejs.org/v2/api/#destroyed)

#### `2.3 相关页面接口`

* `getApp()` 函数用于获取当前应用实例，一般用于获取globalData 。

  ```javascript
  const app = getApp()
  console.log(app.globalData)
  ```

  - 不要在定义于 `App()` 内的函数中，或调用 `App` 前调用 `getApp()` ，可以通过 `this.$scope` 获取对应的app实例
  - 当在首页`nvue`中使用`getApp()`不一定可以获取真正的`App`对象。对此提供了`const app = getApp({allowDefault: true})`用来获取原始的`App`对象，可以用来在首页对`globalData`等初始化

* `getCurrentPages()`用于获取当前页面栈的实例，以数组形式按栈的顺序给出，第一个元素为首页，最后一个元素为当前页面。

* 页面实例的方法属性列表

| 方法                  | 描述                          | 平台说明 |
| --------------------- | ----------------------------- | -------- |
| page.$getAppWebview() | 获取当前页面的webview对象实例 | App      |
| page.route            | 获取当前页面的路由            |          |

* `navigateTo`, `redirectTo` 只能打开非 tabBar 页面。

* `switchTab` 只能打开 `tabBar` 页面。

* 页面底部的 `tabBar` 由页面决定，即只要是定义为 `tabBar` 的页面，底部都有 `tabBar`。

* 不能在 `App.vue` 里面进行页面跳转。

* `$getAppWebview()`可以得到当前webview的对象实例，从而实现对 webview 更强大的控制。

  * 获取当前页面 webview 的对象实例

    ```javascript
    export default {
      data() {
        return {
          title: 'Hello'
        }
      },
      onLoad() {
        // #ifdef APP-PLUS
        const currentWebview = this.$scope.$getAppWebview(); //此对象相当于html5plus里的plus.webview.currentWebview()。在uni-app里vue页面直接使用plus.webview.currentWebview()无效
        currentWebview.setBounce({position:{top:'100px'},changeoffset:{top:'0px'}}); //动态重设bounce效果
        // #endif
      }
    }
    ```

  * 获取指定页面 webview 的对象实例

  ```javascript
  var pages = getCurrentPages();
  var page = pages[pages.length - 1];
  // #ifdef APP-PLUS
  var currentWebview = page.$getAppWebview();
  console.log(currentWebview.id);//获得当前webview的id
  console.log(currentWebview.isVisible());//查询当前webview是否可见
  );
  // #endif
  ```

* [nvue 开发与 vue 开发的常见区别](https://uniapp.dcloud.net.cn/tutorial/page.html#nvue-%E5%BC%80%E5%8F%91%E4%B8%8E-vue-%E5%BC%80%E5%8F%91%E7%9A%84%E5%B8%B8%E8%A7%81%E5%8C%BA%E5%88%AB)



### `3. 互相引用`

#### `3.1 引用组件`

* 传统vue项目开发，引用组件需要`导入 - 注册 - 使用`三个步骤

```vue
<template>
	<view>
		<!-- 3.使用组件 -->
		<uni-rate text="1"></uni-rate>
	</view>
</template>
<script>
	// 1. 导入组件
	import uniRate from '@/components/uni-rate/uni-rate.vue';
	export default {
		components: { uniRate } // 2. 注册组件
	}
</script>
```

* Vue 3.x增加了`script setup`特性，将三步优化为两步，无需注册步骤

```vue
<template>
	<view>
		<!-- 2.使用组件 -->
		<uni-rate text="1"></uni-rate>
	</view>
</template>
<script setup>
	// 1. 导入组件
	import uniRate from '@/components/uni-rate/uni-rate.vue';
</script>
```

* `uni-app`的[easycom](https://uniapp.dcloud.net.cn/collocation/pages.html#easycom)机制，将组件引用进一步优化，开发者只管使用，无需考虑导入和注册

```vue
<template>
	<view>
		<!-- 1.使用组件 -->
		<uni-rate text="1"></uni-rate>
	</view>
</template>
<script>
</script>
```

#### `3.2 引用js`

* `js`文件或`script`标签内（包括 renderjs 等）引入`js`文件时，可以使用相对路径和绝对路径

```js
// 绝对路径，@指向项目根目录，在cli项目中@指向src目录
import add from '@/common/add.js';
// 相对路径
import add from '../../common/add.js';
```

* js 文件不支持使用`/`开头的方式引入

#### `3.3 引用css`

* 使用`@import`语句可以导入外联样式表，`@import`后跟需要导入的外联样式表的相对路径，用`;`表示语句结束。

```css
<style>
    @import "../../common/uni.css";

    .uni-card {
        box-shadow: none;
    }
</style>
```

#### `3.4 引用静态资源`

* templat引入静态资源

  * `template`内引入静态资源，如`image`、`video`等标签的`src`属性时，可以使用相对路径或者绝对路径
  * `@`开头的绝对路径以及相对路径会经过 base64 转换规则校验
  * 引入的静态资源在非 h5 平台，均不转为 base64。
  * H5 平台，小于 4kb 的资源会被转换成 base64，其余不转。
  * 自`HBuilderX 2.6.6`起`template`内支持`@`开头路径引入静态资源，旧版本不支持此方式
  * App 平台自`HBuilderX 2.6.9`起`template`节点中引用静态资源文件时（如：图片），调整查找策略为【基于当前文件的路径搜索】，与其他平台保持一致
  * 支付宝小程序组件内 image 标签不可使用相对路径

  ```html
  <!-- 绝对路径，/static指根目录下的static目录，在cli项目中/static指src目录下的static目录 -->
  <image class="logo" src="/static/logo.png"></image>
  <image class="logo" src="@/static/logo.png"></image>
  <!-- 相对路径 -->
  <image class="logo" src="../../static/logo.png"></image>
  ```

* css 引入静态资源

  * `css`文件或`style标签`内引入`css`文件时（scss、less 文件同理），可以使用相对路径或绝对路径（`HBuilderX 2.6.6`）

  ```css
  /* 绝对路径 */
  @import url('/common/uni.css');
  @import url('@/common/uni.css');
  /* 相对路径 */
  @import url('../../common/uni.css');
  ```

  * `css`文件或`style标签`内引用的图片路径可以使用相对路径也可以使用绝对路径，需要注意的是，有些小程序端 css 文件不允许引用本地文件（请看注意事项）。
  * 引入字体图标请参考，[字体图标](https://uniapp.dcloud.net.cn/tutorial/syntax-css.html#字体图标)
  * `@`开头的绝对路径以及相对路径会经过 base64 转换规则校验
  * 不支持本地图片的平台，小于 40kb，一定会转 base64。（共四个平台 mp-weixin, mp-qq, mp-toutiao, app v2）
  * h5 平台，小于 4kb 会转 base64，超出 4kb 时不转。
  * 其余平台不会转 base64

  ```css
  /* 绝对路径 */
  background-image: url(/static/logo.png);
  background-image: url(@/static/logo.png);
  /* 相对路径 */
  background-image: url(../../static/logo.png);
  ```

#### [3.5 引用原生插件](https://uniapp.dcloud.net.cn/plugin/native-plugin.html)



### `4. js语法`

#### `4.1 ES6 支持`

* uni-app 在支持绝大部分 ES6 API 的同时，也支持了 ES7 的 await/async。各操作系统平台版本的支持情况，[请见](https://uniapp.dcloud.net.cn/tutorial/syntax-js.html)



### `5. CSS语法`

#### `5.1 尺寸单位`

* 支持的通用 css 单位包括 px、rpx
* vue 页面支持下面这些普通 H5 单位，但在 nvue 里不支持：
  * rem 根字体大小可以通过 [page-meta](https://uniapp.dcloud.net.cn/component/page-meta#page-meta) 配置
  * vh viewpoint height，视窗高度，1vh 等于视窗高度的 1%
  * vw viewpoint width，视窗宽度，1vw 等于视窗宽度的 1%
* rpx详细说明:

设计师在提供设计图时，一般只提供一个分辨率的图。严格按设计图标注的 px 做开发，在不同宽度的手机上界面很容易变形。而且主要是宽度变形。高度一般因为有滚动条，不容易出问题。由此，引发了较强的动态宽度单位需求。

微信小程序设计了 rpx 解决这个问题。`uni-app` 在 App 端、H5 端都支持了 `rpx`，并且可以配置不同屏幕宽度的计算方式，具体参考：[rpx 计算配置](https://uniapp.dcloud.io/collocation/pages?id=globalstyle)。rpx 是相对于基准宽度的单位，可以根据屏幕宽度进行自适应。`uni-app` 规定屏幕基准宽度 750rpx。

开发者可以通过设计稿基准宽度计算页面元素 rpx 值，设计稿 1px 与框架样式 1rpx 转换公式如下：

设计稿 1px / 设计稿基准宽度 = 框架样式 1rpx / 750rpx

换言之，页面元素宽度在 `uni-app` 中的宽度计算公式：

`750 * 元素在设计稿中的宽度 / 设计稿基准宽度`

* 若设计稿宽度为 750px，元素 A 在设计稿上的宽度为 100px，那么元素 A 在 `uni-app` 里面的宽度应该设为：`750 * 100 / 750`，结果为：100rpx。

* 若设计稿宽度为 640px，元素 A 在设计稿上的宽度为 100px，那么元素 A 在 `uni-app` 里面的宽度应该设为：`750 * 100 / 640`，结果为：117rpx。

* 若设计稿宽度为 375px，元素 B 在设计稿上的宽度为 200px，那么元素 B 在 `uni-app` 里面的宽度应该设为：`750 * 200 / 375`，结果为：400rpx。
* 注意 rpx 是和宽度相关的单位，屏幕越宽，该值实际像素越大。如不想根据屏幕宽度缩放，则应该使用 px 单位。
* 如果开发者在字体或高度中也使用了 rpx ，那么需注意这样的写法意味着随着屏幕变宽，字体会变大、高度会变大。如果你需要固定高度，则应该使用 px 。
* rpx 不支持动态横竖屏切换计算，使用 rpx 建议锁定屏幕方向
* 早期 uni-app 提供了 upx ，目前已经推荐统一改为 rpx 了，[详见](http://ask.dcloud.net.cn/article/36130)

#### `5.2 内联样式`

* 请尽量避免将静态的样式写进 style 中，以免影响渲染速度。

```html
<view :style="{color:color}" />
```

#### `5.3 选择器`

* 在 `uni-app` 中不能使用 `*` 选择器。
* 微信小程序自定义组件中仅支持 class 选择器
* `page` 相当于 `body` 节点

```css
<!-- 设置页面背景颜色，使用 scoped 会导致失效 -- > 
  page {
	background-color: #ccc;
}
```

#### `5.4 全局样式与局部样式`

* 定义在 App.vue 中的样式为全局样式，作用于每一个页面。在 pages 目录下 的 vue 文件中定义的样式为局部样式，只作用在对应的页面，并会覆盖 App.vue 中相同的选择器。

`5.5 CSS变量`

- 当设置 `"navigationStyle":"custom"` 取消原生导航栏后，由于窗体为沉浸式，占据了状态栏位置。此时可以使用一个高度为 `var(--status-bar-height)` 的 view 放在页面顶部，避免页面内容出现在状态栏。
- 由于在 H5 端，不存在原生导航栏和 tabbar，也是前端 div 模拟。如果设置了一个固定位置的居底 view，在小程序和 App 端是在 tabbar 上方，但在 H5 端会与 tabbar 重叠。此时可使用`--window-bottom`，不管在哪个端，都是固定在 tabbar 上方。
- 目前 nvue 在 App 端，还不支持 `--status-bar-height`变量，替代方案是在页面 onLoad 时通过 uni.getSystemInfoSync().statusBarHeight 获取状态栏高度，然后通过 style 绑定方式给占位 view 设定高度。下方提供了示例代码

| CSS 变量            | 描述                   | App                                                          | 小程序 | H5                   |
| :------------------ | :--------------------- | :----------------------------------------------------------- | :----- | :------------------- |
| --status-bar-height | 系统状态栏高度         | [系统状态栏高度](http://www.html5plus.org/doc/zh_cn/navigator.html#plus.navigator.getStatusbarHeight)、nvue 注意见下 | 25px   | 0                    |
| --window-top        | 内容区域距离顶部的距离 | 0                                                            | 0      | NavigationBar 的高度 |
| --window-bottom     | 内容区域距离底部的距离 | 0                                                            | 0      | TabBar 的高度        |

* 普通页面使用 css 变量

```vue
<template>
	<!-- HBuilderX 2.6.3+ 新增 page-meta, 详情：https://uniapp.dcloud.io/component/page-meta -->
	<page-meta>
		<navigation-bar />
	</page-meta>
	<view>
		<view class="status_bar">
			<!-- 这里是状态栏 -->
		</view>
		<view>状态栏下的文字</view>
	</view>
</template>
<style>
	.status_bar {
		height: var(--status-bar-height);
		width: 100%;
	}
</style>
```

* nvue 页面获取状态栏高度

```vue
<template>
	<view class="content">
		<view :style="{ height: iStatusBarHeight + 'px'}"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				iStatusBarHeight: 0,
			};
		},
		onLoad() {
			this.iStatusBarHeight = uni.getSystemInfoSync().statusBarHeight;
		},
	};
</script>
```

#### `5.5 uni-app 固定值组件`

| 组件          | 描述       | App                                                          | H5   |
| :------------ | :--------- | :----------------------------------------------------------- | :--- |
| NavigationBar | 导航栏     | 44px                                                         | 44px |
| TabBar        | 底部选项卡 | HBuilderX 2.3.4 之前为 56px，2.3.4 起和 H5 调为一致，统一为 50px。（但可以自主更改高度） | 50px |

#### `5.6 建议使用Flex布局`

* [阮一峰的 flex 教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

#### `5.7 背景图片`

* 支持 base64 格式图片。

* 支持网络路径图片。

* 小程序不支持在 css 中使用本地文件，包括本地的背景图和字体文件。需以 base64 方式方可使用。

* 使用本地路径背景图片需注意：

  1. 为方便开发者，在背景图片小于 40kb 时，`uni-app` 编译到不支持本地背景图的平台时，会自动将其转化为 base64 格式；
  2. 图片大于等于 40kb，会有性能问题，不建议使用太大的背景图，如开发者必须使用，则需自己将其转换为 base64 格式使用，或将其挪到服务器上，从网络地址引用。
  3. 本地背景图片的引用路径推荐使用以 ~@ 开头的绝对路径。

  ```css
  .test2 {
  	background-image: url('~@/static/logo.png');
  }
  ```

#### `5.8 字体图标`

* 引用方式

```css
@font-face {
	font-family: test1-icon;
	src: url('~@/static/iconfont.ttf');
}
```

* `nvue`中不可直接使用 css 的方式引入字体文件，需要使用以下方式在 js 内引入。

```vue
<template>
	<view>
		<view>
			<text class="test">&#xe600;</text>
			<text class="test">&#xe687;</text>
			<text class="test">&#xe60b;</text>
		</view>
	</view>
</template>
<style>
	@font-face {
		font-family: 'iconfont';
		src: url('https://at.alicdn.com/t/font_865816_17gjspmmrkti.ttf') format('truetype');
	}
	.test {
		font-family: iconfont;
		margin-left: 20rpx;
	}
</style>
```



### `6. VUE(2) 语法`

#### [6.1 基础](https://uniapp.dcloud.net.cn/tutorial/vue-basics.html)

* 事件映射表

```json
// 事件映射表，左侧为 WEB 事件，右侧为 ``uni-app`` 对应事件
{
    click: 'tap',
    touchstart: 'touchstart',
    touchmove: 'touchmove',
    touchcancel: 'touchcancel',
    touchend: 'touchend',
    tap: 'tap',
    longtap: 'longtap', //推荐使用longpress代替
    input: 'input',
    change: 'change',
    submit: 'submit',
    blur: 'blur',
    focus: 'focus',
    reset: 'reset',
    confirm: 'confirm',
    columnchange: 'columnchange',
    linechange: 'linechange',
    error: 'error',
    scrolltoupper: 'scrolltoupper',
    scrolltolower: 'scrolltolower',
    scroll: 'scroll'
}
```

#### `6.2 组件`

* 跟VUE基本一致

#### `6.3 API`

* 全局配置

| Vue 全局配置                     | 描述                                                         | H5   | App端 | 小程序 | 说明                                        |
| -------------------------------- | ------------------------------------------------------------ | ---- | ----- | ------ | ------------------------------------------- |
| Vue.config.silent                | 取消 Vue 所有的日志与警告 [详情](https://v2.cn.vuejs.org/v2/api/#silent) | √    | √     | √      |                                             |
| Vue.config.optionMergeStrategies | 自定义合并策略的选项 [详情](https://v2.cn.vuejs.org/v2/api/#optionMergeStrategies) | √    | √     | √      |                                             |
| Vue.config.devtools              | 配置是否允许 vue-devtools 检查代码 [详情](https://v2.cn.vuejs.org/v2/api/#devtools) | √    | x     | x      | 只在Web环境下支持                           |
| Vue.config.errorHandler          | 指定组件的渲染和观察期间未捕获错误的处理函数 [详情](https://v2.cn.vuejs.org/v2/api/#errorHandler) | √    | √     | √      |                                             |
| Vue.config.warnHandler           | 为 Vue 的运行时警告赋予一个自定义处理函数 [详情](https://v2.cn.vuejs.org/v2/api/#warnHandler) | √    | √     | √      |                                             |
| Vue.config.ignoredElements       | 须使 Vue 忽略在 Vue 之外的自定义元素 [详情](https://v2.cn.vuejs.org/v2/api/#ignoredElements) | √    | √     | √      | 强烈不推荐，会覆盖uni-app框架配置的内置组件 |
| Vue.config.keyCodes              | 给 v-on 自定义键位别名 [详情](https://v2.cn.vuejs.org/v2/api/#keyCodes) | √    | x     | x      |                                             |
| Vue.config.performance           | 设置为 true 以在浏览器开发工具的性能/时间线面板中启用对组件初始化、编译、渲染和打补丁的性能追踪 [详情](https://v2.cn.vuejs.org/v2/api/#performance) | √    | x     | x      | 只在Web环境下支持                           |
| Vue.config.productionTip         | 设置为 false 以阻止 vue 在启动时生成生产提示 [详情](https://v2.cn.vuejs.org/v2/api/#productionTip) | √    | √     | √      | -                                           |

* 全局API

| Vue 全局 API  | 描述                                                         | H5   | App端 | 小程序 | 说明                                 |
| ------------- | ------------------------------------------------------------ | ---- | ----- | ------ | ------------------------------------ |
| Vue.extend    | 使用基础 Vue 构造器，创建一个“子类” [详情](https://v2.cn.vuejs.org/v2/api/#Vue-extend) | √    | √     | x      | 不可作为组件使用                     |
| Vue.nextTick  | 在下次 DOM 更新循环结束之后执行延迟回调 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-nextTick) | √    | x     | x      |                                      |
| Vue.set       | 向响应式对象中添加一个 property，并确保这个新 property 同样是响应式的，且触发视图更新 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-set) | √    | √     | √      |                                      |
| Vue.delete    | 删除对象的 property。如果对象是响应式的，确保删除能触发更新视图 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-delete) | √    | √     | √      |                                      |
| Vue.directive | 注册或获取全局指令 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-directive) | √    | √     | x      |                                      |
| Vue.filter    | 注册或获取全局过滤器 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-filter) | √    | √     | x      |                                      |
| Vue.component | 注册或获取全局组件。注册还会自动使用给定的 id 设置组件的名称 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-component) | √    | √     | √      |                                      |
| Vue.use       | 安装 Vue.js 插件 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-use) | √    | √     | √      |                                      |
| Vue.mixin     | 全局注册一个混入，影响注册之后所有创建的每个 Vue 实例 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-mixin) | √    | √     | √      |                                      |
| Vue.version   | 提供字符串形式的 Vue 安装版本号 [详情](https://v2.cn.vuejs.org/v2/api/#Vue-version) | √    | √     | √      |                                      |
| Vue.compile   | 将一个模板字符串编译成 render 函数。只在完整版时可用。[详情](https://v2.cn.vuejs.org/v2/api/#Vue-compile) | √    | x     | x      | uni-app使用的vue是只包含运行时的版本 |

* 选项

| Vue 选项       | 描述                                                         | H5   | App端 | 小程序 | 说明                                 |
| -------------- | ------------------------------------------------------------ | ---- | ----- | ------ | ------------------------------------ |
| data           | Vue 实例的数据对象 [详情](https://v2.cn.vuejs.org/v2/api/#data) | √    | √     | √      |                                      |
| props          | props 可以是数组或对象，用于接收来自父组件的数据 [详情](https://v2.cn.vuejs.org/v2/api/#props) | √    | √     | √      |                                      |
| propsData      | 创建实例时传递 props。主要作用是方便测试 [详情](https://v2.cn.vuejs.org/v2/api/#propsData) | √    | √     | √      |                                      |
| computed       | 计算属性将被混入到 Vue 实例中 [详情](https://v2.cn.vuejs.org/v2/api/#computed) | √    | √     | √      |                                      |
| methods        | methods 将被混入到 Vue 实例中 [详情](https://v2.cn.vuejs.org/v2/api/#methods) | √    | √     | √      |                                      |
| watch          | 一个对象，键是需要观察的表达式，值是对应回调函数 [详情](https://v2.cn.vuejs.org/v2/api/#watch) | √    | √     | √      |                                      |
| el             | 提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标 [详情](https://v2.cn.vuejs.org/v2/api/#el) | √    | x     | x      |                                      |
| template       | 一个字符串模板作为 Vue 实例的标识使用 [详情](https://v2.cn.vuejs.org/v2/api/#template) | √    | x     | x      | uni-app使用的vue是只包含运行时的版本 |
| render         | 字符串模板的代替方案，该渲染函数接收一个 createElement 方法作为第一个参数用来创建 VNode。[详情](https://v2.cn.vuejs.org/v2/api/#render) | √    | x     | x      |                                      |
| renderError    | 当 render 函数遭遇错误时，提供另外一种渲染输出，只在开发者环境下工作 [详情](https://v2.cn.vuejs.org/v2/api/#renderError) | √    | x     | x      |                                      |
| directives     | 包含 Vue 实例可用指令的哈希表 [详情](https://v2.cn.vuejs.org/v2/api/#directives) | √    | √     | x      |                                      |
| filters        | 包含 Vue 实例可用过滤器的哈希表 [详情](https://v2.cn.vuejs.org/v2/api/#filters) | √    | √     | √      |                                      |
| components     | 包含 Vue 实例可用组件的哈希表 [详情](https://v2.cn.vuejs.org/v2/api/#components) | √    | √     | √      |                                      |
| parent         | 指定已创建的实例之父实例，在两者之间建立父子关系 [详情](https://v2.cn.vuejs.org/v2/api/#parent) | √    | √     | √      | 不推荐                               |
| mixins         | 选项接收一个混入对象的数组 [详情](https://v2.cn.vuejs.org/v2/api/#mixins) | √    | √     | √      |                                      |
| extends        | 允许声明扩展另一个组件 [详情](https://v2.cn.vuejs.org/v2/api/#extends) | √    | √     | √      |                                      |
| provide/inject | 允许一个祖先组件向其所有子孙后代注入一个依赖，不论组件层次有多深，并在其上下游关系成立的时间里始终生效 [详情](https://v2.cn.vuejs.org/v2/api/#provide-inject) | √    | √     | √      |                                      |
| name           | 允许组件模板递归地调用自身 [详情](https://v2.cn.vuejs.org/v2/api/#name) | √    | √     | √      |                                      |
| delimiters     | 改变纯文本插入分隔符 [详情](https://v2.cn.vuejs.org/v2/api/#delimiters) | √    | x     | x      |                                      |
| functional     | 使组件无状态 (没有 data) 和无实例 (没有 this 上下文) [详情](https://v2.cn.vuejs.org/v2/api/#functional) | √    | x     | x      |                                      |
| model          | 允许一个自定义组件在使用 v-model 时定制 prop 和 event [详情](https://v2.cn.vuejs.org/v2/api/#model) | √    | √     | x      |                                      |
| inheritAttrs   | inheritAttrs属性默认值为true，表示允许组件的根节点继承$attrs包含的属性 [详情](https://v2.cn.vuejs.org/v2/api/#inheritAttrs) | √    | √     | x      |                                      |
| comments       | 当设为 true 时，将会保留且渲染模板中的 HTML 注释 [详情](https://v2.cn.vuejs.org/v2/api/#comments) | √    | x     | x      | -                                    |

* 实例属性

| Vue 实例属性    | 描述                                                         | H5   | App端 | 小程序 | 说明                                                         |
| --------------- | ------------------------------------------------------------ | ---- | ----- | ------ | ------------------------------------------------------------ |
| vm.$data        | Vue 实例观察的数据对象 [详情](https://v2.cn.vuejs.org/v2/api/#vm-data) | √    | √     | √      |                                                              |
| vm.$props       | 当前组件接收到的 props 对象 [详情](https://v2.cn.vuejs.org/v2/api/#vm-props) | √    | √     | √      |                                                              |
| vm.$el          | Vue 实例使用的根 DOM 元素 [详情](https://v2.cn.vuejs.org/v2/api/#vm-el) | √    | x     | x      |                                                              |
| vm.$options     | 用于当前 Vue 实例的初始化选项 [详情](https://v2.cn.vuejs.org/v2/api/#vm-options) | √    | √     | √      |                                                              |
| vm.$parent      | 父实例，如果当前实例有的话 [详情](https://v2.cn.vuejs.org/v2/api/#vm-parent) | √    | √     | √      | H5端 `view`、`text` 等内置标签是以 Vue 组件方式实现，`$parent` 会获取这些到内置组件，导致的问题是 `this.$parent` 与其他平台不一致，解决方式是使用 `this.$parent.$parent` 获取或自定义组件根节点由 `view` 改为 `div` |
| vm.$root        | 当前组件树的根 Vue 实例 [详情](https://v2.cn.vuejs.org/v2/api/#vm-root) | √    | √     | √      |                                                              |
| vm.$children    | 当前实例的直接子组件 [详情](https://v2.cn.vuejs.org/v2/api/#vm-children) | √    | √     | √      | H5端 `view`、`text` 等内置标签是以 Vue 组件方式实现，`$children` 会获取到这些内置组件，导致的问题是 `this.$children` 与其他平台不一致，解决方式是使用 `this.$children.$children` 获取或自定义组件根节点由 `view` 改为 `div` |
| vm.$slots       | 用来访问被插槽分发的内容 [详情](https://v2.cn.vuejs.org/v2/api/#vm-slots) | √    | x     | √      |                                                              |
| vm.$scopedSlots | 用来访问作用域插槽 [详情](https://v2.cn.vuejs.org/v2/api/#vm-scopedSlots) | √    | √     | √      |                                                              |
| vm.$refs        | 一个对象，持有注册过 ref attribute 的所有 DOM 元素和组件实例[详情](https://v2.cn.vuejs.org/v2/api/#vm-refs) | √    | √     | √      | 非H5端只能用于获取自定义组件，不能用于获取内置组件实例（如：view、text） |
| vm.$isServer    | 当前 Vue 实例是否运行于服务器 [详情](https://v2.cn.vuejs.org/v2/api/#vm-isServer) | √    | √     | x      | App端总是返回false                                           |
| vm.$attrs       | 包含了父作用域中不作为 prop 被识别 (且获取) 的 attribute 绑定 [详情](https://v2.cn.vuejs.org/v2/api/#vm-attrs) | √    | √     | x      |                                                              |
| vm.$listeners   | 包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器 [详情](https://v2.cn.vuejs.org/v2/api/#vm-listeners) | √    | √     | x      | -                                                            |

* 实例方法

| 实例方法          | 描述                                                         | H5   | App端 | 小程序 | 说明 |
| ----------------- | ------------------------------------------------------------ | ---- | ----- | ------ | ---- |
| vm.$watch()       | 观察 Vue 实例上的一个表达式或者一个函数计算结果的变化 [详情](https://v2.cn.vuejs.org/v2/api/#vm-watch) | √    | √     | √      |      |
| vm.$set()         | 这是全局 Vue.set 的别名 [详情](https://v2.cn.vuejs.org/v2/api/#vm-set) | √    | √     | √      |      |
| vm.$delete()      | 这是全局 Vue.delete 的别名 [详情](https://v2.cn.vuejs.org/v2/api/#vm-delete) | √    | √     | √      |      |
| vm.$on()          | 监听当前实例上的自定义事件 [详情](https://v2.cn.vuejs.org/v2/api/#vm-on) | √    | √     | √      |      |
| vm.$once()        | 监听一个自定义事件，但是只触发一次 [详情](https://v2.cn.vuejs.org/v2/api/#vm-once) | √    | √     | √      |      |
| vm.$off()         | 移除自定义事件监听器 [详情](https://v2.cn.vuejs.org/v2/api/#vm-off) | √    | √     | √      |      |
| vm.$emit()        | 触发当前实例上的事件 [详情](https://v2.cn.vuejs.org/v2/api/#vm-emit) | √    | √     | √      |      |
| vm.$mount()       | 手动地挂载一个未挂载的实例 [详情](https://v2.cn.vuejs.org/v2/api/#vm-mount) | √    | x     | x      |      |
| vm.$forceUpdate() | 迫使 Vue 实例重新渲染 [详情](https://v2.cn.vuejs.org/v2/api/#vm-forceUpdate) | √    | √     | √      |      |
| vm.$nextTick()    | 将回调延迟到下次 DOM 更新循环之后执行 [详情](https://v2.cn.vuejs.org/v2/api/#vm-nextTick) | √    | √     | √      |      |
| vm.$destroy()     | 完全销毁一个实例 [详情](https://v2.cn.vuejs.org/v2/api/#vm-destroy) | √    | √     | √      | -    |

* 模板指令

| Vue 指令  | 描述                                                         | H5   | App端 | 小程序 | 说明                           |
| --------- | ------------------------------------------------------------ | ---- | ----- | ------ | ------------------------------ |
| v-text    | 更新元素的 textContent [详情](https://v2.cn.vuejs.org/v2/api/#v-text) | √    | √     | √      |                                |
| v-html    | 更新元素的 innerHTML [详情](https://v2.cn.vuejs.org/v2/api/#v-html) | √    | √     | x      | 微信小程序会被转成 `rich-text` |
| v-show    | 根据表达式之真假值，切换元素的 display CSS属性 [详情](https://v2.cn.vuejs.org/v2/api/#v-show) | √    | √     | √      |                                |
| v-if      | 根据表达式的值的 truthiness 来有条件地渲染元素 [详情](https://v2.cn.vuejs.org/v2/api/#v-if) | √    | √     | √      |                                |
| v-else    | 为 v-if 或者 v-else-if 添加“else 块” [详情](https://v2.cn.vuejs.org/v2/api/#v-else) | √    | √     | √      |                                |
| v-else-if | 表示 v-if 的“else if 块”。可以链式调用 [详情](https://v2.cn.vuejs.org/v2/api/#v-else-if) | √    | √     | √      |                                |
| v-for     | 基于源数据多次渲染元素或模板块 [详情](https://v2.cn.vuejs.org/v2/api/#v-for) | √    | √     | √      |                                |
| v-on      | 绑定事件监听器 [详情](https://v2.cn.vuejs.org/v2/api/#v-on)  | √    | √     | √      |                                |
| v-bind    | 动态地绑定一个或多个 attribute，或一个组件 prop 到表达式 [详情](https://v2.cn.vuejs.org/v2/api/#v-bind) | √    | √     | √      |                                |
| v-model   | 在表单控件或者组件上创建双向绑定 [详情](https://v2.cn.vuejs.org/v2/api/#v-model) | √    | √     | √      |                                |
| v-pre     | 跳过这个元素和它的子元素的编译过程 [详情](https://v2.cn.vuejs.org/v2/api/#v-pre) | √    | √     | x      |                                |
| v-cloak   | 这个指令保持在元素上直到关联实例结束编译 [详情](https://v2.cn.vuejs.org/v2/api/#v-cloak) | √    | x     | x      |                                |
| v-once    | 只渲染元素和组件一次 [详情](https://v2.cn.vuejs.org/v2/api/#v-once) | √    | √     | x      | -                              |

* 特殊属性

| 特殊属性 | 描述                                                         | H5   | App端                  | 小程序 | 说明                                                  |
| -------- | ------------------------------------------------------------ | ---- | ---------------------- | ------ | ----------------------------------------------------- |
| key      | 主要用在 Vue 的虚拟 DOM 算法，在新旧 nodes 对比时辨识 VNodes [详情](https://v2.cn.vuejs.org/v2/api/#key) | √    | √                      | √      |                                                       |
| ref      | ref 被用来给元素或子组件注册引用信息 [详情](https://v2.cn.vuejs.org/v2/api/#ref) | √    | √                      | √      | 非 H5 平台只能获取 vue 组件实例不能获取到内置组件实例 |
| is       | 用于动态组件且基于 DOM 内模板的限制来工作 [详情](https://v2.cn.vuejs.org/v2/api/#is) | √    | √ (需传入 String 类型) | x      | -                                                     |

* 内置组件

| 内置组件         | 描述                                                         | H5   | App端 | 小程序 | 说明 |
| ---------------- | ------------------------------------------------------------ | ---- | ----- | ------ | ---- |
| component        | 渲染一个“元组件”为动态组件。依 is 的值，来决定哪个组件被渲染 [详情](https://v2.cn.vuejs.org/v2/api/#component) | √    | √     | x      |      |
| transition       | 作为单个元素/组件的过渡效果 [详情](https://v2.cn.vuejs.org/v2/api/#transition) | √    | x     | x      |      |
| transition-group | 作为多个元素/组件的过渡效果 [详情](https://v2.cn.vuejs.org/v2/api/#transition-group) | √    | x     | x      |      |
| keep-alive       | 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们 [详情](https://v2.cn.vuejs.org/v2/api/#keep-alive) | √    | x     | x      |      |
| slot             | 作为组件模板之中的内容分发插槽 [详情](https://v2.cn.vuejs.org/v2/api/#slot) | √    | √     | √      | -    |
| template         | 并不是一个组件，它仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性 [详情](https://uniapp.dcloud.io/component/vue-component?id=template) | √    | √     | √      | -    |



### `7. VUEX`

用法基本与H5一致, [可见](https://uniapp.dcloud.net.cn/tutorial/vue-vuex.html)



### `8. 组合式 API`

暂时不用, [可见](https://uniapp.dcloud.net.cn/tutorial/vue-composition-api.html)



### `9. TypeScript专题`

暂时不用, [可见](https://uniapp.dcloud.net.cn/tutorial/typescript-subject.html)



### `10. 条件编译`

#### `10.1 以 #ifdef 或 #ifndef 加 **%PLATFORM%** 开头，以 #endif 结尾`

* `#ifdef`：if defined 仅在某平台存在

* `#ifndef`：if not defined 除了某平台均存在

* `%PLATFORM%` 可取值

| 值                      | 生效条件                                                     |
| :---------------------- | :----------------------------------------------------------- |
| VUE3                    | HBuilderX 3.2.0+ [详情](https://ask.dcloud.net.cn/article/37834) |
| APP-PLUS                | App                                                          |
| APP-PLUS-NVUE或APP-NVUE | App nvue 页面                                                |
| APP-ANDROID             | App Android 平台 仅限 uts文件                                |
| APP-IOS                 | App iOS 平台 仅限 uts文件                                    |
| H5                      | H5                                                           |
| MP-WEIXIN               | 微信小程序                                                   |
| MP-ALIPAY               | 支付宝小程序                                                 |
| MP-BAIDU                | 百度小程序                                                   |
| MP-TOUTIAO              | 字节跳动小程序                                               |
| MP-LARK                 | 飞书小程序                                                   |
| MP-QQ                   | QQ小程序                                                     |
| MP-KUAISHOU             | 快手小程序                                                   |
| MP-JD                   | 京东小程序                                                   |
| MP-360                  | 360小程序                                                    |
| MP                      | 微信小程序/支付宝小程序/百度小程序/字节跳动小程序/飞书小程序/QQ小程序/360小程序 |
| QUICKAPP-WEBVIEW        | 快应用通用(包含联盟、华为)                                   |
| QUICKAPP-WEBVIEW-UNION  | 快应用联盟                                                   |
| QUICKAPP-WEBVIEW-HUAWEI | 快应用华为                                                   |

#### `10.2 API的条件编译`

```javascript
// #ifdef  %PLATFORM%
平台特有的API实现
// #endif
```

#### `10.3 组件的条件编译`

```html
<!--  #ifdef  %PLATFORM% -->
平台特有的组件
<!--  #endif -->

<view>
    <view>微信公众号关注组件</view>
    <view>
        <!-- uni-app未封装，但可直接使用微信原生的official-account组件-->
        <!-- #ifdef MP-WEIXIN -->
		        <official-account></official-account>
		    <!-- #endif -->
    </view>
</view>
```

#### `10.4 样式的条件编译`

```css
/*  #ifdef  %PLATFORM%  */
平台特有样式
/*  #endif  */
```

#### `10.5 pages.json的条件编译`

![img](https://web-assets.dcloud.net.cn/unidoc/zh/platform-4.png)

#### `10.6 static目录的条件编译`

* 在不同平台，引用的静态资源可能也存在差异，通过 static 的条件编译可以解决此问题，static 目录下新建不同平台的专有目录，专有目录下的静态资源只有在特定平台才会编译进去。

|  目录名称   |     说明     |
| :---------: | :----------: |
|  app-plus   |     App      |
|     h5      |      H5      |
|  mp-weixin  |  微信小程序  |
|  mp-alipay  | 支付宝小程序 |
|  mp-baidu   |  百度小程序  |
|    mp-qq    |   QQ小程序   |
| mp-toutiao  |  字节小程序  |
|   mp-lark   |  飞书小程序  |
| mp-kuaishou |  快手小程序  |
|    mp-jd    |  京东小程序  |



### `11. APP专题`

#### `11.1 NVUE`

* `适用场景:`

  * 需要高性能的区域长列表或瀑布流滚动。webview 的页面级长列表滚动是没有性能问题的（就是滚动条覆盖 webview 整体高度），但页面中某个区域做长列表滚动，则需要使用 nvue 的`list`、`recycle-list`、`waterfall`等组件([详见](https://uniapp.dcloud.io/component/list))。这些组件的性能要高于 vue 页面里的区域滚动组件`scroll-view`。
  * 复杂高性能的自定义下拉刷新。uni-app 的 pages.json 里可以配置原生下拉刷新，但引擎内置的下拉刷新样式只有雪花和 circle 圈 2 种样式。如果你需要自己做复杂的下拉刷新，推荐使用 nvue 的 refresh 组件。当然[插件市场](https://ext.dcloud.net.cn/search?q=下拉刷新)里也有很多 vue 下的自定义下拉刷新插件，只要是基于 renderjs 或 wxs 的，性能也可以商用，只是没有 nvue 的`refresh`组件更极致。
  * 左右拖动的长列表。在 webview 里，通过`swiper`+`scroll-view`实现左右拖动的长列表，前端模拟下拉刷新，这套方案的性能不好。此时推荐使用 nvue，比如新建 uni-app 项目时的[新闻示例模板](https://ext.dcloud.net.cn/plugin?id=103)，就采用了 nvue，切换很流畅。
  * 实现区域滚动长列表+左右拖动列表+吸顶的复杂排版效果，效果可参考 hello uni-app 模板里的`swiper-list`。[详见](https://ext.dcloud.net.cn/plugin?id=2128)
  * 如需要将软键盘右下角按钮文字改为“发送”，则需要使用 nvue。比如聊天场景，除了软键盘右下角的按钮文字处理外，还涉及聊天记录区域长列表滚动，适合 nvue 来做。
  * 解决前端控件无法覆盖原生控件的层级问题。当你使用`map`、`video`、`live-pusher`等原生组件时，会发现前端写的`view`等组件无法覆盖原生组件，层级问题处理比较麻烦，此时使用 nvue 更好。或者在 vue 页面上也可以覆盖一个 subnvue（一种非全屏的 nvue 页面覆盖在 webview 上），以解决 App 上的原生控件层级问题。[详见](https://uniapp.dcloud.io/component/native-component)
  * 如深度使用`map`组件，建议使用 nvue。除了层级问题，App 端 nvue 文件的 map 功能更完善，和小程序拉齐度更高，多端一致性更好。
  * 如深度使用`video`，建议使用 nvue。比如如下 2 个场景：video 内嵌到 swiper 中，以实现抖音式视频滑动切换，例子见[插件市场](https://ext.dcloud.net.cn/search?q=仿抖音)；nvue 的视频全屏后，通过`cover-view`实现内容覆盖，比如增加文字标题、分享按钮。
  * 直播推流：nvue 下有`live-pusher`组件，和小程序对齐，功能更完善，也没有层级问题。
  * 对 App 启动速度要求极致化。App 端如果首页使用 nvue 且在 manifest 里配置 fast 模式，那么 App 的启动速度可以控制在 1 秒左右。而使用 vue 页面的话，App 的启动速度一般是 3 秒起，取决于你的代码性能和体积。

  但注意，在某些场景下，nvue 不如 vue 页面，如下：

  1. `canvas`。nvue 的 canvas 性能不高，尤其是 Android App 平台，所以这个组件干脆没有内置，而是需要单独引入。操作 canvas 动画，最高性能的方式是使用 vue 页面的 renderjs 技术，在 hello uni-app 里的 canvas 示例就是如此。
  2. 动态横竖屏。nvue 页面的 css 不支持媒体查询，所以横竖屏动态切换、动态适配屏幕是很困难的。

* `nvue开发与vue开发的常见区别`
  * nvue 页面控制显隐只可以使用`v-if`不可以使用`v-show`
  * nvue 页面只能使用`flex`布局，不支持其他布局方式。页面开发前，首先想清楚这个页面的纵向内容有什么，哪些是要滚动的，然后每个纵向内容的横轴排布有什么，按 flex 布局设计好界面。
  * nvue 页面的布局排列方向默认为竖排（`column`），如需改变布局方向，可以在 `manifest.json` -> `app-plus` -> `nvue` -> `flex-direction` 节点下修改，仅在 uni-app 模式下生效。[详情](https://uniapp.dcloud.io/collocation/manifest?id=nvue)。
  * nvue页面编译为H5、小程序时，会做一件css默认值对齐的工作。因为weex渲染引擎只支持flex，并且默认flex方向是垂直。而H5和小程序端，使用web渲染，默认不是flex，并且设置`display:flex`后，它的flex方向默认是水平而不是垂直的。所以nvue编译为H5、小程序时，会自动把页面默认布局设为flex、方向为垂直。当然开发者手动设置后会覆盖默认设置。
  * 文字内容，必须、只能在`<text>`组件下。不能在`<div>`、`<view>`的`text`区域里直接写文字。否则即使渲染了，也无法绑定js里的变量。
  * 只有`text`标签可以设置字体大小，字体颜色。
  * 布局不能使用百分比、没有媒体查询。
  * nvue 切换横竖屏时可能导致样式出现问题，建议有 nvue 的页面锁定手机方向。
  * 支持的css有限，不过并不影响布局出你需要的界面，`flex`还是非常强大的。[详见](https://uniapp.dcloud.net.cn/nvue-css#flex)
  * 不支持背景图。但可以使用`image`组件和层级来实现类似web中的背景效果。因为原生开发本身也没有web这种背景图概念
  * css选择器支持的比较少，只能使用 class 选择器。[详见](https://uniapp.dcloud.net.cn/nvue-css)
  * nvue 的各组件在安卓端默认是透明的，如果不设置`background-color`，可能会导致出现重影的问题。
  * `class` 进行绑定时只支持数组语法。
  * Android端在一个页面内使用大量圆角边框会造成性能问题，尤其是多个角的样式还不一样的话更耗费性能。应避免这类使用。
  * nvue页面没有`bounce`回弹效果，只有几个列表组件有`bounce`效果，包括 `list`、`recycle-list`、`waterfall`。
  * 原生开发没有页面滚动的概念，页面内容高过屏幕高度并不会自动滚动，只有部分组件可滚动（`list`、`waterfall`、`scroll-view/scroller`），要滚的内容需要套在可滚动组件下。这不符合前端开发的习惯，所以在 nvue 编译为 uni-app模式时，给页面外层自动套了一个 `scroller`，页面内容过高会自动滚动。（组件不会套，页面有`recycle-list`时也不会套）。后续会提供配置，可以设置不自动套。
  * 在 App.vue 中定义的全局js变量不会在 nvue 页面生效。`globalData`和`vuex`是生效的。
  * App.vue 中定义的全局css，对nvue和vue页面同时生效。如果全局css中有些css在nvue下不支持，编译时控制台会报警，建议把这些不支持的css包裹在[条件编译](https://uniapp.dcloud.io/platform)里，`APP-PLUS-NVUE`
  * 不能在 `style` 中引入字体文件，nvue 中字体图标的使用参考：[加载自定义字体](https://uniapp.dcloud.net.cn/nvue-api#addrule)。如果是本地字体，可以用`plus.io`的API转换路径。
  * 目前不支持在 nvue 页面使用 `typescript/ts`。
  * nvue 页面关闭原生导航栏时，想要模拟状态栏，可以[参考文章](https://ask.dcloud.net.cn/article/35111)。但是，仍然强烈建议在nvue页面使用原生导航栏。nvue的渲染速度再快，也没有原生导航栏快。原生排版引擎解析`json`绘制原生导航栏耗时很少，而解析nvue的js绘制整个页面的耗时要大的多，尤其在新页面进入动画期间，对于复杂页面，没有原生导航栏会在动画期间产生整个屏幕的白屏或闪屏。

* `样式`
  * nvue的css**仅支持flex布局**，是webview的css语法的子集。这是因为操作系统原生排版不支持非flex之外的web布局。当然flex足以排布出各种页面，只是写法需要适应。
  * class 进行绑定时只支持数组语法。
  * 不支持媒体查询
  * 不能在 style 中引入字体文件
  * 不能使用百分比布局，如`width：100%`
  * 不支持在css里写背景图`background-image`，但可以使用image组件和层级来实现类似web中的背景效果。因为原生开发本身也没有web这种背景图概念
  * 使用`image`标签，支持使用base64，不支持svg格式图片
  * nvue 的各组件在安卓端默认是透明的，如果不设置`background-color`，可能会导致出现重影的问题
  * 文字内容，必须只能在`text`组件下，`text`组件不能换行写内容，否则会出现无法去除的周边空白
  * 只有`text`标签可以设置字体大小，字体颜色
  * 不支持 `/deep/`
  * [NVUE支持的样式](https://uniapp.dcloud.net.cn/tutorial/nvue-css.html)
    * width, height, padding, border, margin, flex, position, transition, transform, 伪类(active, focus, disabled, enabled), 渐变(linear-gradient), box-shadow, color, font-size, font-style, font-weight, text-decoration, text-align, font-family, text-overflow, lines, line-height, word-wrap

* `API`

  * `uni.requireNativePlugin`

    * 引入 App 原生插件

    ```js
    //使用方式
    const PluginName = uni.requireNativePlugin(PluginName); // PluginName 为原生插件名称
    ```

  * `DOM.addRule(type, contentObject)`

    * Weex 提供 DOM.addRule 以**加载自定义字体**。开发者可以通过指定 font-family加载 iconfont 和 custom font。

    ```vue
    <template>
    		<view>
    			<text class="my-iconfont">&#xe85c;</text>	
    		</view>
    	</template>
    	<script>
    		export default{
    			beforeCreate() {
    				const domModule = uni.requireNativePlugin('dom')
    				domModule.addRule('fontFace', {
    					'fontFamily': "myIconfont",
    					'src': "url('http://at.alicdn.com/t/font_2234252_v3hj1klw6k9.ttf')"
    				});
    			}
    		}
    	</script>
    	<style>
    		.my-iconfont {
    			font-family:myIconfont;
    			font-size:60rpx;
    			color: #00AAFF;
    		}
    	</style>
    ```

  * `scrollToElement(ref, options)`
  
    * @ref，要滚动到的那个节点。
    * @options
      - offset，一个到其可见位置的偏移距离，默认是 0。
      - animated，是否需要附带滚动动画，默认是 true。
  
    ```vue
      <template>
        <view class="wrapper">
          <scroller class="scroller">
            <view class="row" v-for="(name, index) in rows" :ref="'item'+index">
              <text class="text" :ref="'text'+index">{{name}}</text>
            </view>
          </scroller>
          <view class="group">
            <text @click="goto10" class="button">Go to 10</text>
            <text @click="goto20" class="button">Go to 20</text>
          </view>
        </view>
      </template>
      <script>
        const dom = uni.requireNativePlugin('dom')
        export default {
          data() {
            return {
              rows: []
            }
          },
          created() {
            for (let i = 0; i < 30; i++) {
              this.rows.push('row ' + i)
            }
          },
          methods: {
            goto10(count) {
              const el = this.$refs.item10[0]
              dom.scrollToElement(el, {})
            },
            goto20(count) {
              const el = this.$refs.item20[0]
              dom.scrollToElement(el, {
                offset: 0
              })
            }
          }
        }
      </script>
    ```
  
  * `getComponentRect(ref, callback)`
  
    * @ref，要获取外框的那个节点。
  
    * @callback，异步方法，通过回调返回信息。
  
      * 回调方法中的数据样例
  
      ```json
       {
          result: true,
          size: {
              bottom: 60,
              height: 15,
              left: 0,
              right: 353,
              top: 45,
              width: 353
          }
        }
      ```
  
  * `animation`
  
    ```vue
    <template>
        <view class="box">
          <view ref="test" @click="move" class="box-item"></view>
        </view>
      </template>
      <script>
          const animation = uni.requireNativePlugin('animation')
          export default {
              methods: {
                  move() {
                      var testEl = this.$refs.test;
                      animation.transition(testEl, {
                          styles: {
                              backgroundColor: '#007AFF',
                              transform: 'translate(100px, 80px)',
                              transformOrigin: 'center center'
                          },
                          duration: 800, //ms
                          timingFunction: 'ease',
                          delay: 0 //ms
                      },()=>{
                          uni.showToast({
                              title: 'finished',
                              icon:'none'
                          });
                      })
                  }
              }
          }
      </script>
      <style scoped>
        .box{
            width:750rpx;
            height:750rpx;
        }
        .box-item{
          width: 250rpx;
          height: 250rpx;
          background-color: #00aaff;
        }
      </style>
    ```
  
  * [transition](https://uniapp.dcloud.net.cn/tutorial/nvue-api.html#transition)
  
  * [BindingX](https://uniapp.dcloud.net.cn/tutorial/nvue-api.html#bindingx)
  
  * `nvue 和 vue 相互通讯`
  
    * 使用 `uni.$on` , `uni.$emit` 的方式进行页面通讯
  
    ```js
    	// 接收信息的页面
    	// $on(eventName, callback)  
    	uni.$on('page-popup', (data) => {  
    	    console.log('标题：' + data.title)
    	    console.log('内容：' + data.content)
    	})  
    	
    	// 发送信息的页面
    	// $emit(eventName, data)  
    	uni.$emit('page-popup', {  
    	    title: '我是title',  
    	    content: '我是content'  
    	});
    ```
  
  * `vue 和 nvue 共享的变量和数据`
  
    * `vuex`
  
    * `uni.storage`
  
    * `globalData`
  
  * `使用 HTML5Plus API`
  
    * nvue页面可直接使用plus的API，并且不需要等待plus ready。
  
  * `nvue 里不支持的 uni-app API`
  
    * 不支持的 API
  
    | API                   | 说明             | 解决方案                                                     |
    | --------------------- | ---------------- | ------------------------------------------------------------ |
    | uni.createAnimation() | 创建一个动画实例 | [animation](https://uniapp.dcloud.net.cn/tutorial/nvue-api#animation) |
  
    | API                | 说明                 | 解决方案                                                     |
    | ------------------ | -------------------- | ------------------------------------------------------------ |
    | uni.pageScrollTo() | 将页面滚动到目标位置 | [scrollToElement](https://uniapp.dcloud.net.cn/tutorial/nvue-api.html#scrolltoelement) |
  
    | API                              | 说明                                         |
    | -------------------------------- | -------------------------------------------- |
    | uni.createIntersectionObserver() | 创建并返回一个 IntersectionObserver 对象实例 |

* [事件](https://uniapp.dcloud.net.cn/tutorial/nvue-event.html)

  用到再看。

#### `11.2 html5plus`

* [h5+ API](https://www.html5plus.org/doc/zh_cn/accelerometer.html)

* #### 在html中使用plus的api，需要等待plus ready。 而`uni-app`不需要等，可以直接使用。而且如果你调用plus ready，反而不会触发。

* 在普通的 H5+ 项目中，需要使用 `document.addEventListener` 监听原生扩展的事件。`uni-app` 中，没有 document。可以使用 `plus.globalEvent.addEventListener` 来实现。

```js
// #ifdef APP-PLUS
// 监听新意图事件
plus.globalEvent.addEventListener('newintent', function(){});
// #endif
```

#### [11.3 native-js](https://uniapp.dcloud.net.cn/tutorial/native-js.html)

用到再看。

#### [11.4 renderjs](https://uniapp.dcloud.net.cn/tutorial/renderjs.html)

用到再看。

#### [11.5 原生插件开发](https://nativesupport.dcloud.net.cn/NativePlugin/#)

用到再看。

#### [11.6 User Agent](https://uniapp.dcloud.net.cn/tutorial/app-useragent.html)

* 默认情况使用系统Webview的User Agent，并添加Html5Plus/1.0、uni-app两字段

#### [11.7 使用高斯模糊](https://uniapp.dcloud.net.cn/tutorial/app-blureffect.html)

用到再看。

[11.8 APP打包配置](https://uniapp.dcloud.net.cn/tutorial/app-base.html)

用到再看。

#### [11.9 uni-app 全局变量的几种实现方式](https://ask.dcloud.net.cn/article/35021)

* `公用模块 (不推荐)`

  * 这种方式只支持多个vue页面或多个nvue页面之间公用，vue和nvue之间不公用。

* `挂载 Vue.prototype (不推荐)`

  * 将一些使用频率较高的常量或者方法，直接扩展到 Vue.prototype 上，每个 Vue 对象都会“继承”下来。这种方式只支持vue页面。

* `globalData (推荐, 可是变量不是响应式)`

  * 在 App.vue 可以定义 globalData ，也可以使用 API 读写这个值。支持vue和nvue共享数据。

  ```js
  App.vue
  <script>  
      export default {  
          globalData: {  
              text: 'text'  
          },  
          onLaunch: function() {  
              console.log('App Launch')  
          },  
          onShow: function() {  
              console.log('App Show')  
          },  
          onHide: function() {  
              console.log('App Hide')  
          }  
      }  
  </script>  
  
  <style>  
      /*每个页面公共css */  
  </style>
  
  
  //js中操作globalData的方式如下:
  //赋值
  getApp().globalData.text = 'test'
  //取值
  console.log(getApp().globalData.text) // 'test'
  ```

* `VUEX (最推荐, 变量是响应式)`



### `12. 性能优化`

#### `12.1 避免使用大图`

#### `12.2 优化数据更新`

* 在 `uni-app` 中，定义在 data 里面的数据每次变化时都会通知视图层重新渲染页面。所以如果不是视图所需要的变量，可以不定义在 data 中，可在外部定义变量或直接挂载在vue实例上，以避免造成资源浪费。

#### `12.3 减少一次性渲染的节点数量`

* 页面初始化时，逻辑层如果一次性向视图层传递很大的数据，使视图层一次性渲染大量节点，可能造成通讯变慢、页面切换卡顿，所以建议以局部更新页面的方式渲染页面。如：服务端返回100条数据，可进行分批加载，一次加载50条，500ms 后进行下一次加载。

#### `12.4 减少组件数量、减少节点嵌套层级`

* 深层嵌套的节点在页面初始化构建时往往需要更多的内存占用，并且在遍历节点时也会更慢些，所以建议减少深层的节点嵌套。

#### `12.5 避免视图层和逻辑层频繁进行通讯`

- 减少 scroll-view 组件的 scroll 事件监听，当监听 scroll-view 的滚动事件时，视图层会频繁的向逻辑层发送数据；
- 监听 scroll-view 组件的滚动事件时，不要实时的改变 scroll-top/scroll-left 属性，因为监听滚动时，视图层向逻辑层通讯，改变 scroll-top/scroll-left 时，逻辑层又向视图层通讯，这样就可能造成通讯卡顿。
- 注意 onPageScroll 的使用，onPageScroll 进行监听时，视图层会频繁的向逻辑层发送数据；
- 多使用css动画，而不是通过js的定时器操作界面做动画
- 如需在canvas里做跟手操作，app端建议使用renderjs，小程序端建议使用web-view组件。web-view里的页面没有逻辑层和视图层分离的概念，自然也不会有通信折损。

#### `12.6 优化页面切换动画`

- 页面初始化时若存在大量图片或原生组件渲染和大量数据通讯，会发生新页面渲染和窗体进入动画抢资源，造成页面切换卡顿、掉帧。建议延时100ms~300ms渲染图片或复杂原生组件，分批进行数据通讯，以减少一次性渲染的节点数量。
- App端动画效果可以自定义。popin/popout的双窗体联动挤压动画效果对资源的消耗更大，如果动画期间页面里在执行耗时的js，可能会造成动画掉帧。此时可以使用消耗资源更小的动画效果，比如slide-in-right/slide-out-right。
- App-nvue和H5，还支持页面预载，[uni.preloadPage](https://uniapp.dcloud.io/api/preload-page)，可以提供更好的使用体验

#### `12.7 优化背景色闪白`

- 如果页面背景是深色，在vue页面中可能会发生新窗体刚开始动画时是灰白色背景，动画结束时才变为深色背景，造成闪屏。这是因为webview的背景生效太慢的问题。此时需将样式写在 `App.vue` 里，可以加速页面样式渲染速度。`App.vue` 里面的样式是全局样式，每次新开页面会优先加载 `App.vue` 里面的样式，然后加载普通 vue 页面的样式。
- app端还可以在pages.json的页面的style里单独配置页面原生背景色，比如在globalStyle->style->app-plus->background下配置全局背景色
- 另外nvue页面不存在此问题，也可以更改为nvue页面。

#### `12.8 使用nvue代替vue`

* 在 App 端 `uni-app` 的 nvue 页面可是基于weex升级改造的原生渲染引擎，实现了页面原生渲染能力、提高了页面流畅性。若对页面性能要求较高可以使用此方式开发，详见：[nvue](https://uniapp.dcloud.net.cn/tutorial/nvue-outline)。

#### `12.9 优化启动速度`

* 工程代码越多，包括背景图和本地字体文件越大，对小程序启动速度有影响，应注意控制体积。组件引用的前景图不影响性能。
* App端的 splash 关闭有白屏检测机制，如果首页一直白屏或首页本身就是一个空的中转页面，可能会造成 splash 10秒才关闭，可参考此文解决https://ask.dcloud.net.cn/article/35565
* App端，首页为nvue页面时，并设置为[fast启动模式](https://ask.dcloud.net.cn/article/36749)，此时App启动速度最快。
* App设置为纯nvue项目（manifest里设置app-plus下的renderer:"native"），这种项目的启动速度更快，2秒即可完成启动。因为它整个应用都使用原生渲染，不加载基于webview的那套框架。

#### `12.10 优化包体积`

- uni-app发行到小程序时，自带引擎只有几十K，主要是一个定制过的vue.js核心库。如果使用了es6转es5、css对齐的功能，可能会增大代码体积，可以配置这些编译功能是否开启。
- uni-app的H5端，自带了vue.js、vue-router及部分es6 polyfill库，这部分的体积gzip后只有92k，和web开发使用vue基本一致。而内置组件ui库（如picker、switch等）、小程序的对齐js api等，相当于一个完善的大型ui库。但大多数应用不会用到所有内置组件和API。由此uni-app提供了摇树优化机制，未摇树优化前的uni-app整体包体积约500k，服务器部署gzip后162k。开启摇树优化需在manifest配置，[详情](https://uniapp.dcloud.io/collocation/manifest?id=optimization)。
- uni-app的App端，因为自带了一个独立v8引擎和小程序框架，所以比HTML5Plus或mui等普通hybrid的App引擎体积要大。Android基础引擎约9M。App还提供了扩展模块，比如地图、蓝牙等，打包时如不需要这些模块，可以裁剪掉，以缩小发行包体积。在 manifest.json-App模块权限 里可以选择。
- App端支持如果选择纯nvue项目（manifest里设置app-plus下的renderer:"native"），包体积可以进一步减少2M左右。
- uni-app的App-Android端有so库的概念，支持不同的cpu类型的so库越多，包越大。在HBuilderX 2.7以前，Android app默认包含arm32和x86两个cpu的支持so库。包体积比较大。如果你在意体积控制，可以在manifest里去掉x86 cpu的支持（manifest可视化界面-App其他设置里选择cpu），这可以减少包体积到9M。从HBuilderX 2.7起，默认不再包含x86，如有需求请自行在manifest里勾选后打包。一般手机都是arm的，涉及x86 cpu场景很少，包括：个别少见的Android pad、as的模拟器里选择x86类型。



### `13. 国际化专题`

uni-app的国际化, 分为应用部分和框架部分。

可以在HBuilderX新建项目里选择`Hello i18n`示例或者插件市场[查看](https://ext.dcloud.net.cn/plugin?id=6462)。

#### `13.1 vue界面和js内容的国际化`

* main.js 引入并初始化 VueI18n

```javascript
// 国际化 json 文件，文件内容详见下面的示例
import en from './en.json'
import zhHans from './zh-Hans.json'
import zhHant from './zh-Hant.json'
const messages = {
	en,
	'zh-Hans': zhHans,
	'zh-Hant': zhHant
}

let i18nConfig = {
  locale: uni.getLocale(),// 获取已设置的语言
  messages
}

// VUE2
// #ifndef VUE3
import Vue from 'vue'
import VueI18n from 'vue-i18n'// v8.x
Vue.use(VueI18n)
const i18n = new VueI18n(i18nConfig)
Vue.config.productionTip = false
App.mpType = 'app'
const app = new Vue({
  i18n,
  ...App
})
app.$mount()
// #endif

// VUE3
// #ifdef VUE3
import { createSSRApp } from 'vue'
import { createI18n } from 'vue-i18n'// v9.x
const i18n = createI18n(i18nConfig)
export function createApp() {
  const app = createSSRApp(App)
  app.use(i18n)
  return {
    app
  }
}
// #endif
```

* 国际化json文件内容

```json
{
  "index.title": "Hello i18n"
}
```

* 页面模板中使用 `$t()` 获取，并传递国际化json文件中定义的key，js中使用 `this.$t('')`

```vue
<template>
  <view class="container">
    <view class="title">$t('index.title')</view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
      }
    }
  }
</script>
```

* 页面中设置语言后需要调用 `this.$i18n.locale = 'zh-Hans'` 后生效

#### `13.2 nvue页面国际化`

* nvue 目前的国际化方案需要在每个页面单独引入uni-i18n，后续框架会抹平差异，抹平差异后和 vue 页面一样只需要在 main.js 中引入

```vue
<script>
  import {
    initVueI18n
  } from '@dcloudio/uni-i18n'

  // const messages = {} 此处内容省略，和 vue 全局引入的写法一致

  const { t } = initVueI18n(messages)

  export default {
    data() {
      return {
      }
    }
  }
</script>
```

#### `13.3 pages.json 国际化`

* pages.json不属于vue页面，其中的原生tabbar和原生导航栏里也有文字内容。
* 项目根目录的locale目录下配置语言json文件，locale/`语言地区代码`.json，如：en.json，zh-Hans.json，zh-Hant.json

```text
├── locale
│   ├── en.json
│   ├── zh-Hans.json
│   └── zh-Hant.json
```

* pages.json 示例
  * pages.json 支持以下属性配置国际化信息
    * navigationBarTitleText
    * titleNView->titleText
    * titleNView->searchInput->placeholder
    * tabBar->list->text

```json
{
  "pages": [
    {
      "path": "pages/index/index",
      "style": {
        "navigationBarTitleText": "%index.title%" // locale目录下 语言地区代码.json 文件中定义的 key，使用 %% 占位
      }
    }
  ],
  "tabBar": {
    "list": [{
        "pagePath": "pages/index/index",
        "text": "%index.home%"
      }
    ]
  }
}
```

#### `13.4 框架内置组件和API国际化`

这部分国际化，提供了2种策略，有自动策略，也有自定义方案。

##### `13.4.1 自动适配手机或浏览器语言`

* 内置组件和接口显示会根据系统语言环境自动切换，未支持的系统语言环境会显示为英文。

##### `13.4.2 自定义国际化内容`

* 项目根目录支持 `locale` 目录，locale/uni-app.`语言地区代码`.json，如：uni-app.en.json，uni-app.zh-Hans.json，uni-app.zh-Hant.json

```text
├── locale
│   ├── uni-app.en.json
│   ├── uni-app.zh-Hans.json
│   └── uni-app.zh-Hant.json
```

* uni-app.zh-Hans.json 文件

```json
{
  "common": {
    "uni.app.quit": "再按一次退出应用",
    "uni.async.error": "连接服务器超时，点击屏幕重试",
    "uni.showActionSheet.cancel": "取消",
    "uni.showToast.unpaired": "请注意 showToast 与 hideToast 必须配对使用",
    "uni.showLoading.unpaired": "请注意 showLoading 与 hideLoading 必须配对使用",
    "uni.showModal.cancel": "取消",
    "uni.showModal.confirm": "确定",
    "uni.chooseImage.cancel": "取消",
    "uni.chooseImage.sourceType.album": "从相册选择",
    "uni.chooseImage.sourceType.camera": "拍摄",
    "uni.chooseVideo.cancel": "取消",
    "uni.chooseVideo.sourceType.album": "从相册选择",
    "uni.chooseVideo.sourceType.camera": "拍摄",
    "uni.previewImage.cancel": "取消",
    "uni.previewImage.button.save": "保存图像",
    "uni.previewImage.save.success": "保存图像到相册成功",
    "uni.previewImage.save.fail": "保存图像到相册失败",
    "uni.setClipboardData.success": "内容已复制",
    "uni.scanCode.title": "扫码",
    "uni.scanCode.album": "相册",
    "uni.scanCode.fail": "识别失败",
    "uni.scanCode.flash.on": "轻触照亮",
    "uni.scanCode.flash.off": "轻触关闭",
    "uni.startSoterAuthentication.authContent": "指纹识别中...",
    "uni.picker.done": "完成",
    "uni.picker.cancel": "取消",
    "uni.video.danmu": "弹幕",
    "uni.video.volume": "音量",
    "uni.button.feedback.title": "问题反馈",
    "uni.button.feedback.send": "发送"
  },
  "ios": {},
  "android": {}
}
```

#### `13.5 manifest.json 国际化`

* 和 pages.json 一致，在项目根目录增加 locale/uni-app.`语言地区代码`.json 文件，然后在 `manifest.json` 中使用 %% 占位

```json
{
  "name" : "%app.name%",
  "appid" : "",
  "description" : "",
  "versionName" : "1.0.0",
  "versionCode" : "100",
  "locale": "zh-Hans" // 设置默认语言，
}
```

#### `13.5 语言API`

* [uni.getSystemInfo](https://uniapp.dcloud.io/api/system/info.html) 可以得到设备OS的语言、运行宿主host的语言以及应用自身的语言。

* [uni.getLocale](https://uniapp.dcloud.net.cn/api/ui/locale#getlocale) 获取应用当前使用的语言
* [uni.setLocale ](https://uniapp.dcloud.net.cn/api/ui/locale#setlocale)设置应用语言
* [uni.onLocaleChange](https://uniapp.dcloud.net.cn/api/ui/locale#onlocalechange) 当前应用语言发生变化时，触发回调。也就是`uni.setLocale`执行时。

#### `13.6 语言代码`

* 语言代码通常为两个或三个字母，参考[ISO 639](https://zh.wikipedia.org/wiki/ISO_639-1代码表)规范

* 语言代码-地区代码，地区代码为两个字母，参考[ISO 3166-2](https://zh.wikipedia.org/wiki/ISO_3166-2)规范



### `14. easycom组件规范`

* 传统vue组件，需要安装、引用、注册，三个步骤后才能使用组件。`easycom`将其精简为一步。

* 只要组件安装在项目的components目录下或`uni_modules`目录下，并符合`components/组件名称/组件名称.vue`目录结构。就可以不用引用、注册，直接在页面中使用。

* 比如前述举例的[uni-rate组件](https://ext.dcloud.net.cn/plugin?id=33)，它导入到uni-app项目后，存放在了目录/components/uni-rate/uni-rate.vue

* 同时它的组件名称也叫uni-rate，所以这样的组件，不用在script里注册和引用。 如下：

```vue
<template>
		<view>
			<uni-rate></uni-rate><!-- 这里会显示一个五角星，并且点击后会自动亮星 -->
		</view>
	</template>
<script>
	// 这里不用import引入，也不需要在components内注册uni-list组件。template里就可以直接用
	export default {
		data() {
			return {
				
			}
		}
	}
</script>
```

* 不管components目录下安装了多少组件，`easycom`打包后会自动剔除没有使用的组件，对组件库的使用尤为友好。组件库批量安装，随意使用，自动按需打包。
* `easycom`是自动开启的，不需要手动开启。
* 如果你的组件名称或路径不符合easycom的默认规范，可以在`pages.json`的`easycom`节点进行个性化设置，自定义匹配组件的策略。[另见](https://uniapp.dcloud.net.cn/collocation/pages#easycom)

### `15. uni_module规范`

uni_module其实不止服务于组件，它可以服务于组件、js库、页面、项目等所有DCloud插件市场所支持的种类。

符合uni_module规范的组件都在项目的`uni_modules`目录下，以插件id为目录存放。（项目模板不放在`uni_modules`目录下）

在HBuilderX中点右键可方便的更新插件，插件作者也可以方便的上传插件。

uni_module还支持云端一体的插件。

uni_module有详细的专项文档，请另行查阅[uni_module规范](https://uniapp.dcloud.net.cn/plugin/uni_modules.html)。







## `III>uni-app 全局配置文件`

### [1. pages.json 页面路由](https://uniapp.dcloud.net.cn/collocation/pages.html)

* 配置项列表

|                                                              |              |      |                                         |            |
| :----------------------------------------------------------- | :----------- | :--- | :-------------------------------------- | :--------- |
| 属性                                                         | 类型         | 必填 | 描述                                    | 平台兼容   |
| [globalStyle](https://uniapp.dcloud.net.cn/collocation/pages#globalstyle) | Object       | 否   | 设置默认页面的窗口表现                  |            |
| [pages](https://uniapp.dcloud.net.cn/collocation/pages#pages) | Object Array | 是   | 设置页面路径及窗口表现                  |            |
| [easycom](https://uniapp.dcloud.net.cn/collocation/pages#easycom) | Object       | 否   | 组件自动引入规则                        | 2.5.5+     |
| [tabBar](https://uniapp.dcloud.net.cn/collocation/pages#tabbar) | Object       | 否   | 设置底部 tab 的表现                     |            |
| [condition](https://uniapp.dcloud.net.cn/collocation/pages#condition) | Object       | 否   | 启动模式配置                            |            |
| [subPackages](https://uniapp.dcloud.net.cn/collocation/pages#subPackages) | Object Array | 否   | 分包加载配置                            |            |
| [preloadRule](https://uniapp.dcloud.net.cn/collocation/pages#preloadrule) | Object       | 否   | 分包预下载规则                          | 微信小程序 |
| [workers](https://developers.weixin.qq.com/miniprogram/dev/framework/workers.html) | String       | 否   | `Worker` 代码放置的目录                 | 微信小程序 |
| [leftWindow](https://uniapp.dcloud.net.cn/collocation/pages#leftwindow) | Object       | 否   | 大屏左侧窗口                            | H5         |
| [topWindow](https://uniapp.dcloud.net.cn/collocation/pages#topwindow) | Object       | 否   | 大屏顶部窗口                            | H5         |
| [rightWindow](https://uniapp.dcloud.net.cn/collocation/pages#rightwindow) | Object       | 否   | 大屏右侧窗口                            | H5         |
| [uniIdRouter](https://uniapp.dcloud.net.cn/uniCloud/uni-id-summary#uni-id-router) | Object       | 否   | 自动跳转相关配置，新增于HBuilderX 3.5.0 |            |
| entryPagePath                                                | String       | 否   | 默认启动首页，新增于HBuilderX 3.7.0     |            |

```json
{
	"pages": [{
		"path": "pages/component/index",
		"style": {
			"navigationBarTitleText": "组件"
		}
	}, {
		"path": "pages/API/index",
		"style": {
			"navigationBarTitleText": "接口"
		}
	}, {
		"path": "pages/component/view/index",
		"style": {
			"navigationBarTitleText": "view"
		}
	}],
	"condition": { //模式配置，仅开发期间生效
		"current": 0, //当前激活的模式（list 的索引项）
		"list": [{
			"name": "test", //模式名称
			"path": "pages/component/view/index" //启动页面，必选
		}]
	},
	"globalStyle": {
		"navigationBarTextStyle": "black",
		"navigationBarTitleText": "演示",
		"navigationBarBackgroundColor": "#F8F8F8",
		"backgroundColor": "#F8F8F8",
		"usingComponents":{
			"collapse-tree-item":"/components/collapse-tree-item"
		},
		"renderingMode": "seperated", // 仅微信小程序，webrtc 无法正常时尝试强制关闭同层渲染
		"pageOrientation": "portrait", //横屏配置，全局屏幕旋转设置(仅 APP/微信/QQ小程序)，支持 auto / portrait / landscape
		"rpxCalcMaxDeviceWidth": 960,
		"rpxCalcBaseDeviceWidth": 375,
		"rpxCalcIncludeWidth": 750
	},
	"tabBar": {
		"color": "#7A7E83",
		"selectedColor": "#3cc51f",
		"borderStyle": "black",
		"backgroundColor": "#ffffff",
		"height": "50px",
		"fontSize": "10px",
		"iconWidth": "24px",
		"spacing": "3px",
    	"iconfontSrc":"static/iconfont.ttf", // app tabbar 字体.ttf文件路径 app 3.4.4+
		"list": [{
			"pagePath": "pages/component/index",
			"iconPath": "static/image/icon_component.png",
			"selectedIconPath": "static/image/icon_component_HL.png",
			"text": "组件",
      		"iconfont": { // 优先级高于 iconPath，该属性依赖 tabbar 根节点的 iconfontSrc
       			"text": "\ue102",
        		"selectedText": "\ue103",
        		"fontSize": "17px",
        		"color": "#000000",
        		"selectedColor": "#0000ff"
      		}
		}, {
			"pagePath": "pages/API/index",
			"iconPath": "static/image/icon_API.png",
			"selectedIconPath": "static/image/icon_API_HL.png",
			"text": "接口"
		}],
		"midButton": {
			"width": "80px",
			"height": "50px",
			"text": "文字",
			"iconPath": "static/image/midButton_iconPath.png",
			"iconWidth": "24px",
			"backgroundImage": "static/image/midButton_backgroundImage.png"
		}
	},
  "easycom": {
    "autoscan": true, //是否自动扫描组件
    "custom": {//自定义扫描规则
      "^uni-(.*)": "@/components/uni-$1.vue"
    }
  },
  "topWindow": {
    "path": "responsive/top-window.vue",
    "style": {
      "height": "44px"
    }
  },
  "leftWindow": {
    "path": "responsive/left-window.vue",
    "style": {
      "width": "300px"
    }
  },
  "rightWindow": {
    "path": "responsive/right-window.vue",
    "style": {
      "width": "300px"
    },
    "matchMedia": {
      "minWidth": 768
    }
  }
}

```

#### [1.1 globalStyle](https://uniapp.dcloud.net.cn/collocation/pages.html#globalstyle)

| 属性                         | 类型     | 默认值   | 描述                                                         | 平台差异说明                                                 |
| :--------------------------- | :------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| navigationBarBackgroundColor | HexColor | #F7F7F7  | 导航栏背景颜色（同状态栏背景色）                             | APP与H5为#F7F7F7，小程序平台请参考相应小程序文档             |
| navigationBarTextStyle       | String   | white    | 导航栏标题颜色及状态栏前景颜色，仅支持 black/white           | 支付宝小程序不支持，请使用 [my.setNavigationBar](https://opendocs.alipay.com/mini/api/xwq8e6) |
| navigationBarTitleText       | String   |          | 导航栏标题文字内容                                           |                                                              |
| navigationStyle              | String   | default  | 导航栏样式，仅支持 default/custom。custom即取消默认的原生导航栏，需看[使用注意](https://uniapp.dcloud.net.cn/collocation/pages#customnav) | 微信小程序 7.0+、百度小程序、H5、App（2.0.3+）               |
| backgroundColor              | HexColor | #ffffff  | 下拉显示出来的窗口的背景色                                   | 微信小程序                                                   |
| backgroundTextStyle          | String   | dark     | 下拉 loading 的样式，仅支持 dark / light                     | 微信小程序                                                   |
| enablePullDownRefresh        | Boolean  | false    | 是否开启下拉刷新，详见[页面生命周期](https://uniapp.dcloud.net.cn/tutorial/page.html#lifecycle)。 |                                                              |
| onReachBottomDistance        | Number   | 50       | 页面上拉触底事件触发时距页面底部距离，单位只支持px，详见[页面生命周期](https://uniapp.dcloud.net.cn/tutorial/page.html#lifecycle) |                                                              |
| backgroundColorTop           | HexColor | #ffffff  | 顶部窗口的背景色（bounce回弹区域）                           | 仅 iOS 平台                                                  |
| backgroundColorBottom        | HexColor | #ffffff  | 底部窗口的背景色（bounce回弹区域）                           | 仅 iOS 平台                                                  |
| titleImage                   | String   |          | 导航栏图片地址（替换当前文字标题），支付宝小程序内必须使用https的图片链接地址 | 支付宝小程序、H5、APP                                        |
| transparentTitle             | String   | none     | 导航栏整体（前景、背景）透明设置。支持 always 一直透明 / auto 滑动自适应 / none 不透明 | 支付宝小程序、H5、APP                                        |
| titlePenetrate               | String   | NO       | 导航栏点击穿透                                               | 支付宝小程序、H5                                             |
| pageOrientation              | String   | portrait | 横屏配置，屏幕旋转设置，仅支持 auto / portrait / landscape 详见 [响应显示区域变化](https://developers.weixin.qq.com/miniprogram/dev/framework/view/resizable.html) | App 2.4.7+、微信小程序、QQ小程序                             |
| animationType                | String   | pop-in   | 窗口显示的动画效果，详见：[窗口动画](https://uniapp.dcloud.net.cn/api/router#animation) | App                                                          |
| animationDuration            | Number   | 300      | 窗口显示动画的持续时间，单位为 ms                            | App                                                          |
| app-plus                     | Object   |          | 设置编译到 App 平台的特定样式，配置项参考下方 [app-plus](https://uniapp.dcloud.net.cn/collocation/pages#app-plus) | App                                                          |
| h5                           | Object   |          | 设置编译到 H5 平台的特定样式，配置项参考下方 [H5](https://uniapp.dcloud.net.cn/collocation/pages#h5) | H5                                                           |
| mp-alipay                    | Object   |          | 设置编译到 mp-alipay 平台的特定样式，配置项参考下方 [MP-ALIPAY](https://uniapp.dcloud.net.cn/collocation/pages#mp-alipay) | 支付宝小程序                                                 |
| mp-weixin                    | Object   |          | 设置编译到 mp-weixin 平台的特定样式                          | 微信小程序                                                   |
| mp-baidu                     | Object   |          | 设置编译到 mp-baidu 平台的特定样式                           | 百度小程序                                                   |
| mp-toutiao                   | Object   |          | 设置编译到 mp-toutiao 平台的特定样式                         | 字节跳动小程序                                               |
| mp-lark                      | Object   |          | 设置编译到 mp-lark 平台的特定样式                            | 飞书小程序                                                   |
| mp-qq                        | Object   |          | 设置编译到 mp-qq 平台的特定样式                              | QQ小程序                                                     |
| mp-kuaishou                  | Object   |          | 设置编译到 mp-kuaishou 平台的特定样式                        | 快手小程序                                                   |
| mp-jd                        | Object   |          | 设置编译到 mp-jd 平台的特定样式                              | 京东小程序                                                   |
| usingComponents              | Object   |          | 引用小程序组件，参考 [小程序组件](https://uniapp.dcloud.net.cn/tutorial/miniprogram-subject.html#小程序自定义组件支持) |                                                              |
| renderingMode                | String   |          | 同层渲染，webrtc(实时音视频) 无法正常时尝试配置 seperated 强制关掉同层 | 微信小程序                                                   |
| leftWindow                   | Boolean  | true     | 当存在 leftWindow 时，默认是否显示 leftWindow                | H5                                                           |
| topWindow                    | Boolean  | true     | 当存在 topWindow 时，默认是否显示 topWindow                  | H5                                                           |
| rightWindow                  | Boolean  | true     | 当存在 rightWindow 时，默认是否显示 rightWindow              | H5                                                           |
| rpxCalcMaxDeviceWidth        | Number   | 960      | rpx 计算所支持的最大设备宽度，单位 px                        | App（vue2 且不含 nvue）、H5（2.8.12+）                       |
| rpxCalcBaseDeviceWidth       | Number   | 375      | rpx 计算使用的基准设备宽度，设备实际宽度超出 rpx 计算所支持的最大设备宽度时将按基准宽度计算，单位 px | App（vue2 且不含 nvue）、H5（2.8.12+）                       |
| rpxCalcIncludeWidth          | Number   | 750      | rpx 计算特殊处理的值，始终按实际的设备宽度计算，单位 rpx     | App（vue2 且不含 nvue）、H5（2.8.12+）                       |
| dynamicRpx                   | Boolean  | false    | 动态 rpx，屏幕大小变化会重新渲染 rpx                         | App-nvue（vue3 固定值为 true） 3.2.13+                       |
| maxWidth                     | Number   |          | 单位px，当浏览器可见区域宽度大于maxWidth时，两侧留白，当小于等于maxWidth时，页面铺满；不同页面支持配置不同的maxWidth；maxWidth = leftWindow(可选)+page(页面主体)+rightWindow(可选) | H5（2.9.9+）                                                 |



#### [1.2 pages](https://uniapp.dcloud.net.cn/collocation/pages.html#pages)

* `uni-app` 通过 pages 节点配置应用由哪些页面组成，pages 节点接收一个数组，数组每个项都是一个对象，其属性值如下：
  * pages节点的第一项为应用入口页（即首页）
  * **应用中新增/减少页面**，都需要对 pages 数组进行修改
  * 文件名**不需要写后缀**，框架会自动寻找路径下的页面资源

| 属性  | 类型   | 默认值 | 描述                                                         |
| :---- | :----- | :----- | :----------------------------------------------------------- |
| path  | String |        | 配置页面路径                                                 |
| style | Object |        | 配置页面窗口表现，配置项参考下方 [pageStyle](https://uniapp.dcloud.net.cn/collocation/pages#style) |

```json
{
    "pages": [
        {
            "path": "pages/index/index",
            "style": { ... }
        }, {
            "path": "pages/login/login",
            "style": { ... }
        }
    ]
}
```



#### [1.3 style](https://uniapp.dcloud.net.cn/collocation/pages.html#style)

* 用于设置每个页面的状态栏、导航条、标题、窗口背景色等。

* 页面中配置项会覆盖 [globalStyle](https://uniapp.dcloud.net.cn/collocation/pages#globalstyle) 中相同的配置项
  * 使用 `maxWidth` 时，页面内fixed元素需要使用--window-left,--window-right来保证布局位置正确

| 属性                         | 类型     | 默认值  | 描述                                                         | 平台差异说明                                                 |
| :--------------------------- | :------- | :------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| navigationBarBackgroundColor | HexColor | #000000 | 导航栏背景颜色（同状态栏背景色），如"#000000"                |                                                              |
| navigationBarTextStyle       | String   | white   | 导航栏标题颜色及状态栏前景颜色，仅支持 black/white           |                                                              |
| navigationBarTitleText       | String   |         | 导航栏标题文字内容                                           |                                                              |
| navigationBarShadow          | Object   |         | 导航栏阴影，配置参考下方 [导航栏阴影](https://uniapp.dcloud.net.cn/collocation/pages#navigationBarShadow) |                                                              |
| navigationStyle              | String   | default | 导航栏样式，仅支持 default/custom。custom即取消默认的原生导航栏，需看[使用注意](https://uniapp.dcloud.net.cn/collocation/pages#customnav) | 微信小程序 7.0+、百度小程序、H5、App（2.0.3+）               |
| disableScroll                | Boolean  | false   | 设置为 true 则页面整体不能上下滚动（bounce效果），只在页面配置中有效，在globalStyle中设置无效 | 微信小程序（iOS）、百度小程序（iOS）                         |
| backgroundColor              | HexColor | #ffffff | 窗口的背景色                                                 | 微信小程序、百度小程序、字节跳动小程序、飞书小程序、京东小程序 |
| backgroundTextStyle          | String   | dark    | 下拉 loading 的样式，仅支持 dark/light                       |                                                              |
| enablePullDownRefresh        | Boolean  | false   | 是否开启下拉刷新，详见[页面生命周期](https://uniapp.dcloud.net.cn/tutorial/page.html#lifecycle)。 |                                                              |
| onReachBottomDistance        | Number   | 50      | 页面上拉触底事件触发时距页面底部距离，单位只支持px，详见[页面生命周期](https://uniapp.dcloud.net.cn/tutorial/page.html#lifecycle) |                                                              |
| backgroundColorTop           | HexColor | #ffffff | 顶部窗口的背景色（bounce回弹区域）                           | 仅 iOS 平台                                                  |
| backgroundColorBottom        | HexColor | #ffffff | 底部窗口的背景色（bounce回弹区域）                           | 仅 iOS 平台                                                  |
| disableSwipeBack             | Boolean  | false   | 是否禁用滑动返回                                             | App-iOS（3.4.0+）                                            |
| titleImage                   | String   |         | 导航栏图片地址（替换当前文字标题），支付宝小程序内必须使用https的图片链接地址 | 支付宝小程序、H5、App                                        |
| transparentTitle             | String   | none    | 导航栏透明设置。支持 always 一直透明 / auto 滑动自适应 / none 不透明 | 支付宝小程序、H5、APP                                        |
| titlePenetrate               | String   | NO      | 导航栏点击穿透                                               | 支付宝小程序、H5                                             |
| app-plus                     | Object   |         | 设置编译到 App 平台的特定样式，配置项参考下方 [app-plus](https://uniapp.dcloud.net.cn/collocation/pages#app-plus) | App                                                          |
| h5                           | Object   |         | 设置编译到 H5 平台的特定样式，配置项参考下方 [H5](https://uniapp.dcloud.net.cn/collocation/pages#h5) | H5                                                           |
| mp-alipay                    | Object   |         | 设置编译到 mp-alipay 平台的特定样式，配置项参考下方 [MP-ALIPAY](https://uniapp.dcloud.net.cn/collocation/pages#mp-alipay) | 支付宝小程序                                                 |
| mp-weixin                    | Object   |         | 设置编译到 mp-weixin 平台的特定样式                          | 微信小程序                                                   |
| mp-baidu                     | Object   |         | 设置编译到 mp-baidu 平台的特定样式                           | 百度小程序                                                   |
| mp-toutiao                   | Object   |         | 设置编译到 mp-toutiao 平台的特定样式                         | 字节跳动小程序                                               |
| mp-lark                      | Object   |         | 设置编译到 mp-lark 平台的特定样式                            | 飞书小程序                                                   |
| mp-qq                        | Object   |         | 设置编译到 mp-qq 平台的特定样式                              | QQ小程序                                                     |
| mp-kuaishou                  | Object   |         | 设置编译到 mp-kuaishou 平台的特定样式                        | 快手小程序                                                   |
| mp-jd                        | Object   |         | 设置编译到 mp-jd 平台的特定样式                              | 京东小程序                                                   |
| usingComponents              | Object   |         | 引用小程序组件，参考 [小程序组件](https://uniapp.dcloud.net.cn/tutorial/miniprogram-subject.html#小程序自定义组件支持) | App、微信小程序、支付宝小程序、百度小程序、京东小程序        |
| leftWindow                   | Boolean  | true    | 当存在 leftWindow时，当前页面是否显示 leftWindow             | H5                                                           |
| topWindow                    | Boolean  | true    | 当存在 topWindow 时，当前页面是否显示 topWindow              | H5                                                           |
| rightWindow                  | Boolean  | true    | 当存在 rightWindow时，当前页面是否显示 rightWindow           | H5                                                           |
| maxWidth                     | Number   |         | 单位px，当浏览器可见区域宽度大于maxWidth时，两侧留白，当小于等于maxWidth时，页面铺满；不同页面支持配置不同的maxWidth；maxWidth = leftWindow(可选)+page(页面主体)+rightWindow(可选) | H5（2.9.9+                                                   |

```json
{
  "pages": [{
      "path": "pages/index/index",
      "style": {
        "navigationBarTitleText": "首页",//设置页面标题文字
        "enablePullDownRefresh":true//开启下拉刷新
      }
    },
    ...
  ]
}
```

##### [1.3.1 app-plus](https://uniapp.dcloud.net.cn/collocation/pages.html#app-plus)

* 配置编译到 App 平台时的特定样式，部分常用配置 H5 平台也支持。以下仅列出常用，更多配置项参考 [WebviewStyles](http://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewStyles)
* `.nvue` 页面仅支持 `titleNView、pullToRefresh、scrollIndicator` 配置，其它配置项暂不支持

| 属性              | 类型     | 默认值    | 描述                                                         | 平台兼容                                                     |
| :---------------- | :------- | :-------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| background        | HexColor | #FFFFFF   | 窗体背景色。无论vue页面还是nvue页面，在App上都有一个父级原生窗体，该窗体的背景色生效时间快于页面里的css生效时间 | App                                                          |
| titleNView        | Object   |           | 导航栏 ，详见:[导航栏](https://uniapp.dcloud.net.cn/collocation/pages#app-titleNView) | App、H5                                                      |
| subNVues          | Object   |           | 原生子窗体，详见:[原生子窗体](https://uniapp.dcloud.net.cn/collocation/pages#app-subNVues) | App 1.9.10+                                                  |
| bounce            | String   |           | 页面回弹效果，设置为 "none" 时关闭效果。                     | App-vue（nvue Android无页面级bounce效果，仅list、recycle-list、waterfall等滚动组件有bounce效果） |
| popGesture        | String   | close     | 侧滑返回功能，可选值："close"（启用侧滑返回）、"none"（禁用侧滑返回） | App-iOS                                                      |
| softinputNavBar   | String   | auto      | iOS软键盘上完成工具栏的显示模式，设置为 "none" 时关闭工具栏。 | App-iOS                                                      |
| softinputMode     | String   | adjustPan | 软键盘弹出模式，支持 adjustResize、adjustPan 两种模式        | App                                                          |
| pullToRefresh     | Object   |           | 下拉刷新                                                     | App                                                          |
| scrollIndicator   | String   |           | 滚动条显示策略，设置为 "none" 时不显示滚动条。               | App                                                          |
| animationType     | String   | pop-in    | 窗口显示的动画效果，详见：[窗口动画](https://uniapp.dcloud.net.cn/api/router#animation)。 | App                                                          |
| animationDuration | Number   | 300       | 窗口显示动画的持续时间，单位为 ms。                          | App                                                          |



###### [1.3.1.1 titleNView (导航栏)](https://uniapp.dcloud.net.cn/collocation/pages.html#app-titlenview)

| 属性             | 类型    | 默认值     | 描述                                                         | 版本兼容性                        |
| :--------------- | :------ | :--------- | :----------------------------------------------------------- | :-------------------------------- |
| backgroundColor  | String  | #F7F7F7    | 背景颜色，支持16进制颜色或RGBA颜色。                         | App端仅悬浮导航栏支持RGBA颜色     |
| buttons          | Array   |            | 自定义按钮，详见 [buttons](https://uniapp.dcloud.net.cn/collocation/pages#app-titlenview-buttons) | 纯nvue即render:native时暂不支持   |
| titleColor       | String  | #000000    | 标题文字颜色                                                 |                                   |
| titleOverflow    | String  | ellipsis   | 标题文字超出显示区域时处理方式。"clip"-超出显示区域时内容裁剪；"ellipsis"-超出显示区域时尾部显示省略标记（...）。 |                                   |
| titleText        | String  |            | 标题文字内容                                                 |                                   |
| titleSize        | String  |            | 标题文字字体大小                                             |                                   |
| type             | String  | default    | 导航栏样式。"default"-默认样式；"transparent"-滚动透明渐变；"float"-悬浮导航栏。 | App-nvue 2.4.4+ 支持、App-vue、H5 |
| tags             | Array   |            | 原生 View 增强，详见：[5+ View 控件](http://www.html5plus.org/doc/zh_cn/nativeobj.html#plus.nativeObj.ViewDrawTagStyles) |                                   |
| searchInput      | Object  |            | 原生导航栏上的搜索框配置，详见：[searchInput](https://uniapp.dcloud.net.cn/collocation/pages#app-titlenview-searchinput) | 1.6.0                             |
| homeButton       | Boolean | false      | 标题栏控件是否显示Home按钮                                   |                                   |
| autoBackButton   | Boolean | true       | 标题栏控件是否显示左侧返回按钮                               | App 2.6.3+                        |
| backButton       | Object  |            | 返回按钮的样式，详见：[backButton](https://uniapp.dcloud.net.cn/collocation/pages#app-titleNView-backButtonStyles) | App 2.6.3                         |
| backgroundImage  | String  |            | 支持以下类型： 背景图片路径 - 如"/static/img.png"，仅支持本地文件绝对路径，根据实际标题栏宽高拉伸绘制； 渐变色 - 仅支持线性渐变，两种颜色的渐变，如“linear-gradient(to top, #a80077, #66ff00)”， 其中第一个参数为渐变方向，可取值： "to right"表示从左向右渐变， “to left"表示从右向左渐变， “to bottom"表示从上到下渐变， “to top"表示从下到上渐变， “to bottom right"表示从左上角到右下角， “to top left"表示从右下角到左上角 | 2.6.3                             |
| backgroundRepeat | String  |            | 仅在backgroundImage设置为图片路径时有效。 可取值： "repeat" - 背景图片在垂直方向和水平方向平铺； "repeat-x" - 背景图片在水平方向平铺，垂直方向拉伸； “repeat-y” - 背景图片在垂直方向平铺，水平方向拉伸； “no-repeat” - 背景图片在垂直方向和水平方向都拉伸。 默认使用 “no-repeat" | 2.6.3                             |
| titleAlign       | String  | "auto"     | 可取值： "center"-居中对齐； "left"-居左对齐； "auto"-根据平台自动选择（Android平台居左对齐，iOS平台居中对齐） | 2.6.3                             |
| blurEffect       | String  | "none"     | 此效果将会高斯模糊显示标题栏后的内容，仅在type为"transparent"或"float"时有效。 可取值： "dark" - 暗风格模糊，对应iOS原生UIBlurEffectStyleDark效果； "extralight" - 高亮风格模糊，对应iOS原生UIBlurEffectStyleExtraLight效果； "light" - 亮风格模糊，对应iOS原生UIBlurEffectStyleLight效果； "none" - 无模糊效果。 注意：使用模糊效果时应避免设置背景颜色，设置背景颜色可能覆盖模糊效果。 | 2.4.3                             |
| coverage         | String  | "132px"    | 标题栏控件变化作用范围，仅在type值为transparent时有效，页面滚动时标题栏背景透明度将发生变化。 当页面滚动到指定偏移量时标题栏背景变为完全不透明。 支持百分比、像素值 |                                   |
| splitLine        | Boolean | false      | 标题栏的底部分割线([SplitLineStyles](https://uniapp.dcloud.net.cn/collocation/pages#app-titleNView-splitLineStyles))，设置此属性则在标题栏控件的底部显示分割线，可配置颜色值及高度。 设置此属性值为undefined或null则隐藏分割线。 默认不显示底部分割线 | 2.6.6                             |
| subtitleColor    | String  |            | 副标题文字颜色，颜色值格式为"#RRGGBB"和"rgba(R,G,B,A)"，如"#FF0000"表示标题文字颜色为红色。 默认值与主标题文字颜色一致 | 2.6.6                             |
| subtitleSize     | String  | "auto"     | 副标题文字字体大小，字体大小单位为像素，如"14px"表示字体大小为14像素，默认值为12像素。 | 2.6.6                             |
| subtitleOverflow | String  | "ellipsis" | 标题文字超出显示区域时处理方式，可取值： "clip" - 超出显示区域时内容裁剪； "ellipsis" - 超出显示区域时尾部显示省略标记（...）。 | 2.6.6                             |
| subtitleText     | String  |            | 副标题文字内容，设置副标后将显示两行标题，副标显示在主标题（titleText）下方。 注意：设置副标题后将居左显示 | 2.6.6                             |
| titleIcon        | String  |            | 标题图标，图标路径如"./img/t.png"，仅支持本地文件路径， 相对路径，相对于当前页面的host位置，固定宽高为逻辑像素值"34px"。 要求图片的宽高相同。 注意：设置标题图标后标题将居左显示。 | 2.6.6                             |
| titleIconRadius  | String  | 无圆角     | 标题图标圆角，取值格式为"XXpx"，其中XX为像素值（逻辑像素），如"10px"表示10像素半径圆角。 | 2.6.6                             |

* [1.3.1.1.1 splitLine](https://uniapp.dcloud.net.cn/collocation/pages.html#app-titlenview-splitlinestyles)

|        |        |         |                                                              |            |
| :----- | :----- | :------ | :----------------------------------------------------------- | :--------- |
| 属性   | 类型   | 默认值  | 描述                                                         | 版本兼容性 |
| color  | String | #CCCCCC | 底部分割线颜色，可取值： "#RRGGBB"格式字符串，如"#FF0000"表示绘制红色分割线； "rgba(R,G,B,A)"，其中R/G/B分别代表红色值/绿色值/蓝色值，正整数类型，取值范围为0-255，A为透明度，浮点数类型，取值范围为0-1（0为全透明，1为不透明），如"rgba(255,0,0,0.5)"，表示红色半透明 |            |
| height | String | "1px"   | 可取值：像素值（逻辑像素），支持小数点，如"1px"表示1像素高；百分比，如"1%"，相对于标题栏控件的高度。 |            |

* [1.3.1.1.2 自定义按钮](https://uniapp.dcloud.net.cn/collocation/pages.html#app-titlenview-buttons)

| 属性         | 类型   | 默认值                                    | 描述                                                         |
| :----------- | :----- | :---------------------------------------- | :----------------------------------------------------------- |
| type         | String | none                                      | 按钮样式，可取值见：[buttons 样式](https://uniapp.dcloud.net.cn/collocation/pages#app-titlenview-buttons-type) |
| color        | String | 默认与标题文字颜色一致                    | 按钮上文字颜色                                               |
| background   | String | 默认值为灰色半透明                        | 按钮的背景颜色，仅在标题栏type=transparent时生效             |
| colorPressed | String | 默认值为 color 属性值自动调整透明度为 0.3 | 按下状态按钮文字颜色                                         |
| float        | String | right                                     | 按钮在标题栏上的显示位置，可取值"left"、"right"              |
| fontWeight   | String | normal                                    | 按钮上文字的粗细。可取值"normal"-标准字体、"bold"-加粗字体。 |
| fontSize     | String |                                           | 按钮上文字大小                                               |
| fontSrc      | String |                                           | 按钮上文字使用的字体文件路径。不支持网络地址，请统一使用本地地址。 |
| select       | String | false                                     | 是否显示选择指示图标（向下箭头），常用于城市选择             |
| text         | String |                                           | 按钮上显示的文字。使用字体图标时 unicode 字符表示必须 '\u' 开头，如 "\ue123"（注意不能写成"\e123"）。 |
| width        | String | 44px                                      | 按钮的宽度，可取值： "*px" - 逻辑像素值，如"10px"表示10逻辑像素值，不支持rpx。按钮的内容居中显示； "auto" - 自定计算宽度，根据内容自动调整按钮宽度 |

* ##### [1.3.1.1.3 自定义返回按钮的样式](https://uniapp.dcloud.net.cn/collocation/pages.html#app-titlenview-backbuttonstyles)

  * 当autoBackButton设置为true时生效。 通过此属性可自定义返回按钮样式，如图标大小、红点、角标、标题等。

| 属性         | 类型    | 默认值                         | 描述                                                         |
| :----------- | :------ | :----------------------------- | :----------------------------------------------------------- |
| background   | String  | none                           | 背景颜色，仅在标题栏type=transparent时生效，当标题栏透明时按钮显示的背景颜色。 可取值#RRGGBB和rgba格式颜色字符串，默认值为灰色半透明。 |
| badgeText    | String  |                                | 角标文本，最多显示3个字符，超过则显示为...                   |
| color        | String  | 窗口标题栏控件的标题文字颜色。 | 图标和标题颜色，可取值： "#RRGGBB"格式字符串，如"#FF0000"表示红色； "rgba(R,G,B,A)"，其中R/G/B分别代表红色值/绿色值/蓝色值，正整数类型，取值范围为0-255，A为透明度，浮点数类型，取值范围为0-1（0为全透明，1为不透明），如"rgba(255,0,0,0.5)"，表示红色半透明。 |
| colorPressed | String  |                                | 按下状态按钮文字颜色，可取值： "#RRGGBB"格式字符串，如"#FF0000"表示红色； "rgba(R,G,B,A)"，其中R/G/B分别代表红色值/绿色值/蓝色值，正整数类型，取值范围为0-255，A为透明度，浮点数类型，取值范围为0-1（0为全透明，1为不透明），如"rgba(255,0,0,0.5)"，表示红色半透明。 默认值为color属性值自动调整透明度为0.3。 |
| fontWeight   | String  | "normal"                       | 返回图标的粗细，可取值： "normal" - 标准字体； "bold" - 加粗字体。 |
| fontSize     | String  |                                | 返回图标文字大小，可取值：字体高度像素值，数字加"px"格式字符串，如"22px"。 窗口标题栏为透明样式（type="transparent"）时，默认值为"22px"； 窗口标题栏为默认样式（type="default"）时，默认值为"27px"。 |
| redDot       | Boolean | false                          | 是否显示红点，设置为true则显示红点，false则不显示红点。默认值为false。 注意：当设置了角标文本时红点不显示。 |
| title        | String  |                                | 返回按钮上的标题，显示在返回图标（字体图标）后，默认为空字符串。 |
| titleWeight  | String  | "normal"                       | 返回按钮上标题的粗细，可取值： "normal" - 标准字体； "bold" - 加粗字体。 |

* [1.3.1.1.4 按钮样式](https://uniapp.dcloud.net.cn/collocation/pages.html#app-titlenview-buttons-type)
  * 使用 type 值设置按钮的样式时，会忽略 fontSrc 和 text 属性。

| 值       | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| forward  | 前进按钮                                                     |
| back     | 后退按钮                                                     |
| share    | 分享按钮                                                     |
| favorite | 收藏按钮                                                     |
| home     | 主页按钮                                                     |
| menu     | 菜单按钮                                                     |
| close    | 关闭按钮                                                     |
| none     | 无样式，需通过 text 属性设置按钮上显示的内容、通过 fontSrc 属性设置使用的字体库。 |

* [1.3.1.1.5 搜索框配置](https://uniapp.dcloud.net.cn/collocation/pages.html#app-titlenview-searchinput)

  * searchInput可以在titleNView的原生导航栏上放置搜索框。其宽度根据周围元素自适应。

  | 属性             | 类型    | 默认值                | 描述                                                         |
  | :--------------- | :------ | :-------------------- | :----------------------------------------------------------- |
  | autoFocus        | Boolean | false                 | 是否自动获取焦点                                             |
  | align            | String  | center                | 非输入状态下文本的对齐方式。可取值： "left" - 居左对齐； "right" - 居右对齐； "center" - 居中对齐。 |
  | backgroundColor  | String  | rgba(255,255,255,0.5) | 背景颜色                                                     |
  | borderRadius     | String  | 0px                   | 输入框的圆角半径，取值格式为"XXpx"，其中XX为像素值（逻辑像素），不支持rpx。 |
  | placeholder      | String  |                       | 提示文本。                                                   |
  | placeholderColor | String  | #CCCCCC               | 提示文本颜色                                                 |
  | disabled         | Boolean | false                 | 是否可输入                                                   |

* 常见titleNView配置代码示例

  * buttons 的 text 推荐使用字体图标。如果使用了汉字或英文，推荐把字体改小一点，否则文字长度增加后，距离屏幕右边距太近。
  * App平台，buttons动态修改，[详见](https://ask.dcloud.net.cn/article/35374)
  * App平台，buttons角标动态修改，见 hello uni-app 中模板-顶部导航标题栏-导航栏带红点和角标
  * App平台，设置searchInput的文字动态修改，API见[文档](https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject.setTitleNViewSearchInputText)。注意disable状态无法设置文字、placehold暂不支持动态设置
  * H5平台，如需实现上述动态修改，需在条件编译通过dom操作修改

```json
{
	"pages": [{
			"path": "pages/index/index", //首页
			"style": {
				"app-plus": {
					"titleNView": false //禁用原生导航栏
				}
			}
		}, {
			"path": "pages/log/log", //日志页面
			"style": {
				"app-plus": {
					"bounce": "none", //关闭窗口回弹效果
					"titleNView": {
						"buttons": [ //原生标题栏按钮配置,
							{
								"text": "分享" //原生标题栏增加分享按钮，点击事件可通过页面的 onNavigationBarButtonTap 函数进行监听
							}
						],
						"backButton": { //自定义 backButton
							"background": "#00FF00"
						}
					}
				}
			}
		}, {
			"path": "pages/detail/detail", //详情页面
			"style": {
				"navigationBarTitleText": "详情",
				"app-plus": {
					"titleNView": {
						"type": "transparent"//透明渐变导航栏 App-nvue 2.4.4+ 支持
					}
				}
			}
		}, {
			"path": "pages/search/search", //搜索页面
			"style": {
				"app-plus": {
					"titleNView": {
						"type": "transparent",//透明渐变导航栏 App-nvue 2.4.4+ 支持
						"searchInput": {
							"backgroundColor": "#fff",
							"borderRadius": "6px", //输入框圆角
							"placeholder": "请输入搜索内容",
							"disabled": true //disable时点击输入框不置焦，可以跳到新页面搜索
						}
					}
				}
			}
		}
		...
	]
}
```



###### [1.3.1.2 subNVues(原生子窗体)](https://uniapp.dcloud.net.cn/collocation/pages.html#app-subnvues)

* `subNVues` 是 vue 页面的原生子窗体。用于解决App中 vue 页面中的层级覆盖和原生界面灵活自定义用的。
* 它不是全屏页面，也不是组件，就是一个原生子窗体。它是一个 nvue 页面，使用 weex 引擎渲染，提供了比 cover-view、plus.nativeObj.view 更强大的原生排版能力，方便自定义原生导航或覆盖原生地图、视频等。请详读[subNVues 开发指南](http://ask.dcloud.net.cn/article/35948)
* `subNVue` 也可以在 nvue 页面中使用。
* `subNVues` 的 `id` 是全局唯一的，不能重复
* 可以通过 [uni.getSubNVueById('id')](https://uniapp.dcloud.net.cn/api/window/subNVues#app-getsubnvuebyid) 获取 `subNVues` 的实例
* `subNVues` 的 `path` 属性只能是 `nvue` 文件路径

| 属性  | 类型   | 描述                                                         |
| :---- | :----- | :----------------------------------------------------------- |
| id    | String | subNVue 原生子窗体的标识                                     |
| path  | String | 配置 nvue 文件路径，nvue 文件需放置到使用 subNvue 的页面文件目录下 |
| type  | String | 原生子窗口内置样式，可取值：'popup',弹出层；"navigationBar",导航栏 |
| style | Object | subNVue 原生子窗体的样式，配置项参考下方 [subNVuesStyle](https://uniapp.dcloud.net.cn/collocation/pages#app-subNVuesStyle) |

* [1.3.1.2.1 原生子窗体样式](https://uniapp.dcloud.net.cn/collocation/pages.html#app-subnvuesstyle)

| 属性       | 类型     | 默认值          | 描述                                                         |
| :--------- | :------- | :-------------- | :----------------------------------------------------------- |
| position   | String   | absolute        | 原生子窗体的排版位置，排版位置决定原生子窗体在父窗口中的定位方式。 可取值："static"，原生子窗体在页面中正常定位，如果页面存在滚动条则随窗口内容滚动；"absolute"，原生子窗体在页面中绝对定位，如果页面存在滚动条不随窗口内容滚动；"dock"，原生子窗体在页面中停靠，停靠的位置由dock属性值决定。 默认值为"absolute"。 |
| dock       | String   | bottom          | 原生子窗体的停靠方式,仅当原生子窗体 "position" 属性值设置为 "dock" 时才生效，可取值："top"，原生子窗体停靠则页面顶部；"bottom"，原生子窗体停靠在页面底部；"right"，原生子窗体停靠在页面右侧；"left"，原生子窗体停靠在页面左侧。 默认值为"bottom"。 |
| mask       | HexColor | rgba(0,0,0,0.5) | 原生子窗体的遮罩层,仅当原生子窗体 "type" 属性值设置为 "popup" 时才生效，可取值： rgba格式字符串，定义纯色遮罩层样式，如"rgba(0,0,0,0.5)"，表示黑色半透明； |
| width      | String   | 100%            | 原生子窗体的宽度,支持百分比、像素值，默认为100%。未设置width属性值时，可同时设置left和right属性值改变窗口的默认宽度。 |
| height     | String   | 100%            | 原生子窗体的高度,支持百分比、像素值，默认为100%。 当未设置height属性值时，优先通过top和bottom属性值来计算原生子窗体的高度。 |
| top        | String   | 0px             | 原生子窗体垂直向下的偏移量，支持百分比、像素值，默认值为0px。 未设置top属性值时，优先通过bottom和height属性值来计算原生子窗体的top位置。 |
| bottom     | String   |                 | 原生子窗体垂直向上偏移量,支持百分比、像素值，默认值无值（根据top和height属性值来自动计算）。 当同时设置了top和height值时，忽略此属性值； 当未设置height值时，可通过top和bottom属性值来确定原生子窗体的高度。 |
| left       | String   | 0px             | 原生子窗体水平向左的偏移量，支持百分比、像素值，默认值为0px。 未设置left属性值时，优先通过right和width属性值来计算原生子窗体的left位置。 |
| right      | String   |                 | 原生子窗体水平向右的偏移量，支持百分比、像素值，默认无值（根据left和width属性值来自动计算）。 当设置了left和width值时，忽略此属性值； 当未设置width值时，可通过left和bottom属性值来确定原生子窗体的宽度。 |
| margin     | String   |                 | 原生子窗体的边距，用于定位原生子窗体的位置，支持auto，auto表示居中。若设置了left、right、top、bottom则对应的边距值失效。 |
| zindex     | Number   |                 | 原生子窗体的窗口的堆叠顺序值，拥有更高堆叠顺序的窗口总是会处于堆叠顺序较低的窗口的前面，拥有相同堆叠顺序的窗口后调用show方法则在前面。 |
| background | String   | #FFFFFF         | 窗口的背景颜色,Android平台4.0以上系统才支持“transparent”背景透明样式。比如subnvue为圆角时需要设置为 |

```json
{
	"pages": [{
		"path": "pages/index/index", //首页
		"style": {
			"app-plus": {
				"titleNView": false , //禁用原生导航栏
				"subNVues":[{//侧滑菜单
					"id": "drawer", //subNVue 的 id，可通过 uni.getSubNVueById('drawer') 获取
					"path": "pages/index/drawer.nvue", // nvue 路径
					"style": { //webview style 子集，文档可暂时开放出来位置，大小相关配置
						"position": "popup", //除 popup 外，其他值域参考 5+ webview position 文档
						"width": "50%"
					}

				}, {//弹出层
					"id": "popup",
					"path": "pages/index/popup",
					"style": {
						"position": "popup",
						"margin":"auto",
						"width": "150px",
						"height": "150px"
					}

				}, {//自定义头
					"id": "nav",
					"path": "pages/index/nav",
					"style": {
						"position": "dock",
						"height": "44px"
					}

				}]
			}
		}
	}]
}
```



###### [1.3.1.3 下拉刷新](https://uniapp.dcloud.net.cn/collocation/pages.html#app-pulltorefresh)

* 在 App 平台下可以自定义部分下拉刷新的配置 `page->style->app-plus->pullToRefresh`。
* `enablePullDownRefresh` 与 `pullToRefresh->support` 同时设置时，后者优先级较高。
* 如果期望在 App 和小程序上均开启下拉刷新的话，请配置页面的 `enablePullDownRefresh` 属性为 true。
* 若仅期望在 App 上开启下拉刷新，则不要配置页面的 `enablePullDownRefresh` 属性，而是配置 `pullToRefresh->support` 为 true。
* 开启原生下拉刷新时，页面里不应该使用全屏高的scroll-view，向下拖动内容时，会优先触发下拉刷新而不是scroll-view滚动
* 原生下拉刷新的起始位置在原生导航栏的下方，如果取消原生导航栏，使用自定义导航栏，原生下拉刷新的位置会在屏幕顶部。如果希望在自定义导航栏下方拉动，只能使用circle方式的下拉刷新，并设置offset参数，将circle圈的起始位置调整到自定义导航栏下方。hello uni-app的扩展组件中有示例。
* 如果想在app端实现更多复杂的下拉刷新，比如美团、京东App那种拉下一个特殊图形，可以使用nvue的`<refresh>`组件。HBuilderX 2.0.3+起，新建项目选择新闻模板可以体验
* 如果想在vue页面通过web前端技术实现下拉刷新，插件市场有例子，但前端下拉刷新的性能不如原生，复杂长列表会很卡
* iOS上，default模式的下拉刷新和bounce回弹是绑定的，如果设置了bounce:none，会导致无法使用default下拉刷新

| 属性           | 类型    | 默认值                                      | 描述                                                         |
| :------------- | :------ | :------------------------------------------ | :----------------------------------------------------------- |
| support        | Boolean | false                                       | 是否开启窗口的下拉刷新功能                                   |
| color          | String  | #2BD009                                     | 颜色值格式为"#RRGGBB"，仅"circle"样式下拉刷新支持此属性。    |
| style          | String  | Android 平台为 circle；iOS 平台为 default。 | 可取值："default"——经典下拉刷新样式（下拉拖动时页面内容跟随）；"circle"——圆圈样式下拉刷新控件样式（下拉拖动时仅刷新控件跟随）。 |
| height         | String  |                                             | 窗口的下拉刷新控件进入刷新状态的拉拽高度。支持百分比，如"10%"；像素值，如"50px"，不支持rpx。 |
| range          | String  |                                             | 窗口可下拉拖拽的范围。支持百分比，如"10%"；像素值，如"50px"，不支持rpx。 |
| offset         | String  | 0px                                         | 下拉刷新控件的起始位置。仅对"circle"样式下拉刷新控件有效，用于定义刷新控件下拉时的起始位置。支持百分比，如"10%"；像素值，如"50px"，不支持rpx。如使用了非原生title且需要原生下拉刷新，一般都使用circle方式并将offset调至自定义title的高度 |
| contentdown    | Object  |                                             | 目前支持一个属性：caption——在下拉可刷新状态时下拉刷新控件上显示的标题内容。仅对"default"样式下拉刷新控件有效。 |
| contentover    | Object  |                                             | 目前支持一个属性：caption——在释放可刷新状态时下拉刷新控件上显示的标题内容。仅对"default"样式下拉刷新控件有效。 |
| contentrefresh | Object  |                                             | 目前支持一个属性：caption——在正在刷新状态时下拉刷新控件上显示的标题内容。仅对"default"样式下拉刷新控件有效。 |

```json
{
    "pages": [
        {
            "path": "pages/index/index", //首页
            "style": {
                "app-plus": {
                    "pullToRefresh": {
                        "support": true,
                        "color": "#ff3333",
                        "style": "default",
                        "contentdown": {
                            "caption": "下拉可刷新自定义文本"
                        },
                        "contentover": {
                            "caption": "释放可刷新自定义文本"
                        },
                        "contentrefresh": {
                            "caption": "正在刷新自定义文本"
                        }
                    }
                }
            }
        }
    ]
}
```



##### [1.3.2 h5](https://uniapp.dcloud.net.cn/collocation/pages.html#h5)

用到再看。



#### [1.4 tabBar](https://uniapp.dcloud.net.cn/collocation/pages.html#tabbar)

*	如果应用是一个多 tab 应用，可以通过 tabBar 配置项指定一级导航栏，以及 tab 切换时显示的对应页。

* 在 pages.json 中提供 tabBar 配置，不仅仅是为了方便快速开发导航，更重要的是在App和小程序端提升性能。在这两个平台，底层原生引擎在启动时无需等待js引擎初始化，即可直接读取 pages.json 中配置的 tabBar 信息，渲染原生tab。
* 当设置 position 为 top 时，将不会显示 icon
* tabBar 中的 list 是一个数组，只能配置最少2个、最多5个 tab，tab 按数组的顺序排序。
* tabbar 切换第一次加载时可能渲染不及时，可以在每个tabbar页面的onLoad生命周期里先弹出一个等待雪花（hello uni-app使用了此方式）
* tabbar 的页面展现过一次后就保留在内存中，再次切换 tabbar 页面，只会触发每个页面的onShow，不会再触发onLoad。
* 顶部的 tabbar 目前仅微信小程序上支持。需要用到顶部选项卡的话，建议不使用 tabbar 的顶部设置，而是自己做顶部选项卡，可参考 hello uni-app->模板->顶部选项卡。

| 属性            | 类型     | 必填 | 默认值 | 描述                                                         | 平台差异说明                                         |
| :-------------- | :------- | :--- | :----- | :----------------------------------------------------------- | :--------------------------------------------------- |
| color           | HexColor | 是   |        | tab 上的文字默认颜色                                         |                                                      |
| selectedColor   | HexColor | 是   |        | tab 上的文字选中时的颜色                                     |                                                      |
| backgroundColor | HexColor | 是   |        | tab 的背景色                                                 |                                                      |
| borderStyle     | String   | 否   | black  | tabbar 上边框的颜色，可选值 black/white，也支持其他颜色值    | App 2.3.4+ 、H5 3.0.0+                               |
| blurEffect      | String   | 否   | none   | iOS 高斯模糊效果，可选值 dark/extralight/light/none（参考:[使用说明](https://ask.dcloud.net.cn/article/36617)） | App 2.4.0+ 支持、H5 3.0.0+（只有最新版浏览器才支持） |
| list            | Array    | 是   |        | tab 的列表，详见 list 属性说明，最少2个、最多5个 tab         |                                                      |
| position        | String   | 否   | bottom | 可选值 bottom、top                                           | top 值仅微信小程序支持                               |
| fontSize        | String   | 否   | 10px   | 文字默认大小                                                 | App 2.3.4+、H5 3.0.0+                                |
| iconWidth       | String   | 否   | 24px   | 图标默认宽度（高度等比例缩放）                               | App 2.3.4+、H5 3.0.0+                                |
| spacing         | String   | 否   | 3px    | 图标和文字的间距                                             | App 2.3.4+、H5 3.0.0+                                |
| height          | String   | 否   | 50px   | tabBar 默认高度                                              | App 2.3.4+、H5 3.0.0+                                |
| midButton       | Object   | 否   |        | 中间按钮 仅在 list 项为偶数时有效                            | App 2.3.4+、H5 3.0.0+                                |
| iconfontSrc     | String   | 否   |        | list设置 iconfont 属性时，需要指定字体文件路径               | App 3.4.4+、H5 3.5.3+                                |

* 其中 list 接收一个数组，数组中的每个项都是一个对象，其属性值如下：

| 属性             | 类型    | 必填 | 说明                                                         | 平台差异                    |
| :--------------- | :------ | :--- | :----------------------------------------------------------- | :-------------------------- |
| pagePath         | String  | 是   | 页面路径，必须在 pages 中先定义                              |                             |
| text             | String  | 是   | tab 上按钮文字，在 App 和 H5 平台为非必填。例如中间可放一个没有文字的+号图标 |                             |
| iconPath         | String  | 否   | 图片路径，icon 大小限制为40kb，建议尺寸为 81px * 81px，当 position 为 top 时，此参数无效，不支持网络图片，不支持字体图标 |                             |
| selectedIconPath | String  | 否   | 选中时的图片路径，icon 大小限制为40kb，建议尺寸为 81px * 81px ，当 position 为 top 时，此参数无效 |                             |
| visible          | Boolean | 否   | 该项是否显示，默认显示                                       | App (3.2.10+)、H5 (3.2.10+) |
| iconfont         | Object  | 否   | 字体图标，优先级高于 iconPath                                | App（3.4.4+）、H5 (3.5.3+)  |

* midButton 属性说明
  * midButton没有pagePath，需监听点击事件，自行处理点击后的行为逻辑。监听点击事件为调用API：uni.onTabBarMidButtonTap，详见https://uniapp.dcloud.io/api/ui/tabbar?id=ontabbarmidbuttontap

| 属性            | 类型   | 必填 | 默认值 | 描述                                                         |
| :-------------- | :----- | :--- | :----- | :----------------------------------------------------------- |
| width           | String | 否   | 80px   | 中间按钮的宽度，tabBar 其它项为减去此宽度后平分，默认值为与其它项平分宽度 |
| height          | String | 否   | 50px   | 中间按钮的高度，可以大于 tabBar 高度，达到中间凸起的效果     |
| text            | String | 否   |        | 中间按钮的文字                                               |
| iconPath        | String | 否   |        | 中间按钮的图片路径                                           |
| iconWidth       | String | 否   | 24px   | 图片宽度（高度等比例缩放）                                   |
| backgroundImage | String | 否   |        | 中间按钮的背景图片路径                                       |
| iconfont        | Object | 否   |        | 字体图标，优先级高于 iconPath                                |

* iconfont参数说明:

| 属性          | 类型   | 说明                  |
| :------------ | :----- | :-------------------- |
| text          | String | 字库 Unicode 码       |
| selectedText  | String | 选中后字库 Unicode 码 |
| fontSize      | String | 字体图标字号(px)      |
| color         | String | 字体图标颜色          |
| selectedColor | String | 字体图标选中颜色      |



##### [1.4.1 tabbar常见问题](https://uniapp.dcloud.net.cn/collocation/pages.html#tips-tabbar)

* tabbar 的 js api 见[接口-界面-tabbar](https://uniapp.dcloud.io/api/ui/tabbar)，可实现动态显示隐藏（如弹出层无法覆盖tabbar）、内容修改（如国际化）、item加角标等功能。hello uni-app中也有示例。
* tabbar 的 item 点击事件见[页面生命周期的onTabItemTap](https://uniapp.dcloud.io/tutorial/page.html#lifecycle)。
* 代码跳转到 tabbar 页面，api只能使用[uni.switchTab](https://uniapp.dcloud.io/api/router?id=switchtab)，不能使用uni.navigateTo、uni.redirectTo；使用navigator组件跳转时必须设置[open-type="switchTab"](https://uniapp.dcloud.io/component/navigator)
* tabbar 的默认高度，在不同平台不一样。App端的默认高度在HBuilderX 2.3.4起从56px调整为50px，与H5端统一。开发者也可以自行设定高度，调回56px。[详见](https://uniapp.dcloud.io/tutorial/syntax-css.html#固定值)
* tabbar 在H5端是div模拟的，属于前端屏幕窗口的一部分，如果要使用bottom居底定位方式，应该使用css变量`--window-bottom`，比如悬浮在tabbar上方10px的按钮，样式如下`bottom: calc(var(--window-bottom) + 10px)`
* 中间带+号的tabbar模板例子，[参考](https://ext.dcloud.net.cn/plugin?id=98)。可跨端，但+号不凸起。如需中间凸起，配置tabbar的midButton。
* 如果是需要先登录、后进入tab页面，不需要把登录页设为首页，首页仍然是tabbar页，可参考[云端一体登录模板](https://ext.dcloud.net.cn/plugin?id=13)
* 前端弹出遮罩层挡不住tabbar的问题，跨端处理方式时动态隐藏tabbar。App端可以使用plus.nativeObj.view或subNVue做弹出和遮罩，可参考这个[底部原生图标分享菜单例子](https://ext.dcloud.net.cn/plugin?id=69)
* 微信小程序模拟器1.02.1904090版有bug，在缩放模拟器页面百分比后，tabbar点击多次后就会卡死。真机无碍，使用时注意。[详见](https://developers.weixin.qq.com/community/develop/doc/0002e6e6bf0d602d8c783e10756400)
* PC宽屏上，当页面存在topWindow或leftWindow或rightWindow等多窗体结构时，若想改变 tabbar 显示的位置，请使用 [custom-tab-bar组件](https://uniapp.dcloud.io/component/custom-tab-bar) 配置，若想隐藏 tabbar，可以使用如下 css（好处是可以和 leftwindow 等窗体联动）：



##### [1.4.2 自定义tabbar](https://uniapp.dcloud.net.cn/collocation/pages.html#custom-tab-bar)

原生tabBar是相对固定的配置方式，可能无法满足所有场景，这就涉及到自定义tabBar。

但注意除了H5端，自定义tabBar的性能体验会低于原生tabBar。App和小程序端非必要不要自定义。

- H5端的自定义tabBar组件：H5端不存在原生tabBar性能更高的概念，并且宽屏下常见的tabBar在顶部而不是底部，此时可以使用 [custom-tab-bar组件](https://uniapp.dcloud.io/component/custom-tab-bar) 来自定义
- 普通自定义tabBar：使用view自行绘制tabBar。如果页面是多页方式，切换tabBar将无法保持底部tabBar一直显示。所以这种情况建议使用单页方式。单页方式，如果是复杂页面，应用性能会下降明显，需减少页面复杂度。如果是App端，nvue单页的性能会显著高于vue页面
- 微信小程序自定义tabbar：微信提供一直基于webview自定义tabBar的方案。该功能体验不佳，不太推荐使用。如果要使用，参考[微信文档](https://developers.weixin.qq.com/miniprogram/dev/framework/ability/custom-tabbar.html)，项目根创建 custom-tab-bar 目录，注意里边的代码是 wxml,wxss，不是 vue，uni-app编译器会直接拷贝该目录到微信小程序中
- 原生的tabbar有且只有一个且在首页。二级页如需的tab，需自行编写view来实现。一般二级页面更适合的导航是 [segement组件](https://ext.dcloud.net.cn/plugin?id=54)



#### [1.5 condition](https://uniapp.dcloud.net.cn/collocation/pages.html#condition)

* 启动模式配置，仅开发期间生效，用于模拟直达页面的场景，如：小程序转发后，用户点击所打开的页面。

**属性说明：**

| 属性    | 类型   | 是否必填 | 描述                             |
| :------ | :----- | :------- | :------------------------------- |
| current | Number | 是       | 当前激活的模式，list节点的索引值 |
| list    | Array  | 是       | 启动模式列表                     |

**list说明：**

| 属性  | 类型   | 是否必填 | 描述                                                         |
| :---- | :----- | :------- | :----------------------------------------------------------- |
| name  | String | 是       | 启动模式名称                                                 |
| path  | String | 是       | 启动页面路径                                                 |
| query | String | 否       | 启动参数，可在页面的 [onLoad](https://uniapp.dcloud.net.cn/tutorial/page.html#lifecycle) 函数里获得 |

```json
"condition": { //模式配置，仅开发期间生效
	"current": 0, //当前激活的模式（list 的索引项）
	"list": [{
			"name": "swiper", //模式名称
			"path": "pages/component/swiper/swiper", //启动页面，必选
			"query": "interval=4000&autoplay=false" //启动参数，在页面的onLoad函数里面得到。
		},
		{
			"name": "test",
			"path": "pages/component/switch/switch"
		}
	]
}
```



[1.6 subPackages](subPackages)

分包加载配置，此配置为小程序的分包加载机制。

因小程序有体积和资源加载限制，各家小程序平台提供了分包方式，优化小程序的下载和启动速度。

所谓的主包，即放置默认启动页面/TabBar 页面，以及一些所有分包都需用到公共资源/JS 脚本；而分包则是根据pages.json的配置进行划分。

在小程序启动时，默认会下载主包并启动主包内页面，当用户进入分包内某个页面时，会把对应分包自动下载下来，下载完成后再进行展示。此时终端界面会有等待提示。

App默认为整包。从uni-app 2.7.12+ 开始，也兼容了小程序的分包配置。其目的不用于下载提速，而用于首页是vue时的启动提速。App下开启分包，除在pages.json中配置分包规则外，还需要在manifest中设置在app端开启分包设置，详见：https://uniapp.dcloud.io/collocation/manifest?id=app-vue-optimization

subPackages 节点接收一个数组，数组每一项都是应用的子包，其属性值如下：

| 属性  | 类型   | 是否必填 | 描述                                                         |
| :---- | :----- | :------- | :----------------------------------------------------------- |
| root  | String | 是       | 子包的根目录                                                 |
| pages | Array  | 是       | 子包由哪些页面组成，参数同 [pages](https://uniapp.dcloud.net.cn/collocation/pages.html#pages) |

**注意：**

- `subPackages` 里的pages的路径是 `root` 下的相对路径，不是全路径。
- 微信小程序每个分包的大小是2M，总体积一共不能超过20M。
- 百度小程序每个分包的大小是2M，总体积一共不能超过8M。
- 支付宝小程序每个分包的大小是2M，总体积一共不能超过8M。
- QQ小程序每个分包的大小是2M，总体积一共不能超过24M。
- 字节小程序每个分包的大小是2M，总体积一共不能超过16M（字节小程序基础库 1.88.0 及以上版本开始支持，字节小程序开发者工具请使用大于等于 2.0.6 且小于 3.0.0 的版本）。
- 快手小程序每个分包的大小是2M，总体积一共不能超过24M。
- 分包下支持独立的 `static` 目录，用来对静态资源进行分包。
- `uni-app`内支持对`微信小程序`、`QQ小程序`、`百度小程序`、`支付宝小程序`、`字节小程序(HBuilderX 3.0.3+)`、`快手小程序`分包优化，即将静态资源或者js文件放入分包内不占用主包大小。详情请参考：[关于分包优化的说明](https://uniapp.dcloud.net.cn/collocation/manifest#关于分包优化的说明)
- 针对vendor.js过大的情况可以使用运行时压缩代码
  - `HBuilderX`创建的项目勾选`运行-->运行到小程序模拟器-->运行时是否压缩代码`
  - `cli`创建的项目可以在`package.json`中添加参数`--minimize`，示例：`"dev:mp-weixin": "cross-env NODE_ENV=development UNI_PLATFORM=mp-weixin vue-cli-service uni-build --watch --minimize"`

**使用方法：**

假设支持分包的 `uni-app` 目录结构如下：

```
┌─pages
│  ├─index
│  │  └─index.vue
│  └─login
│     └─login.vue
├─pagesA
│  ├─static
│  └─list
│     └─list.vue
├─pagesB
│  ├─static
│  └─detail
│     └─detail.vue
├─static
├─main.js
├─App.vue
├─manifest.json
└─pages.json
```

则需要在 pages.json 中填写

```javascript
{
	"pages": [{
		"path": "pages/index/index",
		"style": { ...}
	}, {
		"path": "pages/login/login",
		"style": { ...}
	}],
	"subPackages": [{
		"root": "pagesA",
		"pages": [{
			"path": "list/list",
			"style": { ...}
		}]
	}, {
		"root": "pagesB",
		"pages": [{
			"path": "detail/detail",
			"style": { ...}
		}]
	}],
	"preloadRule": {
		"pagesA/list/list": {
			"network": "all",
			"packages": ["__APP__"]
		},
		"pagesB/detail/detail": {
			"network": "all",
			"packages": ["pagesA"]
		}
	}
}
```

#### [1.6 preloadRule](https://uniapp.dcloud.net.cn/collocation/pages.html#preloadrule)

用到再看。



### [2. manifest.json 应用配置](https://uniapp.dcloud.net.cn/collocation/manifest.html#)

`manifest.json` 文件是应用的配置文件，用于指定应用的名称、图标、权限等。HBuilderX 创建的工程此文件在根目录，CLI 创建的工程此文件在 src 目录。

* 配置项列表

| 属性           | 类型    | 默认值                                                       | 描述                                                         | 最低版本 |
| :------------- | :------ | :----------------------------------------------------------- | :----------------------------------------------------------- | :------- |
| name           | String  |                                                              | 应用名称                                                     |          |
| appid          | String  | 新建 uni-app 项目时，DCloud 云端分配。用途[详见](https://ask.dcloud.net.cn/article/35907) | 应用标识                                                     |          |
| description    | String  |                                                              | 应用描述                                                     |          |
| locale         | String  | auto                                                         | 设置当前默认语言，具体参考 [locale](https://uniapp.dcloud.net.cn/api/ui/locale) |          |
| versionName    | String  |                                                              | 版本名称，例如：1.0.0。详见下方Tips说明                      |          |
| versionCode    | Number  |                                                              | 版本号，例如：36                                             |          |
| transformPx    | Boolean | true                                                         | 是否转换项目的px，为true时将px转换为rpx，为false时，px为传统的实际像素。为兼容历史项目默认值为 true，但不推荐新项目启用此配置（新建项目模板一般配置为 false） |          |
| networkTimeout | Object  |                                                              | 网络超时时间，[详见](https://uniapp.dcloud.net.cn/collocation/manifest#networktimeout) |          |
| debug          | Boolean | false                                                        | 是否开启 debug 模式，开启后调试信息以 `info` 的形式给出，其信息有页面的注册，页面路由，数据更新，事件触发等 |          |
| uniStatistics  | Object  |                                                              | [是否开启 uni 统计，全局配置](https://uniapp.dcloud.net.cn/collocation/manifest#uniStatistics) | 2.2.3+   |
| app-plus       | Object  |                                                              | [App 特有配置](https://uniapp.dcloud.net.cn/collocation/manifest#app-plus) |          |
| h5             | Object  |                                                              | [H5 特有配置](https://uniapp.dcloud.net.cn/collocation/manifest#h5) |          |
| quickapp       | Object  |                                                              | 快应用特有配置，即将支持                                     |          |
| mp-weixin      | Object  |                                                              | [微信小程序特有配置](https://uniapp.dcloud.net.cn/collocation/manifest#mp-weixin) |          |
| mp-alipay      | Object  |                                                              | [支付宝小程序特有配置](https://uniapp.dcloud.net.cn/collocation/manifest#mp-alipay) |          |
| mp-baidu       | Object  |                                                              | [百度小程序特有配置](https://uniapp.dcloud.net.cn/collocation/manifest#mp-baidu) |          |
| mp-toutiao     | Object  |                                                              | [字节跳动小程序特有配置](https://uniapp.dcloud.net.cn/collocation/manifest#mp-toutiao) | 1.6.0    |
| mp-lark        | Object  |                                                              | [飞书小程序特有配置](https://uniapp.dcloud.net.cn/collocation/manifest#mp-lark) | 3.2.12   |
| mp-qq          | Object  |                                                              | [qq 小程序特有配置](https://uniapp.dcloud.net.cn/collocation/manifest#mp-qq) | 2.1.0    |
| mp-kuaishou    | Object  |                                                              | [快手小程序特有配置](https://uniapp.dcloud.net.cn/collocation/manifest.html#mp-kuaishou) | 3.2.2    |



#### [2.1 networkTimeout](https://uniapp.dcloud.net.cn/collocation/manifest.html#networktimeout)

各类网络请求的超时时间，单位均为毫秒。

| 属性          | 类型   | 必填 | 默认值 | 说明                                     |
| ------------- | ------ | ---- | ------ | ---------------------------------------- |
| request       | Number | 否   | 60000  | uni.request 的超时时间，单位毫秒。       |
| connectSocket | Number | 否   | 60000  | uni.connectSocket 的超时时间，单位毫秒。 |
| uploadFile    | Number | 否   | 60000  | uni.uploadFile 的超时时间，单位毫秒。    |
| downloadFile  | Number | 否   | 60000  | uni.downloadFile 的超时时间，单位毫秒。  |



#### [2.2 uniStatistics](https://uniapp.dcloud.net.cn/collocation/manifest.html#unistatistics)

* uni 统计配置项

| 属性   | 类型    | 必填 | 默认值 | 说明            |
| ------ | ------- | ---- | ------ | --------------- |
| enable | Boolean | 是   | true   | 是否开启uni统计 |



#### [2.3 app-plus](https://uniapp.dcloud.net.cn/collocation/manifest.html#app-plus)

| 属性              | 类型   | 说明                                                         | 最低版本        |
| :---------------- | :----- | :----------------------------------------------------------- | :-------------- |
| splashscreen      | Object | App 启动界面信息，[详见](https://uniapp.dcloud.net.cn/collocation/manifest#splashscreen) |                 |
| screenOrientation | Array  | 重力感应、横竖屏配置，可取值："portrait-primary"：竖屏正方向；"portrait-secondary"：竖屏反方向；"landscape-primary"：横屏正方向；"landscape-secondary"：横屏反方向。 |                 |
| modules           | Object | 权限模块，[详见](https://uniapp.dcloud.net.cn/collocation/manifest#modules) |                 |
| distribute        | Object | App 发布信息，[详见](https://uniapp.dcloud.net.cn/collocation/manifest#distribute) |                 |
| nvueCompiler      | String | 切换 nvue 编译模式，可选值，`weex` ：老编译模式，`uni-app`： 新编译模式，默认为 `weex` 。[编译模式区别详情](http://ask.dcloud.net.cn/article/36074) | 2.0.3+          |
| nvueStyleCompiler | String | 切换 nvue 样式编译模式，可选值，`weex` ：老编译模式，`uni-app`： 新编译模式，默认为 `weex` 。[编译模式区别详情](https://ask.dcloud.net.cn/article/38751) | 3.1.1+          |
| renderer          | String | 可不加载基于 webview 的运行框架，减少包体积、提升启动速度。可选值 `native` | App-nvue 2.2.0+ |
| nvueLaunchMode    | String | Nvue 首页启动模式，可选值：normal、fast 默认 normal（HBuilderX 2.4.4-2.4.9 固定为 fast） [详见](https://ask.dcloud.net.cn/article/36749) | 2.5.0+          |
| nvue              | Object | nvue 页面布局初始配置，[详见](https://uniapp.dcloud.net.cn/collocation/manifest#nvue) | 2.0.3+          |
| optimization      | Object | 分包配置，可以减轻启动时加载的js数量，提升启动速度           | 2.7.12+         |
| runmode           | String | normal：默认模式，liberate：资源释放模式                     |                 |
| uniStatistics     | Object | [App 是否开启 uni 统计，配置方法同全局配置](https://uniapp.dcloud.net.cn/collocation/manifest#uniStatistics) | 2.2.3+          |
| webView           | Object | 当系统webview低于指定版本时，会弹出提示。或者下载x5内核后继续启动，仅Android支持，[详情](https://uniapp.dcloud.net.cn/collocation/manifest#appwebview) | 3.5.0+          |

PS：上表只列出了核心部分，App平台的配置其实非常多，完整内容请参考 [完整的 manifest.json](https://uniapp.dcloud.net.cn/collocation/manifest-app#full-manifest)。

- manifest.json 文件的配置，推荐在 HBuilderX 提供的可视化操作界面完成。
- 部分配置在打包时的操作界面补全，例如：证书等信息。
- Native.js 权限部分会根据配置的模块权限，在打包后自动填充。
- 部分 modules 是默认的，不需要进行配置。
- 微信小程序的 `appid` 等信息，需要配置在 `mp-weixin` 节点下。不要配置在 `app-plus`下。`sdkConfigs` 下出现的 `weixin` 节点，配置的是 App 的第三方 SDK 信息。



##### [2.3.1 App Splashscreen](https://uniapp.dcloud.net.cn/collocation/manifest.html#splashscreen)

splash（启动封面）是App必然存在的、不可取消的。

| 属性                   | 类型    | 默认值 | 描述                                                         | 最低版本 |
| :--------------------- | :------ | :----- | :----------------------------------------------------------- | :------- |
| alwaysShowBeforeRender | Boolean | true   | 是否等待首页渲染完毕后再关闭启动界面                         | 1.6.0    |
| autoclose              | Boolean | true   | 是否自动关闭启动界面，仅当alwaysShowBeforeRender设置为false时生效，如果需要[手动关闭](https://www.html5plus.org/doc/zh_cn/navigator.html#plus.navigator.closeSplashscreen)启动界面，需将 alwaysShowBeforeRender 及 autoclose 均设置为 false。 |          |
| waiting                | Boolean | true   | 是否在程序启动界面显示等待圈或雪花                           |          |

* alwaysShowBeforeRender和autoclose属性组合设置，可配置以下三种关闭启动界面（splash）策略，[详见](https://uniapp.dcloud.net.cn/tutorial/app-splashscreen)

- 如果不配置自己的splash图，App端会默认把App的icon放到splash中
- splash只能是标准png，不要用jpg改名为png。也不支持gif等动画
- 相关改动，云打包生效，真机运行不生效。本地打包需自行在原生工程中配置
- App启动图中iOS的MAX等大屏设备的splash图若不配，会导致iOS认为此App没有为MAX优化，App将无法全屏，四周会有黑边
- Android的splash支持.9.png，[详见](https://uniapp.dcloud.net.cn/tutorial/app-splashscreen#9png)



##### [2.3.2 App Modules](https://uniapp.dcloud.net.cn/collocation/manifest.html#modules)

模块选择是为了控制App的包体积，不需要的模块可以在打包时剔除。

| 名称        | 描述         |
| :---------- | :----------- |
| Bluetooth   | BLE蓝牙      |
| Contacts    | 系统通讯录   |
| Fingerprint | 指纹识别     |
| iBeacon     | iBeacon      |
| LivePusher  | 直播推流     |
| Maps        | 地图         |
| Messaging   | 短彩邮件消息 |
| OAuth       | 登录授权     |
| Payment     | 支付         |
| Push        | 消息推送     |
| Share       | 社交分享     |
| Speech      | 语音识别     |
| SQLite      | SQLite数据库 |
| Statistic   | 统计         |
| VideoPlayer | 视频播放     |



##### [2.3.3 App Distribute](https://uniapp.dcloud.net.cn/collocation/manifest.html#distribute)

| 属性        | 类型   | 描述                                                         |
| :---------- | :----- | :----------------------------------------------------------- |
| android     | Object | Android 应用配置，详见: [Android配置明细](https://uniapp.dcloud.net.cn/collocation/manifest-app#android) |
| ios         | Object | iOS 应用配置，详见: [iOS配置明细](https://uniapp.dcloud.net.cn/collocation/manifest-app#ios) |
| sdkConfigs  | Object | SDK配置，仅打包生效 [详见](https://uniapp.dcloud.net.cn/collocation/manifest#sdkConfigs) |
| orientation | Array  | 同 screenOrientation 配置，仅打包生效，已废弃，推荐使用 screenOrientation |



[2.3.4 App SdkConfigs](https://uniapp.dcloud.net.cn/collocation/manifest.html#sdkconfigs)

| 属性    | 类型   | 描述                                                         |
| :------ | :----- | :----------------------------------------------------------- |
| oauth   | Object | 授权登录，配置后可调用 [uni.login](https://uniapp.dcloud.net.cn/api/plugins/login#login) 进行登录操作，目前支持的授权登录平台有：[QQ](http://open.qq.com/)、[微信](https://open.weixin.qq.com/)、[新浪微博](http://open.weibo.com/)。 |
| share   | Object | 分享，配置后可调用 [uni.share](https://uniapp.dcloud.net.cn/api/plugins/share#share) 进行分享，目前支持QQ、微信、新浪微博等分享， 具体配置 [详见](https://uniapp.dcloud.net.cn/api/plugins/share#app-端各平台分享配置说明)。 |
| push    | Object | push配置，使用方式 [详见](https://uniapp.dcloud.net.cn/unipush)，目前支持：[uniPush](http://ask.dcloud.net.cn/article/35716)、[个推](http://www.igetui.com/)，注意App仅支持一种 push 方式，配置多个 push 无效，建议使用 uniPush，支持多厂商推送。 |
| payment | Object | 三方支付配置，配置后可调用 [uni.payment](https://uniapp.dcloud.net.cn/api/plugins/payment#payment) 进行支付，目前支持微信支付、支付宝支付、苹果内购， 具体配置 [详见](https://uniapp.dcloud.net.cn/api/plugins/payment#uni-app-app-平台支付流程)。 |
| statics | Object | 统计配置，目前仅支付友盟统计，[详见](https://uniapp.dcloud.net.cn/tutorial/app-statistic)，在uni-app中只用 [plus.statistic](http://www.html5plus.org/doc/zh_cn/statistic.html) 进行调用。 |
| speech  | Object | 语音识别配置，支持讯飞语音、百度语音，[详见](https://uniapp.dcloud.net.cn/tutorial/app-speech)，在uni-app中只用 [plus.speech](http://www.html5plus.org/doc/zh_cn/speech.html) 进行调用。 |
| maps    | Object | 原生地图配置，目前仅支持 [高德地图](http://lbs.amap.com/)，申请方式可参考：[地图插件配置](https://uniapp.dcloud.net.cn/tutorial/app-maps)。 |



##### [2.3.4 optimization](https://uniapp.dcloud.net.cn/collocation/manifest.html#app-vue-optimization)

可以减轻启动时加载的js数量，提升启动速度。

从uni-app 2.7.12+ 开始，App-vue平台也兼容了小程序的分包配置，但默认并不开启。

在manifest配置以下节点，可以在App端启动分包。

| 属性        | 类型    | 说明             |
| :---------- | :------ | :--------------- |
| subPackages | Boolean | 是否开启分包优化 |

```json
"app-plus": {
  "optimization": {
    "subPackages": true
  },
  "runmode" : "liberate" // 开启分包优化后，必须配置资源释放模式
}
```

在manifest中启动分包后，需要在pages.json中配置具体的分包规则，与小程序的配置相同，详见：https://uniapp.dcloud.io/collocation/pages?id=subpackages

也就是一旦在pages.json里配置分包，小程序一定生效，而app是否生效，取决于manifest里是否开启。

注意:

- App开启分包后，每个分包单独编译成一个js文件(都包含在app内，不会联网下载)，当App首页是vue时，可减小启动加载文件大小，提升启动速度。
- 首页是nvue时，分包不会提升启动速度，nvue本身启动速度就快于vue，也快于开启分包后的首页为vue的应用。如果追求极致启动速度，还是应该使用nvue做首页并在manifest开启fast模式。
- App页面较少时，分包对启动速度的优化不明显。



##### [2.3.5 nvue](https://uniapp.dcloud.net.cn/collocation/manifest.html#nvue)

`nvue` 页面布局初始设置

| 属性           | 类型   | 描述                                                         |
| :------------- | :----- | :----------------------------------------------------------- |
| flex-direction | String | flex 成员项的排列方向，支持项，row：从左到右； row-reverse：从右到左；column：从上到下；column-reverse：与 column 相反，默认值 column。 |



##### [2.3.6 webview](https://uniapp.dcloud.net.cn/collocation/manifest.html#appwebview)

当App代码使用了低版本webview不支持的语法时（比如使用了vue3），可以在manifest配置本属性，来指定最低运行的webview版本。

当系统webview版本不符合需求时，uni-app引擎会自动弹框。同时开发者可以指定使用 x5引擎webview 来替代系统webview，以保障浏览器兼容性。详见[x5文档](https://uniapp.dcloud.net.cn/tutorial/app-android-x5.html)

当你的应用强依赖x5时，比如需要vue页面的字体和tabbar等原生界面保持一致时，也可以在manifest配置本属性。

| 属性                | 类型   | 说明                                                         |
| :------------------ | :----- | :----------------------------------------------------------- |
| minUserAgentVersion | String | 最小webview版本，例如：64.0.3282.116。（当低于最小版本要求时，显示 `WebView版本过低` 弹框，点击确定退出应用。） |
| x5                  | Object | 此属性需要在manifest模块配置中勾选 Android X5 Webview 模块，详细参见下面的说明 |

x5 属性说明

| 属性                     | 类型    | 默认值 | 说明                                                         |
| :----------------------- | :------ | :----- | :----------------------------------------------------------- |
| timeOut                  | Number  | 3000   | 超时时间                                                     |
| showTipsWithoutWifi      | Boolean | false  | 是否在非WiFi网络环境时，显示用户确认下载x5内核的弹窗。（如果为true时，在非WiFi网络下载x5模块，会显示用户确认弹框，内容为 `当前处于非WiFi网络，是否允许下载x5模块？` ，false时不显示弹框 。） |
| allowDownloadWithoutWiFi | Boolean | false  | 是否允许用户在非WiFi网络时进行x5内核的下载。（如果为true，就不会显示用户确认的弹窗。false时，如果showTipsWithoutWifi为true，就会显示用户确认弹框；showTipsWithoutWifi为false时，不下载x5模块。） |

```json
{
  "app-plus" : {
    "webView": {
      "minUserAgentVersion": "64.0.3282.116",
      "x5": {
        "timeOut": 3000,
        "showTipsWithoutWifi": true,
        "allowDownloadWithoutWiFi": false
      }
    }
  }
}

```



#### [2.4 h5](https://uniapp.dcloud.net.cn/collocation/manifest.html#h5)

用到再看。



#### [2.5 mp-weixin](https://uniapp.dcloud.net.cn/collocation/manifest.html#mp-weixin)

用到再看。



#### [2.6 mp-alipay](https://uniapp.dcloud.net.cn/collocation/manifest.html#mp-alipay)

用到再看。



#### [2.7 mp-baidu](https://uniapp.dcloud.net.cn/collocation/manifest.html#mp-baidu)

用到再看。



#### [2.8 mp-toutiao](https://uniapp.dcloud.net.cn/collocation/manifest.html#mp-toutiao)

用到再看。



#### [2.9 mp-lark](https://uniapp.dcloud.net.cn/collocation/manifest.html#mp-lark)

用到再看。



#### [2.10 mp-qq](https://uniapp.dcloud.net.cn/collocation/manifest.html#mp-qq)

用到再看。



#### [2.11 mp-kuaishou](https://uniapp.dcloud.net.cn/collocation/manifest.html#mp-kuaishou)

用到再看。



#### [2.12 完整 manifest.json](https://uniapp.dcloud.net.cn/collocation/manifest-app.html#full-manifest)

```json
{
    "appid": "__UNI__XXXXXX，创建应用时云端分配的，不要修改。",
    "name": "应用名称，如uni-app",
    "description": "应用描述",
    "versionName": "1.0.0",
    "versionCode": "100",
    "uniStatistics": {
        "enable": false
    },
    "app-plus": {
        "nvueCompiler": "weex",         //可选，字符串类型，nvue页面编译模式，可取值uni-app、weex，参考：https://ask.dcloud.net.cn/article/36074
        "nvueStyleCompiler": "weex",    //可选，字符串类型，nvue页面样式编译模式，可取值uni-app、weex，参考：https://ask.dcloud.net.cn/article/38751
        "renderer": "native",           //可选，字符串类型，可不加载基于 webview 的运行框架，可取值native
        "compilerVersion": 2,           //可选，数字类型，编译器版本，可取值2、3，参考：https://ask.dcloud.net.cn/article/36599
        "nvueLaunchMode": "normal",     //可选，字符串类型，nvue首页启动模式，compilerVersion值为3时生效，可取值normal、fast，参考：https://ask.dcloud.net.cn/article/36749
        "nvue": {                       //可选，JSON对象，nvue页面相关配置
            "flex-direction": "row"             //可选，字符串类型，nvue页面的flex-direction默认值，可取值row、row-reverse、column、column-reverse
        },
        "optimization": {               //可选，JSON对象，分包配置
            "subPackages": true                 //可选，Boolean类型，是否开启分包优化，参考：https://uniapp.dcloud.io/collocation/pages.html#subpackages
        },
        "uniStatistics": {              //可选，JSON对象，uni统计配置
            "enable": true,                     //可选，Boolean类型，是否开启uni统计
        },
        "screenOrientation": [          //可选，字符串数组类型，应用支持的横竖屏
            "portrait-primary",                 //可选，字符串类型，支持竖屏
            "portrait-secondary",               //可选，字符串类型，支持反向竖屏
            "landscape-primary",                //可选，字符串类型，支持横屏
            "landscape-secondary"               //可选，字符串类型，支持反向横屏
        ],
        "splashscreen": {               //可选，JSON对象，splash界面配置
            "alwaysShowBeforeRender": true,     //可选，Boolean类型，是否等待首页渲染完毕后再关闭启动界面
            "autoclose": true,                  //可选，Boolean类型，是否自动关闭启动界面
            "waiting": true,                    //可选，Boolean类型，是否在程序启动界面显示等待雪花
            "event": "loaded",                  //可选，字符串类型，可取值titleUpdate、rendering、loaded，uni-app项目已废弃
            "target": "defalt",                 //可选，字符串类型，可取值default、second，uni-app项目已废弃
            "dealy": 0,                         //可选，数字类型，延迟自动关闭启动时间，单位为毫秒，uni-app项目已废弃
            "ads": {                            //可选，JSON对象，开屏广告配置
                "backaground": "#RRGGBB",               //可选，字符串类型，格式为#RRGGBB，开屏广告背景颜色
                "image": ""                             //可选，字符串类型，底部图片地址，相对应用资源目录路径
            },
            "androidTranslucent": false         //可选，Boolean类型，使用“自定义启动图”启动界面时是否显示透明过渡界面，可解决点击桌面图标延时启动应用的效果
        },
        "modules": {                    //可选，JSON对象，使用的模块
            "Bluetooth": {                      //可选，JSON对象，Bluetooth(低功耗蓝牙)
                "description": "低功耗蓝牙"
            },
            "Contacts": {                       //可选，JSON对象，Contact(通讯录)
                "description": "通讯录"
            },
            "FaceID": {                         //可选，JSON对象，FaceID(人脸识别)，仅iOS支持
                "description": "人脸识别"
            },
            "Fingerprint": {                    //可选，JSON对象，Fingerprint(指纹识别)
                "description": "指纹识别"
            },
            "Geolocation": {                    //可选，JSON对象，Geolocation(定位)
                "description": "定位"
            },
            "iBeacon": {                        //可选，JSON对象，iBeacon
                "description": "iBeacon"
            },
            "LivePusher": {                     //可选，JSON对象，LivePusher(直播推流)
                "description": "直播推流"
            },
            "Maps": {                           //可选，JSON对象，Maps(地图)
                "description": "地图"
            },
            "Messaging": {                      //可选，JSON对象，Messaging(短彩邮件消息)
                "description": "短彩邮件消息"
            },
            "OAuth": {                          //可选，JSON对象，OAuth(登录鉴权)
                "description": "登录鉴权"
            },
            "Payment": {                        //可选，JSON对象，Payment(支付)
                "description": "iBeacon"
            },
            "Push": {                           //可选，JSON对象，Push(消息推送)
                "description": "iBeacon"
            },
            "Share": {                          //可选，JSON对象，Share(分享)
                "description": "iBeacon"
            },
            "Speech": {                         //可选，JSON对象，Speech(语音输入)
                "description": "iBeacon"
            },
            "Statistic": {                      //可选，JSON对象，Statistic(统计)
                "description": "iBeacon"
            },
            "SQLite": {                         //可选，JSON对象，SQLite(统计)
                "description": "iBeacon"
            },
            "VideoPlayer": {                    //可选，JSON对象，VideoPlayer(视频播放)
                "description": "iBeacon"
            },
            "Webview-x5": {                     //可选，JSON对象，Android X5 Webview(腾讯TBS)，仅Android支持
                "description": "iBeacon"
            },
            "UIWebview": {                      //可选，JSON对象，UIWebview，仅iOS支持
                "description": "iBeacon"
            }
        },
        "webView": { // 3.5.0 + 当系统webview低于指定版本时，会弹出提示。或者下载x5内核后继续启动，仅Android支持
          "minUserAgentVersion": "95.0.4638.75", // 最小webview版本
          "x5": { // 此属性需要勾选 Android X5 Webview 模块，详细参见下面的说明
            "timeOut": 3000, // 超时时间
            "showTipsWithoutWifi": true, // 是否在非WiFi网络环境时，显示用户确认下载x5内核的弹窗。
            "allowDownloadWithoutWiFi": false // 是否允许用户在非WiFi网络时进行x5内核的下载。（如果为true，就不会显示用户确认的弹窗。）
          }
        },
		"checkPermissionDenied": false, // 是否校验已拒绝权限 如果拒绝则不会再申请 默认false 不校验已拒绝权限
        "distribute": {      //必选，JSON对象，云端打包配置
            "android": {            //可选，JSON对象，Android平台云端打包配置
                "packagename": "",          //必填，字符串类型，Android包名
                "keystore": "",             //必填，字符串类型，Android签名证书文件路径
                "password": "",             //必填，字符串类型，Android签名证书文件的密码
                "aliasname": "",            //必填，字符串类型，Android签名证书别名
                "schemes": "",              //可选，字符串类型，参考：https://uniapp.dcloud.io/tutorial/app-android-schemes
                "abiFilters": [             //可选，字符串数组类型，参考：https://uniapp.dcloud.io/tutorial/app-android-abifilters
                    "armeabi-v7a",
                    "arm64-v8a",
                    "x86",
                    "x86_64"
                ],
                "permissions": [                //可选，字符串数组类型，Android权限配置
                    "<uses-feature android:name=\"android.hardware.camera\"/>"
                ],
                "custompermissions": false,     //可选，Boolean类型，是否自定义Android权限配置
                "permissionExternalStorage": {  //可选，JSON对象，Android平台应用启动时申请读写手机存储权限策略
                    "request": "always",                //必填，字符串类型，申请读写手机存储权限策略，可取值none、once、always
                    "prompt": ""                        //可选，字符串类型，当request设置为always值用户拒绝时弹出提示框上的内容
                },
                "permissionPhoneState": {       //可选，JSON对象，Android平台应用启动时申请读取设备信息权限配置
                    "request": "always",                //必填，字符串类型，申请读取设备信息权限策略，可取值none、once、always
                    "prompt": ""                        //可选，字符串类型，当request设置为always值用户拒绝时弹出提示框上的内容
                },
                "minSdkVersion": 21,            //可选，数字类型，Android平台最低支持版本，参考：https://uniapp.dcloud.io/tutorial/app-android-minsdkversion
                "targetSdkVersion": 30,         //可选，数字类型，Android平台目标版本，参考：https://uniapp.dcloud.io/tutorial/app-android-targetsdkversion
                "packagingOptions": [           //可选，字符串数组类型，Android平台云端打包时build.gradle的packagingOptions配置项
                    "doNotStrip '*/armeabi-v7a/*.so'",
                    "merge '**/LICENSE.txt'"
                ],
                "jsEngine": "v8",               //可选，字符串类型，uni-app使用的JS引擎，可取值v8、jsc
                "debuggable": false,            //可选，Boolean类型，是否开启Android调试开关
                "locale": "default",            //可选，应用的语言
                "forceDarkAllowed": false,      //可选，Boolean类型，是否强制允许暗黑模式
                "resizeableActivity": false,    //可选，Boolean类型，是否支持分屏调整窗口大小
                "hasTaskAffinity": false,       //可选，Boolean类型，是否设置android：taskAffinity
                "buildFeatures": {              //（HBuilderX3.5.0+版本支持）可选，JSON对象，Android平台云端打包时build.gradle的buildFeatures配置项  
                    "dataBinding": false,           //可选，Boolean类型，是否设置dataBinding
                    "viewBinding": false            //可选，Boolean类型，是否设置viewBinding
                }
            },
            "ios": {                //可选，JSON对象，iOS平台云端打包配置
                "appid": "",                    //必填，字符串类型，iOS平台Bundle ID
                "mobileprovision": "",          //必填，字符串类型，iOS打包使用的profile文件路径
                "p12": "",                      //必填，字符串类型，iOS打包使用的证书文件路径
                "password": "",                 //必填，字符串类型，iOS打包使用的证书密码
                "devices": "iphone",            //必填，字符串类型，iOS支持的设备类型，可取值iphone、ipad、universal
                "urlschemewhitelist": "baidumap",//可选，字符串类型，应用访问白名单列表，参考：https://uniapp.dcloud.io/tutorial/app-ios-schemewhitelist
                "urltypes": "",                 //可选，字符串类型，参考：https://uniapp.dcloud.io/tutorial/app-ios-schemes
                "UIBackgroundModes": "audio",   //可选，字符串类型，应用后台运行模式，参考：https://uniapp.dcloud.io/tutorial/app-ios-uibackgroundmodes
                "frameworks": [                 //可选，字符串数组类型，依赖的系统库，已废弃，推荐使用uni原生插件扩展使用系统依赖库
                    "CoreLocation.framework"
                ],
                "deploymentTarget": "10.0",     //可选，字符串类型，iOS支持的最低版本
                "privacyDescription": {         //可选，JSON对象，iOS隐私信息访问的许可描述
                    "NSPhotoLibraryUsageDescription": "",                       //可选，字符串类型，系统相册读取权限描述
                    "NSPhotoLibraryAddUsageDescription": "",                    //可选，字符串类型，系统相册写入权限描述
                    "NSCameraUsageDescription": "",                             //可选，字符串类型，摄像头使用权限描述
                    "NSMicrophoneUsageDescription": "",                         //可选，字符串类型，麦克风使用权限描述
                    "NSLocationWhenInUseUsageDescription": "",                  //可选，字符串类型，运行期访问位置权限描述
                    "NSLocationAlwaysUsageDescription": "",                     //可选，字符串类型，后台运行访问位置权限描述
                    "NSLocationAlwaysAndWhenInUseUsageDescription": "",         //可选，字符串类型，运行期后后台访问位置权限描述
                    "NSCalendarsUsageDescription": "",                          //可选，字符串类型，使用日历权限描述
                    "NSContactsUsageDescription": "",                           //可选，字符串类型，使用通讯录权限描述
                    "NSBluetoothPeripheralUsageDescription": "",                //可选，字符串类型，使用蓝牙权限描述
                    "NSBluetoothAlwaysUsageDescription": "",                    //可选，字符串类型，后台使用蓝牙权限描述
                    "NSSpeechRecognitionUsageDescription": "",                  //可选，字符串类型，系统语音识别权限描述
                    "NSRemindersUsageDescription": "",                          //可选，字符串类型，系统提醒事项权限描述
                    "NSMotionUsageDescription": "",                             //可选，字符串类型，使用运动与健康权限描述
                    "NSHealthUpdateUsageDescription": "",                       //可选，字符串类型，使用健康更新权限描述
                    "NSHealthShareUsageDescription": "",                        //可选，字符串类型，使用健康分享权限描述
                    "NSAppleMusicUsageDescription": "",                         //可选，字符串类型，使用媒体资料库权限描述
                    "NFCReaderUsageDescription": "",                            //可选，字符串类型，使用NFC权限描述
                    "NSHealthClinicalHealthRecordsShareUsageDescription": "",   //可选，字符串类型，访问临床记录权限描述
                    "NSHomeKitUsageDescription": "",                            //可选，字符串类型，访问HomeKit权限描述
                    "NSSiriUsageDescription": "",                               //可选，字符串类型，访问Siri权限描述
                    "NSFaceIDUsageDescription": "",                             //可选，字符串类型，使用FaceID权限描述
                    "NSLocalNetworkUsageDescription": "",                       //可选，字符串类型，访问本地网络权限描述
                    "NSUserTrackingUsageDescription": ""                        //可选，字符串类型，跟踪用户活动权限描述
                },
                "idfa": true,                   //可选，Boolean类型，是否使用广告标识
                "capabilities": {               //可选，JSON对象，应用的能力配置（Capabilities）
                },
                "CFBundleName": "HBuilder",     //可选，字符串类型，CFBundleName名称
                "validArchitectures": [         //可选，字符串数组类型，编译时支持的CPU指令，可取值arm64、arm64e、armv7、armv7s、x86_64
                    "arm64"
                ],
                "pushRegisterMode": "manual"    //可选，使用“Push(消息推送)”模块时申请系统推送权限模式，manual表示调用push相关API时申请，其它值表示应用启动时自动申请
            },
            "sdkConfigs": {         //可选，JSON对象，三方SDK相关配置
                "geolocation": {        //可选，JSON对象，Geolocation(定位)模块三方SDK配置
                    "system": {                     //可选，JSON对象，使用系统定位
                        "__platform__" : [ "ios", "android" ]   //可选，字符串数组类型，支持的平台
                    },
                    "amap": {                           //可选，JSON对象，使用高德定位SDK配置
                        "__platform__" : ["ios", "android"],    //可选，字符串数组类型，支持的平台
                        "appkey_ios": "",                       //必填，字符串类型，iOS平台高德定位appkey
                        "appkey_android": ""                    //必填，字符串类型，Android平台高德定位appkey
                    },
                    "baidu": {                         //可选，JSON对象，使用百度定位SDK配置
                        "__platform__" : [ "ios", "android" ],  //可选，字符串数组类型，支持的平台
                        "appkey_ios": "",                       //必填，字符串类型，iOS平台百度定位appkey
                        "appkey_android": ""                    //必填，字符串类型，Android平台百度定位appkey
                    }
                },
                "maps" : {              //可选，JSON对象，Maps(地图)模块三方SDK配置
                    "amap": {                       //可选，JSON对象，使用高德地图SDK配置
                        "appkey_ios": "",                       //必填，字符串类型，iOS平台高德地图appkey
                        "appkey_android": ""                    //必填，字符串类型，Android平台高德地图appkey
                    },
                    "baidu": {                      //可选，JSON对象，使用百度地图SDK配置
                        "appkey_ios": "",                       //必填，字符串类型，iOS平台百度地图appkey
                        "appkey_android": ""                    //必填，字符串类型，Android平台百度地图appkey
                    },
                    "google": {                     //可选，JSON对象，使用Google地图SDK配置
                        "APIKey_ios": "",                       //必填，字符串类型，iOS平台Google地图APIKey
                        "APIKey_android": ""                    //必填，字符串类型，Android平台Google地图APIKey
                    }
                },
                "oauth": {              //可选，JSON对象，OAuth(登录鉴权)模块三方SDK配置
                    "univerify" : {                 //可选，JSON对象，使用一键登录(univerify)SDK配置，无需手动配置参数，云端打包自动获取配置参数
                    },
                    "apple": {                      //可选，JSON对象，使用苹果登录(Sign in with Apple)SDK配置，无配置参数，仅iOS平台支持
                    },
                    "weixin": {                     //可选，JSON对象，使用微信登录SDK配置
                        "appid": "",                            //必填，字符串类型，微信开放平台申请的appid
                        "appsecret": "",                        //必填，字符串类型，微信开放平台申请的appsecret
                        "UniversalLinks": ""                    //可选，字符串类型，微信开放平台配置的iOS平台通用链接
                    },
                    "qq": {                         //可选，JSON对象，使用QQ登录SDK配置
                        "appid": "",                            //必填，字符串类型，QQ开放平台申请的appid
                        "UniversalLinks": ""                    //可选，字符串类型，QQ开放平台配置的iOS平台通用链接
                    },
                    "sina": {                       //可选，JSON对象，使用新浪微博登录SDK配置
                        "appkey": "",                           //必填，字符串类型，新浪微博开放平台申请的appid
                        "redirect_uri": "",                     //必填，字符串类型，新浪微博开放平台配置的redirect_uri
                        "UniversalLinks": ""                    //可选，字符串类型，新浪微博开放平台配置的iOS平台通用链接
                    },
                    "google": {                     //可选，JSON对象，使用Google登录SDK配置
                        "clientid": ""                          //必填，字符串类型，Google开发者后台申请的clientid
                    },
                    "facebook": {                   //可选，JSON对象，使用Facebook登录SDK配置
                        "appid": ""                             //必填，字符串类型，Facebook开发者后台申请的appid
                    }
                },
                "payment": {            //可选，JSON对象，Payment(支付)模块三方SDK配置
                    "appleiap": {                   //可选，JSON对象，使用Apple应用内支付配置，无配置参数，仅iOS平台支持
                    },
                    "alipay": {                     //可选，JSON对象，使用支付宝支付SDK配置
                        "__platform__": [ "ios", "android" ]    //可选，字符串数组类型，支持的平台
                    },
                    "weixin": {                     //可选，JSON对象，使用微信支付SDK配置
                        "__platform__": [ "ios", "android" ],   //可选，字符串数组类型，支持的平台
                        "appid": "",                            //必填，字符串类型，微信开放平台申请的appid
                        "UniversalLinks": ""                    //可选，字符串类型，微信开放平台配置的iOS平台通用链接
                    },
                    "paypal": {                     //可选，JSON对象，使用paypal支付SDK配置
                        "__platform__": [ "ios", "android" ],   //可选，字符串数组类型，支持的平台
                        "returnURL_ios": "",                    //必填，字符串类型，paypa开发者者后台配置的iOS平台returnURL
                        "returnURL_android": ""                 //必填，字符串类型，paypa开发者者后台配置的Android平台returnURL
                    },
                    "stripe": {                     //可选，JSON对象，使用stripe支付SDK配置
                        "__platform__": [ "ios", "android" ],   //可选，字符串数组类型，支持的平台
                        "returnURL_ios" : ""                    //必填，字符串类型，stripe开发者者后台配置的iOS平台returnURL
                    },
                    "google": {                     //可选，JSON对象，使用google支付SDK配置，无配置参数，仅Android平台支持
                    }
                },
                "push": {               //可选，JSON对象，Push(消息推送)模块三方SDK配置
                    "unipush": {                    //可选，JSON对象，使用UniPush SDK配置，无需手动配置参数，云端打包自动获取配置参数
                        "icons": {                          //可选，JSON对象，推送图标配置
                            "push": {                               //可选，JSON对象，Push图标配置
                                "ldpi": "",                                 //可选，字符串类型，普通屏设备推送图标路径，分辨率要求48x48
                                "mdpi": "",                                 //可选，字符串类型，大屏设备设备推送图标路径，分辨率要求48x48
                                "hdpi": "",                                 //可选，字符串类型，高分屏设备推送图标路径，分辨率要求72x72
                                "xdpi": "",                                 //可选，字符串类型，720P高分屏设备推送图标路径，分辨率要求96x96
                                "xxdpi": "",                                //可选，字符串类型，1080P高密度屏幕推送图标路径，分辨率要求144x144
                                "xxxdpi": "",                               //可选，字符串类型，4K屏设备推送图标路径，分辨率要求192x192
                            },
                            "smal": {                               //可选，JSON对象，Push小图标配置
                                "ldpi": "",                                 //可选，字符串类型，普通屏设备推送小图标路径，分辨率要求18x18
                                "mdpi": "",                                 //可选，字符串类型，大屏设备设备推送小图标路径，分辨率要求24x24
                                "hdpi": "",                                 //可选，字符串类型，高分屏设备推送小图标路径，分辨率要求36x36
                                "xdpi": "",                                 //可选，字符串类型，720P高分屏设备推送小图标路径，分辨率要求48x48
                                "xxdpi": "",                                //可选，字符串类型，1080P高密度屏幕推送小图标路径，分辨率要求72x72
                                "xxxdpi": "",                               //可选，字符串类型，4K屏设备推送小图标路径，分辨率要求96x96
                            }
                        }
                    },
                    "igexin": {                     //可选，JSON对象，使用个推推送SDK配置，**已废弃，推荐使用UniPush，UniPush是个推推送VIP版，功能更强大**
                        "appid": "",                            //必填，字符串类型，个推开放平台申请的appid
                        "appkey": "",                           //必填，字符串类型，个推开放平台申请的appkey
                        "appsecret": "",                        //必填，字符串类型，个推开放平台申请的appsecret
                        "icons": {                          //可选，JSON对象，推送图标配置
                            "push": {                               //可选，JSON对象，Push图标配置
                                "ldpi": "",                                 //可选，字符串类型，普通屏设备推送图标路径，分辨率要求48x48
                                "mdpi": "",                                 //可选，字符串类型，大屏设备设备推送图标路径，分辨率要求48x48
                                "hdpi": "",                                 //可选，字符串类型，高分屏设备推送图标路径，分辨率要求72x72
                                "xdpi": "",                                 //可选，字符串类型，720P高分屏设备推送图标路径，分辨率要求96x96
                                "xxdpi": "",                                //可选，字符串类型，1080P高密度屏幕推送图标路径，分辨率要求144x144
                                "xxxdpi": "",                               //可选，字符串类型，4K屏设备推送图标路径，分辨率要求192x192
                            },
                            "smal": {                               //可选，JSON对象，Push小图标配置
                                "ldpi": "",                                 //可选，字符串类型，普通屏设备推送小图标路径，分辨率要求18x18
                                "mdpi": "",                                 //可选，字符串类型，大屏设备设备推送小图标路径，分辨率要求24x24
                                "hdpi": "",                                 //可选，字符串类型，高分屏设备推送小图标路径，分辨率要求36x36
                                "xdpi": "",                                 //可选，字符串类型，720P高分屏设备推送小图标路径，分辨率要求48x48
                                "xxdpi": "",                                //可选，字符串类型，1080P高密度屏幕推送小图标路径，分辨率要求72x72
                                "xxxdpi": "",                               //可选，字符串类型，4K屏设备推送小图标路径，分辨率要求96x96
                            }
                        }
                    }
                },
                "share": {              //可选，JSON对象，Share(分享)模块三方SDK配置
                    "weixin": {                     //可选，JSON对象，使用微信分享SDK配置
                        "appid": "",                            //必填，字符串类型，微信开放平台申请的appid
                        "UniversalLinks": ""                    //可选，字符串类型，微信开放平台配置的iOS平台通用链接
                    },
                    "qq": {                         //可选，JSON对象，使用QQ分享SDK配置
                        "appid": "",                            //必填，字符串类型，QQ开放平台申请的appid
                        "UniversalLinks": ""                    //可选，字符串类型，QQ开放平台配置的iOS平台通用链接
                    },
                    "sina": {                       //可选，JSON对象，使用新浪微博分享SDK配置
                        "appkey": "",                           //必填，字符串类型，新浪微博开放平台申请的appid
                        "redirect_uri": "",                     //必填，字符串类型，新浪微博开放平台配置的redirect_uri
                        "UniversalLinks": ""                    //可选，字符串类型，新浪微博开放平台配置的iOS平台通用链接
                    }
                },
                "speech": {             //可选，JSON对象，Speech(语音识别)模块三方SDK配置
                    "baidu": {                      //可选，JSON对象，使用百度语音识别SDK配置
                        "appid": "",                            //必填，字符串类型，百度开放平台申请的appid
                        "apikey": "",                           //必填，字符串类型，百度开放平台申请的apikey
                        "secretkey": ""                         //必填，字符串类型，百度开放平台申请的secretkey
                    }
                },
                "statics": {            //可选，JSON对象，Statistic(统计)模块三方SDK配置
                    "umeng": {                      //可选，JSON对象，使用友盟统计SDK配置
                        "appkey_ios": "",                       //必填，字符串类型，友盟统计开放平台申请的iOS平台appkey
                        "channelid_ios": "",                    //可选，字符串类型，友盟统计iOS平台的渠道标识
                        "appkey_android": "",                   //必填，字符串类型，友盟统计开放平台申请的Android平台appkey
                        "channelid_android": ""                 //可选，字符串类型，友盟统计Android平台的渠道标识
                    },
                    "google" : {                    //可选，JSON对象，使用Google Analytics for Firebase配置
                        "config_ios" : "",                      //必填，字符串类型，Google Firebase统计开发者后台获取的iOS平台配置文件路径
                        "config_android" : ""                   //必填，字符串类型，Google Firebase统计开发者后台获取的Android平台配置文件路径
                    }
                },
                "ad": {                 //可选，JSON对象，uni-AD配置
                    "360": {                        //可选，JSON对象，使用360广告联盟SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    },
                    "csj": {                        //可选，JSON对象，使用今日头条穿山甲广告联盟SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    },
                    "gdt": {                        //可选，JSON对象，使用腾讯优量汇广告联盟SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    },
                    "ks": {                         //可选，JSON对象，使用快手广告联盟SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    },
                    "ks-content": {                 //可选，JSON对象，使用快手内容联盟SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    },
                    "sigmob": {                     //可选，JSON对象，使用Sigmob广告联盟SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    },
                    "hw": {                         //可选，JSON对象，使用华为广告联盟SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    },
                    "bd": {                         //可选，JSON对象，使用百度百青藤广告联盟SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    },
                    "BXM-AD": {                     //可选，JSON对象，使用互动游戏(变现猫)SDK，无需手动配置，在uni-AD后台申请开通后自动获取配置参数
                    }                    
                }
            },
            "icons": {              //可选，JSON对象，应用图标相关配置
                "ios":{                     //可选，JSON对象，iOS平台图标配置 
                    "appstore": "",                 //必填，字符串类型，分辨率1024x1024, 提交app sotre使用的图标路径
                    "iphone":{                      //可选，JSON对象，iPhone设备图标配置
                        "app@2x": "",                       //可选，字符串类型，分辨率120x120，程序图标路径  
                        "app@3x": "",                       //可选，字符串类型，分辨率180x180，程序图标路径  
                        "spotlight@2x": "",                 //可选，字符串类型，分辨率80x80，Spotlight搜索图标路径
                        "spotlight@3x": "",                 //可选，字符串类型，分辨率120x120，Spotlight搜索图标路径
                        "settings@2x": "",                  //可选，字符串类型，分辨率58x58，Settings设置图标路径
                        "settings@3x": "",                  //可选，字符串类型，分辨率87x87，Settings设置图标路径
                        "notification@2x": "",              //可选，字符串类型，分辨率40x40，通知栏图标路径
                        "notification@3x": ""               //可选，字符串类型，分辨率60x60，通知栏图标路径
                    },  
                    "ipad":{                        //可选，JSON对象，iPad设备图标配置
                        "app": "",                          //可选，字符串类型，分辨率76x76，程序图标图标路径
                        "app@2x": "",                       //可选，字符串类型，分辨率152x152，程序图标图标路径
                        "proapp@2x": "",                    //可选，字符串类型，分辨率167x167，程序图标图标路径
                        "spotlight": "",                    //可选，字符串类型，分辨率40x40，Spotlight搜索图标路径
                        "spotlight@2x": "",                 //可选，字符串类型，分辨率80x80，Spotlight搜索图标路径
                        "settings": "",                     //可选，字符串类型，分辨率29x29，Settings设置图标路径
                        "settings@2x": "",                  //可选，字符串类型，分辨率58x58，Settings设置图标路径
                        "notification": "",                 //可选，字符串类型，分辨率20x20，通知栏图标路径
                        "notification@2x": ""               //可选，字符串类型，分辨率740x40，通知栏图标路径
                    }  
                },  
                "android":{                 //可选，JSON对象，Android平台图标配置
                    "ldpi": "",                         //可选，字符串类型，普通屏设备程序图标，分辨率要求48x48，已废弃  
                    "mdpi": "",                         //可选，字符串类型，大屏设备程序图标，分辨率要求48x48，已废弃  
                    "hdpi": "",                         //可选，字符串类型，高分屏设备程序图标，分辨率要求72x72
                    "xhdpi": "",                        //可选，字符串类型，720P高分屏设备程序图标，分辨率要求96x96
                    "xxhdpi": "",                       //可选，字符串类型，1080P高分屏设备程序图标，分辨率要求144x144
                    "xxxhdpi": ""                       //可选，字符串类型，2K屏设备程序图标，分辨率要求192x192
                }
            },
            "splashscreen":{    //可选，JSON对象，启动界面配置
                "iosStyle": "common",   //可选，字符串类型，iOS平台启动界面样式，可取值common、default、storyboard
                "ios":{                 //可选，JSON对象，iOS平台启动界面配置 
                    "storyboard": "",               //可选，字符串类型，自定义storyboard启动界面文件路径，iosStyle值为storyboard时生效
                    "iphone":{                      //可选，JSON对象，iPhone设备启动图配置，iosStyle值为default时生效
                        "default": "",                      //可选，字符串类型，分辨率320x480，iPhone3（G/GS）启动图片路径，已废弃  
                         "retina35": "",                    //可选，字符串类型，分辨率640x960，3.5英寸设备(iPhone4/4S)启动图片路径，已废弃 
                         "retina40": "",                    //可选，字符串类型，分辨率640x1136，4.0英寸设备(iPhone5/5S)启动图片路径
                         "retina40l":"",                    //可选，字符串类型，分辨率1136x640，4.0英寸设备(iPhone5/5S)横屏启动图片路径
                         "retina47": "",                    //可选，字符串类型，分辨率750x1334，4.7英寸设备（iPhone6/7/8）启动图片路径
                         "retina47l": "",                   //可选，字符串类型，分辨率1334x750，4.7英寸设备（iPhone6/7/8）横屏启动图片路径
                         "retina55": "",                    //可选，字符串类型，分辨率1242x2208，5.5英寸设备（iPhone6/7/8Plus）启动图片路径  
                         "retina55l": "",                   //可选，字符串类型，分辨率2208x1242，5.5英寸设备（iPhone6/7/8Plus）横屏启动图片路径
                         "iphonex": "",                     //可选，字符串类型，分辨率1125x2436，5.8英寸设备（iPhoneX/XS）启动图片路径
                         "iphonexl": "",                    //可选，字符串类型，分辨率2436x1125，5.8英寸设备（iPhoneX/XS）横屏启动图片路径
                         "portrait-896h@2x": "",            //可选，字符串类型，分辨率828x1792，6.1英寸设备（iPhoneXR）启动图片路径
                         "landscape-896h@2x": "",           //可选，字符串类型，分辨率1792x828，6.1英寸设备（iPhoneXR）iPhoneXR横屏启动图片路径
                         "portrait-896h@3x": "",            //可选，字符串类型，分辨率1242x2688，6.5英寸设备（iPhoneXS Max）启动图片路径
                         "landscape-896h@3x": ""            //可选，字符串类型，分辨率2688x1242，6.5英寸设备（iPhoneXS Max）横屏启动图片路径
                    },  
                    "ipad":{                        //可选，JSON对象，iPad设备启动图配置，iosStyle值为default时生效
                         "portrait": "",                    //可选，字符串类型，分辨率768x1004，iPad竖屏启动图片路径，已废弃  
                         "portrait-retina": "",             //可选，字符串类型，分辨率1536x2008，iPad高分屏竖屏启动图片路径，已废弃  
                         "landscape": "",                   //可选，字符串类型，分辨率1024x748，iPad横屏启动图片路径，已废弃   
                         "landscape-retina": "",            //可选，字符串类型，分辨率2048x1496，iPad高分屏横屏启动图片路径，已废弃  
                         "portrait7": "",                   //可选，字符串类型，分辨率768x1024，9.7/7.9英寸iPad/mini竖屏启动图片路径 
                         "landscape7": "",                  //可选，字符串类型，分辨率1024x768，9.7/7.9英寸iPad/mini横屏启动图片路径
                         "portrait-retina7": "",            //可选，字符串类型，分辨率1536x2048，9.7/7.9英寸iPad/mini高分屏竖屏图片路径
                         "landscape-retina7": "",           //可选，字符串类型，分辨率2048x1536，9.7/7.9英寸iPad/mini高分屏横屏启动图片路径
                         "portrait-1112h@2x":"",            //可选，字符串类型，分辨率1668x2224，10.5英寸iPad Pro竖屏启动图片路径
                         "landscape-1112h@2x":"",           //可选，字符串类型，分辨率2224x1668，10.5英寸iPad Pro横屏启动图片路径
                         "portrait-1194h@2x":"",            //可选，字符串类型，分辨率1668x2388，11英寸iPad Pro竖屏启动图片路径
                         "landscape-1194h@2x":"",           //可选，字符串类型，分辨率2388x1668，11英寸iPad Pro横屏启动图片路径
                         "portrait-1366h@2x":"",            //可选，字符串类型，分辨率2048x2732，12.9英寸iPad Pro竖屏启动图片路径
                         "landscape-1366h@2x":""            //可选，字符串类型，分辨率2732x2048，12.9英寸iPad Pro横屏启动图片路径
                    }  
                },
                "androidStyle": "common",//可选，字符串类型，Android平台启动界面样式，可取值common、default
                "android":{         //可选，JSON对象，Android平台启动图片配置， androidStyle值为default时生效
                   "ldpi": "",                          //可选，字符串类型，分辨率320x442，低密度屏幕启动图片路径，已废弃
                   "mdpi": "",                          //可选，字符串类型，分辨率240x282，中密度屏幕启动图片路径，已废弃
                   "hdpi": "",                          //可选，字符串类型，分辨率480x762，高密度屏幕启动图片路径
                   "xhdpi": "",                         //可选，字符串类型，分辨率720x1242，720P高密度屏幕启动图片路径
                   "xxhdpi": ""                         //可选，字符串类型，分辨率1080x1882，1080P高密度屏幕启动图片路径
                }  
            },
            "orientation": [            //可选，字符串数组类型，应用支持的横竖屏，**已废弃，使用screenOrientation配置** 
                "portrait-primary",
                "portrait-secondary",
                "landscape-primary",
                "landscape-secondary"
            ]
        },
        "compatible": {                             //可选，JSON对象，uni-app兼容模式
            "ignoreVersion": false,                             //可选，Boolean类型，是否忽略版本兼容检查提示
            "runtimeVersion": "",                               //可选，字符串类型，兼容的uni-app运行环境版本号，多个版本使用,分割
            "compilerVersion": ""                               //可选，字符串类型，兼容的编译器版本号
        },
        "confusion": {                              //可选，JSON对象，原生混淆加密配置，参考：https://uniapp.dcloud.io/tutorial/app-sec-confusion
            "description": "",                                      //可选，字符串类型，原生混淆描述
            "resources": {                                          //必填，JSON对象，原生混淆文件配置
                "js/common.js": {                                           //可选，JSON对象，键名为需要原生混淆的文件路径
                }
            },
        },
        "channel": "",                              //可选，字符串类型，渠道标识
        "cers": {                                   //可选，JSON对象，应用的异常崩溃与错误报告系统配置
            "crash": true,                                          //可选，Boolean类型，是否提交应用异常崩溃信息
        },
        "cache": {                                  //可选，JSON对象，Webview窗口默认使用的缓存模式，uni-app项目已废弃
            "mode": "default"                                       //可选，字符串类型，可取值default、cacheElseNetwork、noCache、cacheOnly
        },
        "error": {                                  //可选，JSON对象，页面加载错误配置，uni-app项目仅对webview组件有效，参考：https://uniapp.dcloud.io/tutorial/app-webview-error
            "url": ""                                               //必填，字符串类型，webview页面错误是跳转的页面地址
        },
        "kernel": {                                 //可选，JSON对象，webview内核配置
            "ios": "WKWebview",                                     //可选，iOS平台使用的webview类型，可取值WKWebview、UIWebview
            "recovery": "reload"                                    //可选，iOS平台使用WKWebview时，内核崩溃后的处理逻辑，可取值restart、reload、none
        },
        "launchwebview": {                          //可选，JSON对象，应用首页相关配置，uni-app项目不建议手动修改
            "plusrequire": "normal",                                //可选，字符串类型，加载plus API时机，可取值ahead、normal、later、none
            "injection": false,                                     //可选，Boolean类型，是否提前注入plus API
            "overrideresource": [                           //可选，JSON对象数组，应用首页的拦截资源相关配置
                {
                    "match": "",                                    //可选，字符串类型，匹配拦截的资源url地址的正则表达式
                    "redirect":"",                                  //可选，字符串类型，拦截资源的重定向地址
                    "mime":"",                                      //可选，字符串类型，拦截资源的数据类型mime
                    "encoding":"",                                  //可选，字符串类型，拦截资源的数据编码
                    "header": {                                     //可选，JSON对象，拦截资源的http头数据
                    }  
                }
            ],  
            "overrideurl": {                                //可选，JSON对象，应用首页的拦截链接请求处理逻辑
                "mode": "reject",                                   //可选，字符串类型，拦截模式，可取值allow、reject
                "match": "",                                        //可选，字符串类型，匹配拦截规则，支持正则表达式
                "exclude": "none"                                   //可选，字符串类型，排除拦截理规则，可取值none、redirect
            },  
            "replacewebapi": {                              //可选，JSON对象，是否重写Web API实现相关配置
                "geolocation": "none"                               //可选，字符串类型，重写标准定位API，可取值none、alldevice、auto 
            },  
            "subNViews": [                                  //可选，JSON对象数组，首页原生View相关配置，已废弃
                {  
                    "id": "",                                       //可选，字符串类型，原生View标识
                    "styles": {                                     //可选，JSON对象，原生View样式
                    },  
                    "tags": [                                       //可选，JSON对象数组，原生View中包含的tag标签列表
                        {}
                    ]  
                }
            ],  
            "titleNView": {                                 //可选，JSON对象，标题栏相关配置
                "backgroundColor": "#RRGGBB",                       //可选，字符串类型，#RRGGBB格式，标题栏背景颜色
                "titleText": "",                                    //可选，字符串类型，标题栏标题文字内容
                "titleColor": "#RRGGBB",                            //可选，字符串类型，#RRGGBB格式，标题栏标题文字颜色  
                "titleSize": "17px",                                //可选，字符串类型，标题字体大小，默认大小为17px
                "autoBackButton": true,                             //可选，Boolean类型，是否显示标题栏上返回键
                "backButton": {                                     //可选，JSON对象，返回键样式
                    "backgournd": "#RRGGBB",                                //可选，字符串类型，#RRGGBB格式，返回按钮背景颜色
                    "color": "#RRGGBB",                                     //可选，字符串类型，#RRGGBB格式，返回图标颜色
                    "colorPressed": "#RRGGBB",                              //可选，字符串类型，#RRGGBB，返回图标按下时的颜色
                },  
                "buttons": [                                        //可选，JSON对象数组，标题栏按钮配置
                    {  
                        "color": "#RRGGBB",                                 //可选，字符串类型，#RRGGBB格式，按钮上的文字颜色
                        "colorPressed": "#RRGGBB",                          //可选，字符串类型，#RRGGBB格式，按钮按下状态的文字颜色
                        "float": "right",                                   //可选，字符串类型，按钮显示位置，可取值left、right  
                        "fontWeight": "normal",                             //可选，字符串类型，按钮上文字的粗细，可取值normal、bold
                        "fontSize": "22px",                                 //可选，字符串类型，按钮上文字的大小  
                        "fontSrc": "",                                      //可选，字符串类型，按钮上文字使用的字体文件路径
                        "text": ""                                          //可选，字符串类型，按钮上显示的文字
                    }
                ],  
                "splitLine": {                                      //可选，JSON对象，标题栏分割线样式
                    "color": "#RRGGBB",                                     //可选，字符串类型，#RRGGBB格式，分割线颜色
                    "height": "1px"                                         //可选，字符串类型，分割线高度
                } 
            },  
            "statusbar": {                                  //可选，JSON对象，状态栏配置
                "background": "#RRGGBB"                             //可选，字符串类型，#RRGGBB格式，沉浸式状态栏样式下系统状态栏背景颜色
            },  
            "top": "0px",                                   //可选，字符串类型，Webview的顶部偏移量，支持px、%单位
            "height": "100%",                               //可选，字符串类型，Webview窗口高度，支持px、%单位
            "bottom": "0px",                                //可选，字符串类型，Webview的底部偏移量，仅在未同时设置top和height属性时生效
            "backButtonAutoControl": "none",                //可选，字符串类型，运行环境自动处理返回键的控制逻辑，可取值none、hide、close
            "additionalHttpHeaders": {                      //可选，JSON对象，额外添加HTTP请求头数据
            }
        },
        "nativePlugins": {                          //可选，JSON数组对象，uni原生插件配置，参考：https://nativesupport.dcloud.net.cn/NativePlugin/use/use_local_plugin
            "%UniPlugin-ID%": {                                     //可选，JSON对象，键名为插件标识，值为插件配置参数
            }
        },
        "popGesture": "none",                       //可选，字符串类型，窗口侧滑返回默认效果，可取值none、close、hide
        "runmode": "liberate",                      //可选，字符串类型，应用资源运行模式，可取值normal、liberate
        "safearea": {                              //可选，JSON对象，安全区域配置
            "background": "#RRGGBB",                                //可选，字符串类型，#RRGGBB格式，安全区域背景颜色
            "backgroundDark": "#RRGGBB",                            //可选，字符串类型，#RRGGBB格式，暗黑模式安全区域背景颜色
            "bottom": {                                             //可选，JSON对象，底部安全区域配置
                "offset": "none"                                            //可选，字符串类型，安全区域偏移值，可取值auto、none
            },
            "left": {                                               //可选，JSON对象，左侧安全区域配置
                "offset": "none"                                            //可选，字符串类型，安全区域偏移值，可取值auto、none
            },
            "right": {                                              //可选，JSON对象，左侧安全区域配置
                "offset": "none"                                            //可选，字符串类型，安全区域偏移值，可取值auto、none
            }
        },
        "softinput": {                              //可选，JSON对象，软键盘相关配置
            "navBar": "auto",                                       //可选，字符串类型，iOS平台软键盘上导航条的显示模式，可取值auto、none
            "auxiliary": false,                                     //可选，Boolean类型，是否开启辅助输入功能
            "mode": "adjustResize"                                  //可选，字符串类型，弹出系统软键盘模式，可取值adjustResize、adjustPan
        },
        "ssl": {                                    //可选，JSON对象，ssl相关设置
            "untrustedca": "accept"                                 //可选，字符串类型，https请求时服务器非受信证书的处理逻辑，可取值accept、refuse、warning
        },
        "statusbar": {                              //可选，JSON对象，应用启动后的系统状态栏相关配置
            "immersed": "none",                                     //可选，字符串类型，沉浸式状态栏样式，可取值none、suggestedDevice、supportedDevice
            "style": "light",                                       //可选，字符串类型，系统状态栏样式（前景颜色），可取值dark、light
            "background": "#RRGGBB"                                 //可选，字符串类型，#RRGGBB格式，系统状态栏背景颜色
        },
        "useragent": {                              //可选，JSON对象，应用UserAgent相关配置，默认值为系统UserAgent，并添加 uni-app Html5Plus/1.0 
            "value": "",                                            //可选，字符串类型，设置的默认userAgent值
            "concatenate": false                                    //可选，Boolean类型，是否将value值作为追加值连接到系统默认userAgent值之后
        },
        "useragent_android": {                      //可选，JSON对象，Android平台应用UserAgent相关配置，优先级高于useragent配置
            "value": "",                                            //可选，字符串类型，设置的默认userAgent值
            "concatenate": false                                    //可选，Boolean类型，是否将value值作为追加值连接到系统默认userAgent值之后
        },
        "useragent_ios": {                          //可选，JSON对象，iOS平台应用UserAgent相关配置，优先级高于useragent配置
            "value": "",                                            //可选，字符串类型，设置的默认userAgent值
            "concatenate": false                                    //可选，Boolean类型，是否将value值作为追加值连接到系统默认userAgent值之后
        }
	},
    "quickapp": {},
    "mp-weixin": {
        "appid": "wx开头的微信小程序appid",
        "uniStatistics": {
            "enable": false
        }
    },
    "mp-baidu": {
        "appid": "百度小程序appid"
    },
    "mp-toutiao": {
        "appid": "字节跳动小程序appid"
    },
    "mp-lark": {
        "appid": "飞书小程序appid"
    },
    "h5": {
        "title": "演示",
        "template": "index.html",
        "router": {
            "mode": "history",
            "base": "/hello/"
        },
        "async": {
            "loading": "AsyncLoading",
            "error": "AsyncError",
            "delay": 200,
            "timeout": 3000
        }
    }
}
```





### [3. package.json 包配置](https://uniapp.dcloud.net.cn/collocation/package.html)

uni-app 通过在`package.json`文件中增加`uni-app`扩展节点，可实现自定义条件编译平台。

扩展新的平台后，有3点影响：

1. 可以在代码里编写自定义的条件编译，为这个新平台编写专用代码
2. 运行时可以执行面向新平台的编译运行
3. 发行时可以执行面向新平台的编译发行

注意只能扩展web和小程序平台，不能扩展app打包。并且扩展小程序平台时只能基于指定的基准平台扩展子平台，不能扩展基准平台。基准平台详见下文。

package.json扩展配置用法：

```json
{
    /**
     * package.json其它原有配置 
     * 拷贝代码后请去掉注释！
     */
    "uni-app": {// 扩展配置
        "scripts": {
            "custom-platform": { //自定义编译平台配置，可通过cli方式调用
                "title":"自定义扩展名称", // 在HBuilderX中会显示在 运行/发行 菜单中
                "browser":"",  //运行到的目标浏览器，仅当UNI_PLATFORM为h5时有效
                "env": {//环境变量
                    "UNI_PLATFORM": "",  //基准平台
                    "MY_TEST": "", // ... 其他自定义环境变量
                 },
                "define": { //自定义条件编译
                    "CUSTOM-CONST": true //自定义条件编译常量，建议为大写
                }
            }
        }    
    }
}
```

- `UNI_PLATFORM`仅支持填写`uni-app`默认支持的基准平台，目前仅限如下枚举值：`h5`、`mp-weixin`、`mp-alipay`、`mp-baidu`、`mp-toutiao`、`mp-qq`
- `browser` 仅在`UNI_PLATFORM`为`h5`时有效,目前仅限如下枚举值：`chrome`、`firefox`、`ie`、`edge`、`safari`、`hbuilderx`
- `package.json`文件中不允许出现注释，否则扩展配置无效
- `vue-cli`需更新到最新版，HBuilderX需升级到 2.1.6+ 版本



### [4. vue.config.js](https://uniapp.dcloud.net.cn/collocation/vue-config.html)

vue.config.js 是一个可选的配置文件，如果项目的根目录中存在这个文件，那么它会被自动加载，一般用于配置 webpack 等编译选项，具体规范参考：[vue.config.js](https://cli.vuejs.org/zh/config/#vue-config-js)

**支持情况**

- CLI 工程
- HBuilderX 2.1.5 及以上版本

**注意事项**

- 仅vue页面生效

部分配置项会被编译配置覆盖，例如：

- publicPath 不支持，如果需要配置，请在 manifest.json->h5->router->base 中配置，参考文档：[h5-router](https://uniapp.dcloud.net.cn/collocation/manifest#h5-router)
- outputDir 不支持
- assetsDir 固定 static
- pages 不支持
- runtimeCompiler 固定 false
- productionSourceMap 固定 false
- css.extract H5 平台固定 false，其他平台固定 true
- parallel 固定 false
- 使用cli项目时，默认情况下 babel-loader 会忽略所有 node_modules 中的文件。如果你想要通过 Babel 显式转译一个依赖，可以在transpileDependencies中列出来。[详情参考](https://cli.vuejs.org/zh/config/#transpiledependencies)



**自定义静态资源目录**

```javascript
const path = require('path')
const CopyWebpackPlugin = require('copy-webpack-plugin') //最新版本copy-webpack-plugin插件暂不兼容，推荐v5.0.0

module.exports = {
	configureWebpack: {
		plugins: [
			new CopyWebpackPlugin([
				{
					from: path.join(__dirname, 'src/images'),
					to: path.join(__dirname, 'dist', process.env.NODE_ENV === 'production' ? 'build' : 'dev', process.env.UNI_PLATFORM, 'images')
				}
			])
		]
	}
}
```

**注入全局依赖**

```javascript
// 示例从插件市场下载 mp-storage
const webpack = require('webpack')

module.exports = {
	configureWebpack: {
		plugins: [
			new webpack.ProvidePlugin({
				'localStorage': ['mp-storage', 'localStorage'],
				'window.localStorage': ['mp-storage', 'localStorage']
			})
		]
	}
}
```

**发布时删除console**

```javascript
module.exports = {
	chainWebpack: (config) => {
		// 发行或运行时启用了压缩时会生效
		config.optimization.minimizer('terser').tap((args) => {
			const compress = args[0].terserOptions.compress
			// 非 App 平台移除 console 代码(包含所有 console 方法，如 log,debug,info...)
			compress.drop_console = true
			compress.pure_funcs = [
				'__f__', // App 平台 vue 移除日志代码
				// 'console.debug' // 可移除指定的 console 方法
			]
			return args
		})
	}
}
```

**发布时动态修改 manifest.json**

```javascript
// 读取 manifest.json ，修改后重新写入
const fs = require('fs')

const manifestPath = './src/manifest.json'
let Manifest = fs.readFileSync(manifestPath, { encoding: 'utf-8' })
function replaceManifest(path, value) {
  const arr = path.split('.')
  const len = arr.length
  const lastItem = arr[len - 1]

  let i = 0
  let ManifestArr = Manifest.split(/\n/)

  for (let index = 0; index < ManifestArr.length; index++) {
    const item = ManifestArr[index]
    if (new RegExp(`"${arr[i]}"`).test(item)) ++i;
    if (i === len) {
      const hasComma = /,/.test(item)
      ManifestArr[index] = item.replace(new RegExp(`"${lastItem}"[\\s\\S]*:[\\s\\S]*`), `"${lastItem}": ${value}${hasComma ? ',' : ''}`)
      break;
    }
  }

  Manifest = ManifestArr.join('\n')
}
// 使用
replaceManifest('app-plus.usingComponents', false)
replaceManifest('app-plus.splashscreen.alwaysShowBeforeRender', false)
replaceManifest('mp-baidu.usingComponents', false)
fs.writeFileSync(manifestPath, Manifest, {
  "flag": "w"
})

module.exports = {
	// ...
}
```



### [5. vite.config.js](https://uniapp.dcloud.net.cn/collocation/vite-config.html)

用到再看。



### [6. uni.scss](https://uniapp.dcloud.net.cn/collocation/uni-scss.html)

* `uni.scss`文件的用途是为了方便整体控制应用的风格。比如按钮颜色、边框风格，`uni.scss`文件里预置了一批scss变量预置。
* `uni-app` 官方扩展插件（uni ui）及 [插件市场](https://ext.dcloud.net.cn/) 上很多三方插件均使用了这些样式变量，如果你是插件开发者，建议你使用 scss 预处理，并在插件代码中直接使用这些变量（无需 import 这个文件），方便用户通过搭积木的方式开发整体风格一致的App。
* `uni.scss`是一个特殊文件，在代码中无需 import 这个文件即可在scss代码中使用这里的样式变量。uni-app的编译器在webpack配置中特殊处理了这个uni.scss，使得每个scss文件都被注入这个uni.scss，达到全局可用的效果。如果开发者想要less、stylus的全局使用，需要在vue.config.js中自行配置webpack策略。

* pages.json不支持scss，原生导航栏和tabbar的动态修改只能使用js api





### [7. App.vue](https://uniapp.dcloud.net.cn/collocation/App.html)

* `App.vue`是uni-app的主组件，所有页面都是在`App.vue`下进行切换的，是页面入口文件。但`App.vue`本身不是页面，这里不能编写视图元素，也就是没有`<template>`。
* 应用生命周期仅可在`App.vue`中监听，在页面监听无效。



#### [7.1 应用生命周期](https://uniapp.dcloud.net.cn/collocation/App.html#applifecycle)

| 函数名               | 说明                                                         |
| :------------------- | :----------------------------------------------------------- |
| onLaunch             | 当`uni-app` 初始化完成时触发（全局只触发一次）               |
| onShow               | 当 `uni-app` 启动，或从后台进入前台显示                      |
| onHide               | 当 `uni-app` 从前台进入后台                                  |
| onError              | 当 `uni-app` 报错时触发                                      |
| onUniNViewMessage    | 对 `nvue` 页面发送的数据进行监听，可参考 [nvue 向 vue 通讯](https://uniapp.dcloud.io/tutorial/nvue-api?id=communication) |
| onUnhandledRejection | 对未处理的 Promise 拒绝事件监听函数（2.8.1+）                |
| onPageNotFound       | 页面不存在监听函数                                           |
| onThemeChange        | 监听系统主题变化                                             |

```javascript
<script>
	// 只能在App.vue里监听应用的生命周期
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

```

- **应用生命周期仅可在`App.vue`中监听，在其它页面监听无效**。
- 以组合式 API 使用时，在 Vue2 和 Vue3 中存在一定区别，请分别参考：[Vue2 组合式 API 使用文档](https://uniapp.dcloud.net.cn/tutorial/vue-composition-api.html) 和 [Vue3 组合式 API 使用文档](https://uniapp.dcloud.net.cn/tutorial/vue3-composition-api.html)。
- 应用启动参数，可以在API `uni.getLaunchOptionsSync`获取，[详见](https://uniapp.dcloud.net.cn/api/plugins/getLaunchOptionsSync.html#getlaunchoptionssync)
- onlaunch里进行页面跳转，如遇白屏报错，请参考https://ask.dcloud.net.cn/article/35942
- `App.vue` 不能写模板
- onPageNotFound 页面实际上已经打开了（比如通过分享卡片、小程序码）且发现页面不存在，才会触发，api 跳转不存在的页面不会触发（如 uni.navigateTo）



#### [7.2 globalData](https://uniapp.dcloud.net.cn/collocation/App.html#globaldata)

**App.vue 中定义globalData的相关配置：**

```javascript
<script>  
    export default {  
        globalData: {  
            text: 'text'  
        }
    }  
</script>  
```

* js中操作globalData的方式如下： `getApp().globalData.text = 'test'`
* 在应用onLaunch时，getApp对象还未获取，暂时可以使用this.globalData获取globalData。
* 如果需要把globalData的数据绑定到页面上，可在页面的onShow页面生命周期里进行变量重赋值。
* nvue的weex编译模式中使用globalData的话，由于weex生命周期不支持onShow，但熟悉5+的话，可利用监听webview的addEventListener show事件实现onShow效果，或者直接使用weex生命周期中的beforeCreate。但建议开发者使用uni-app编译模式，而不是weex编译模式。
* globalData是简单的全局变量，如果使用状态管理，请使用`vuex`（main.js中定义）



#### [7.3 全局样式](https://uniapp.dcloud.net.cn/collocation/App.html#%E5%85%A8%E5%B1%80%E6%A0%B7%E5%BC%8F)

* 在`App.vue`中，可以定义一些全局通用样式，例如需要加一个通用的背景色，首屏页面渲染的动画等都可以写在App.vue中。
* 注意如果工程下同时有vue和nvue文件，全局样式的所有css会应用于所有文件，而nvue支持的css有限，编译器会在控制台报警，提示某些css无法在nvue中支持。此时需要把nvue不支持的css写在单独的条件编译里。如：

```stylus
<style>
    /* #ifndef APP-PLUS-NVUE */
    @import './common/uni.css';
    /* #endif*/
</style>
```



### [8. main.js](https://uniapp.dcloud.net.cn/collocation/main.html)

* `main.js`是 uni-app 的入口文件，主要作用是初始化`vue`实例、定义全局组件、使用需要的插件如 vuex。
* 首先引入了`Vue`库和`App.vue`，创建了一个`vue`实例，并且挂载`vue`实例。
* 使用`Vue.use`引用插件，使用`Vue.prototype`添加全局变量，使用`Vue.component`注册全局组件。
* 无法使用`vue-router`，路由须在`pages.json`中进行配置。如果开发者坚持使用`vue-router`，可以在[插件市场](https://ext.dcloud.net.cn/search?q=vue-router)找到转换插件。
* nvue 暂不支持在 main.js 注册全局组件

```javascript
import Vue from 'vue'
import App from './App'
import pageHead from './components/page-head.vue' //全局引用 page-head 组件

Vue.config.productionTip = false
Vue.component('page-head', pageHead) //全局注册 page-head 组件，每个页面将可以直接使用该组件
App.mpType = 'app'

const app = new Vue({
...App
})
app.$mount() //挂载 Vue 实例
```





## `IV>uni-app 组件`

### [1. 基础组件](https://uniapp.dcloud.net.cn/component/view.html#)

* 基础组件在uni-app框架中已经内置，无需将内置组件的文件导入项目，也无需注册内置组件，随时可以直接使用

### [2. NVUE组件](https://uniapp.dcloud.net.cn/component/barcode.html#)

### [3. 拓展组件](https://uniapp.dcloud.net.cn/component/uniui/uni-ui.html)

* 扩展组件需要将组件导入项目中才可以使用。

* uni-ui不包括基础组件，**它是基础组件的补充**。

### [4. datacom 组件规范](https://uniapp.dcloud.net.cn/component/datacom.html)

* 用到再看。

### [5. 组件库选型指南](https://uniapp.dcloud.net.cn/component/component-selection.html)

* 选择组件的建议:
  * 首先使用内置组件
  * 然后使用uni ui扩展组件
  * 其他需求依靠插件市场其他组件灵活补充

#### `5.1 uni ui`

* 优化逻辑层和视图层的通信折损：非H5端的各个平台，包括App和各种小程序，其逻辑层和视图层是分离的，两层之间通信交互会有折损，导致诸如跟手滑动不流畅。uni ui在底层会利用wxs等技术，把适当的js代码运行在视图层，减少通信折损，保证诸如swiperAction左滑菜单等跟手操作流畅顺滑
* 自动差量diff数据：在uni-app下，开发App和小程序，不需要手动setData，底层自动会差量更新数据。但如果使用了小程序组件，则需要按小程序的setData方式来更新数据，很难做到自动diff更新数据。
* 背景停止：很多ui组件是会一直动的，比如轮播图、跑马灯。即便这个窗体被新窗体挡住，它在背景层仍然在消耗着硬件资源。在Android的webview版本为chrome66以上，背景操作ui会引发很严重的性能问题，造成前台界面明显卡顿。而uni ui的组件，会自动判断自己的显示状态，在组件不再可见时，不会再做动画消耗硬件资源。
* 纯vue语法：uni ui的引用、开发都是纯vue方式。而小程序组件的引用注册、开发都是小程序语法，两种语法混合在一个工程，写的也不舒服，维护也麻烦。
* 与[uni统计](https://tongji.dcloud.net.cn/)自动整合：比如使用uni ui的导航栏组件，就不需要写统计的自定义事件来触发页面标题上报。uni统计会自动识别导航栏组件的标题。类似的，收藏组件、购物车组件，都可以免打点直接使用。
* uni ui兼容Android 4.4等低端机webview，没有浏览器兼容问题。
* uni ui支持nvue：App端，uni-app同时支持webview渲染和原生渲染，而uni ui是可以一套代码同时支持webview渲染和原生渲染的。为了兼容原生渲染，uni ui也做到了纯flex布局。
* uni ui内置vue doc，使用组件时有良好的代码提示
* 支持[easycom](https://uniapp.dcloud.net.cn/collocation/pages?id=easycom)规范，使用非常简单
* 支持[datacom规范](https://uniapp.dcloud.net.cn/component/datacom)，云端一体全部封装掉
* 支持[uni_module规范](https://uniapp.dcloud.net.cn/uni_modules)，方便插件的更新
* 推荐在HBuilderX新建项目时，直接选择uni ui项目模板，然后在代码里直接敲u，所有组件都拉出来，不用引用、不用注册，直接就用。

#### `5.2 uView`

* 整合了非常多组件，功能丰富、文档清晰，但不支持nvue(2.x已支持nvue)

#### `5.3 colorUI css库`

* 颜值很高，css库而非组件

#### `5.4 unify UI`

* 全端支持的组件库，侧重nvue（商城已下架）

#### `5.5 mypUI`

* 全端支持的组件库，侧重nvue

#### `5.6 ThorUI`

#### `5.7 graceUI`





## [V>uni-app API](https://uniapp.dcloud.net.cn/api/)

### [1. 概述](https://uniapp.dcloud.net.cn/api/)

#### [1.1 API Promise 化](https://uniapp.dcloud.net.cn/api/#api-promise-%E5%8C%96)

* 具体 API Promise 化 的策略

  * 异步的方法，如果不传入 success、fail、complete 等 callback 参数，将以 Promise 返回数据。例如：`uni.getImageInfo()`
  * 异步的方法，且有返回对象，如果希望获取返回对象，必须至少传入一项 success、fail、complete 等 callback 参数。

  ```javascript
   // 正常使用
   const task = uni.connectSocket(
    success(res){
     console.log(res)
    }
   )
  
   // Promise 化
   uni.connectSocket().then(res => {
     // 此处即为正常使用时 success 回调的 res
     // uni.connectSocket() 正常使用时是会返回 task 对象的，如果想获取 task ，则不要使用 Promise 化
     console.log(res)
   })
  ```

* 不进行 Promise 化 的 API
  * 同步的方法（即以 sync 结束）。例如：`uni.getSystemInfoSync()`
  * 以 create 开头的方法。例如：`uni.createMapContext()`
  * 以 manager 结束的方法。例如：`uni.getBackgroundAudioManager()`

#### [1.2 Vue 2 和 Vue 3 的 API Promise 化](https://uniapp.dcloud.net.cn/api/#vue-2-%E5%92%8C-vue-3-%E7%9A%84-api-promise-%E5%8C%96)

- Vue2 对部分 API 进行了 Promise 封装，返回数据的第一个参数是错误对象，第二个参数是返回数据。此时使用 `catch` 是拿不到报错信息的，因为内部对错误进行了拦截。
- Vue3 对部分 API 进行了 Promise 封装，调用成功会进入 `then 方法` 回调。调用失败会进入 `catch 方法` 回调

```javascript
//VUE 2
// 默认方式
uni.request({
  url: "https://www.example.com/request",
  success: (res) => {
    console.log(res.data);
  },
  fail: (err) => {
    console.error(err);
  },
});

// Promise
uni
  .request({
    url: "https://www.example.com/request",
  })
  .then((data) => {
    // data为一个数组
    // 数组第一项为错误信息 即为 fail 回调
    // 第二项为返回数据
    var [err, res] = data;
    console.log(res.data);
  });

// Await
async function request() {
  var [err, res] = await uni.request({
    url: "https://www.example.com/request",
  });
  console.log(res.data);
}
```

```javascript
//VUE 3
// 默认方式
uni.request({
  url: "https://www.example.com/request",
  success: (res) => {
    console.log(res.data);
  },
  fail: (err) => {
    console.error(err);
  },
});

// 使用 Promise then/catch 方式调用
uni
  .request({
    url: "https://www.example.com/request",
  })
  .then((res) => {
    // 此处的 res 参数，与使用默认方式调用时 success 回调中的 res 参数一致
    console.log(res.data);
  })
  .catch((err) => {
    // 此处的 err 参数，与使用默认方式调用时 fail 回调中的 err 参数一致
    console.error(err);
  });

// 使用 Async/Await 方式调用
async function request() {
  try {
    var res = await uni.request({
      url: "https://www.example.com/request",
    });
    // 此处的 res 参数，与使用默认方式调用时 success 回调中的 res 参数一致
    console.log(res);
  } catch (err) {
    // 此处的 err 参数，与使用默认方式调用时 fail 回调中的 err 参数一致
    console.error(err);
  }
}
```



### `2. 基础`

#### [2.1 日志打印](https://uniapp.dcloud.net.cn/api/log.html)

* console.debug, console.log, console.info, console.warn, console.error

* 快捷键
  * clog
  * clogv



#### [2.2 定时器](https://uniapp.dcloud.net.cn/api/timer.html)

##### `2.2.1 setTimeout(callback, delay, rest)`

设定一个定时器。在定时到期以后执行注册的回调函数

**参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| callback | Function | 是   | 回调函数                                                     |
| delay    | Number   | 否   | 延迟的时间，函数的调用会在该延迟之后发生，单位 ms            |
| rest     | Any      | 否   | param1, param2, ..., paramN 等附加参数，它们会作为参数传递给回调函数 |

**返回值**

| 返回值    | 类型   | 说明                                                         |
| :-------- | :----- | :----------------------------------------------------------- |
| timeoutID | Number | 定时器的编号，这个值可以传递给 [clearTimeout](https://uniapp.dcloud.net.cn/api/timer#cleartimeout) 来取消该定时 |

##### `2.2.2 clearTimeout(timeoutID)`

取消由 setTimeout 设置的定时器。

**参数说明**

| 参数      | 类型   | 必填 | 说明                |
| :-------- | :----- | :--- | :------------------ |
| timeoutID | Number | 是   | 要取消的定时器的 ID |

##### `2.2.3 setInterval(callback, delay, rest)`

设定一个定时器。按照指定的周期（以毫秒计）来执行注册的回调函数

**参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| callback | Function | 是   | 回调函数                                                     |
| delay    | Number   | 否   | 执行回调函数之间的时间间隔，单位 ms                          |
| rest     | Any      | 否   | param1, param2, ..., paramN 等附加参数，它们会作为参数传递给回调函数 |

**返回值**

| 返回值     | 类型   | 说明                                                         |
| :--------- | :----- | :----------------------------------------------------------- |
| intervalID | Number | 定时器的编号，这个值可以传递给 [clearInterval](https://uniapp.dcloud.net.cn/api/timer#clearinterval) 来取消该定时 |

##### `2.2.4 clearInterval(intervalID)`

取消由 setInterval 设置的定时器。

**参数说明**

| 参数       | 类型   | 必填 | 说明                |
| :--------- | :----- | :--- | :------------------ |
| intervalID | Number | 是   | 要取消的定时器的 ID |



#### 2.3 [Base64 转 ArrayBuffer](https://uniapp.dcloud.net.cn/api/base64ToArrayBuffer.html) & [Base64 转 ArrayBuffer](https://uniapp.dcloud.net.cn/api/arrayBufferToBase64.html)

##### `2.3.1 uni.base64ToArrayBuffer(base64)`

将 Base64 字符串转成 ArrayBuffer 对象

```javascript
const base64 = 'test'
const arrayBuffer = uni.base64ToArrayBuffer(base64)
```

##### `2.3.2 uni.arrayBufferToBase64(arrayBuffer)`

将 ArrayBuffer 对象转成 Base64 字符串

```javascript
const arrayBuffer = new Uint8Array([55, 55, 55])
const base64 = uni.arrayBufferToBase64(arrayBuffer)
```



#### [2.4 uni.getLaunchOptionsSync()](https://uniapp.dcloud.net.cn/api/getLaunchOptionsSync.html#getlaunchoptionssync)

* 获取启动时的参数。返回值与App.onLaunch的回调参数一致



#### [2.5 uni.getEnterOptionsSync()](https://uniapp.dcloud.net.cn/api/getEnterOptionsSync.html)

* 获取启动时的参数。



#### [2.6 uni.onPageNotFound(CALLBACK)](https://uniapp.dcloud.net.cn/api/application.html#onpagenotfound)

* 监听应用要打开的页面不存在事件。该事件与 `App.onPageNotFound` 的回调时机一致

* `uni.offPageNotFound(CALLBACK)`
  * 取消监听应用要打开的页面不存在事件。



#### [2.7 uni.onError(CALLBACK)](https://uniapp.dcloud.net.cn/api/application.html#onerror)

* 监听小程序错误事件。如脚本错误或 `API` 调用报错等。该事件与 `App.onError` 的回调时机与参数一致。
* `uni.offError(CALLBACK)`
  * 取消监听应用错误事件。



#### [2.8 uni.onAppShow(CALLBACK)](https://uniapp.dcloud.net.cn/api/application.html#onappshow)

* 监听应用切前台事件。该事件与 `App.onShow` 的回调参数一致。

* `uni.offAppShow(CALLBACK)`
  * 取消监听小程序切前台事件。



#### [2.9 uni.onAppHide(CALLBACK)](监听应用切后台事件。该事件与 `App.onHide` 的回调参数一致。)

* 监听应用切前台事件。该事件与 `App.onShow` 的回调参数一致。
* uni.offAppHide(CALLBACK)
  * 取消监听小程序切后台事件。



#### [2.10 拦截器](https://uniapp.dcloud.net.cn/api/interceptor.html)

##### `2.10.1 uni.addInterceptor(STRING, OBJECT)`

添加拦截器

* 仅支持异步接口，如：`uni.setStorage(OBJECT)`，暂不支持同步接口如：`uni.setStorageSync(KEY,DATA)`

* uniCloud请求云端接口时（callFunction、uploadFile等）也会使用uni.request发送请求，请确保拦截器内不错误的处理此类请求

* **STRING 参数说明**

  需要拦截的`api`名称，如：`uni.addInterceptor('request', OBJECT)` ，将拦截 `uni.request()`

* **OBJECT 参数说明**

| 参数名      | 类型     | 必填 | 默认值 | 说明                       | 平台差异说明 |
| :---------- | :------- | :--- | :----- | :------------------------- | :----------- |
| invoke      | Function | 否   |        | 拦截前触发                 |              |
| returnValue | Function | 否   |        | 方法调用后触发，处理返回值 |              |
| success     | Function | 否   |        | 成功回调拦截               |              |
| fail        | Function | 否   |        | 失败回调拦截               |              |
| complete    | Function | 否   |        | 完成回调拦截               |              |

```javascript
uni.request({
    url: 'request/login', //仅为示例，并非真实接口地址。
    success: (res) => {
        console.log(res.data);
        // 打印： {code:1,...}
    }
});

uni.addInterceptor('request', {
  invoke(args) {
    // request 触发前拼接 url 
    args.url = 'https://www.example.com/'+args.url
  },
  success(args) {
    // 请求成功后，修改code值为1
    args.data.code = 1
  }, 
  fail(err) {
    console.log('interceptor-fail',err)
  }, 
  complete(res) {
    console.log('interceptor-complete',res)
  }
})

uni.addInterceptor({
  returnValue(args) {
    // 只返回 data 字段
    return args.data
  }
})
```

##### `2.10.2 uni.removeInterceptor(STRING)`

删除拦截器

* **STRING 参数说明**

  需要删除拦截器的`api`名称

```javascript
uni.removeInterceptor('request')
```



#### [2.11 uni.canIUse(String)](https://uniapp.dcloud.net.cn/api/caniuse.html)

* 判断应用的 API，回调，参数，组件等是否在当前版本可用。

* 平台差异说明
* App、web 端暂不支持 `${API}.${method}.${param}.${options}` 方式调用，只支持 `${API}`

| App  |         Web         | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ程序 |
| :--: | :-----------------: | :--------: | :----------: | :--------: | :------------------------: | :----: |
|  √   | √ (uni-app 3.4.13+) |     √      |      √       |     √      |             √              |   √    |

**String 参数说明**

使用 `${API}.${method}.${param}.${options}` 或者 `${component}.${attribute}.${option}` 方式来调用，例如：

- `${API}` 代表 API 名字
- `${method}` 代表调用方式，有效值为return, success, object, callback
- `${param}` 代表参数或者返回值
- `${options}` 代表参数的可选值
- `${component}` 代表组件名字
- `${attribute}` 代表组件属性
- `${option}` 代表组件属性的可选值

```javascript
uni.canIUse('getSystemInfoSync.return.screenWidth');
uni.canIUse('getSystemInfo.success.screenWidth');
uni.canIUse('showToast.object.image');
uni.canIUse('request.object.method.GET');

uni.canIUse('live-player');
uni.canIUse('text.selectable');
uni.canIUse('button.open-type.contact');
```





### `3. 网路`

#### [3.1 uni.request(OBJECT)](https://uniapp.dcloud.net.cn/api/request/request.html)

发起网络请求。

**OBJECT 参数说明**

| 参数名               | 类型                      | 必填 | 默认值 | 说明                                                         | 平台差异说明                                                 |
| :------------------- | :------------------------ | :--- | :----- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| url                  | String                    | 是   |        | 开发者服务器接口地址                                         |                                                              |
| data                 | Object/String/ArrayBuffer | 否   |        | 请求的参数                                                   | App 3.3.7 以下不支持 ArrayBuffer 类型                        |
| header               | Object                    | 否   |        | 设置请求的 header，header 中不能设置 Referer                 | App、H5端会自动带上cookie，且H5端不可手动修改                |
| method               | String                    | 否   | GET    | 有效值详见下方说明                                           |                                                              |
| timeout              | Number                    | 否   | 60000  | 超时时间，单位 ms                                            | H5(HBuilderX 2.9.9+)、APP(HBuilderX 2.9.9+)、微信小程序（2.10.0）、支付宝小程序 |
| dataType             | String                    | 否   | json   | 如果设为 json，会对返回的数据进行一次 JSON.parse，非 json 不会进行 JSON.parse |                                                              |
| responseType         | String                    | 否   | text   | 设置响应的数据类型。合法值：text、arraybuffer                | 支付宝小程序不支持                                           |
| sslVerify            | Boolean                   | 否   | true   | 验证 ssl 证书                                                | 仅App安卓端支持（HBuilderX 2.3.3+），不支持离线打包          |
| withCredentials      | Boolean                   | 否   | false  | 跨域请求时是否携带凭证（cookies）                            | 仅H5支持（HBuilderX 2.6.15+）                                |
| firstIpv4            | Boolean                   | 否   | false  | DNS解析时优先使用ipv4                                        | 仅 App-Android 支持 (HBuilderX 2.8.0+)                       |
| enableHttp2          | Boolean                   | 否   | false  | 开启 http2                                                   | 微信小程序                                                   |
| enableQuic           | Boolean                   | 否   | false  | 开启 quic                                                    | 微信小程序                                                   |
| enableCache          | Boolean                   | 否   | false  | 开启 cache                                                   | 微信小程序、字节跳动小程序 2.31.0+                           |
| enableHttpDNS        | Boolean                   | 否   | false  | 是否开启 HttpDNS 服务。如开启，需要同时填入 httpDNSServiceId 。 HttpDNS 用法详见 [移动解析HttpDNS](https://developers.weixin.qq.com/miniprogram/dev/framework/ability/HTTPDNS.html) | 微信小程序                                                   |
| httpDNSServiceId     | String                    | 否   |        | HttpDNS 服务商 Id。 HttpDNS 用法详见 [移动解析HttpDNS](https://developers.weixin.qq.com/miniprogram/dev/framework/ability/HTTPDNS.html) | 微信小程序                                                   |
| enableChunked        | Boolean                   | 否   | false  | 开启 transfer-encoding chunked                               | 微信小程序                                                   |
| forceCellularNetwork | Boolean                   | 否   | false  | wifi下使用移动网络发送请求                                   | 微信小程序                                                   |
| enableCookie         | Boolean                   | 否   | false  | 开启后可在headers中编辑cookie                                | 支付宝小程序 10.2.33+                                        |
| cloudCache           | Object/Boolean            | 否   | false  | 是否开启云加速（详见[云加速服务](https://smartprogram.baidu.com/docs/develop/extended/component-codeless/cloud-speed/introduction/)） | 百度小程序 3.310.11+                                         |
| defer                | Boolean                   | 否   | false  | 控制当前请求是否延时至首屏内容渲染后发送                     | 百度小程序 3.310.11+                                         |
| success              | Function                  | 否   |        | 收到开发者服务器成功返回的回调函数                           |                                                              |
| fail                 | Function                  | 否   |        | 接口调用失败的回调函数                                       |                                                              |
| complete             | Function                  | 否   |        | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                                              |

**method 有效值**

注意：method有效值必须大写，每个平台支持的method有效值不同，详细见下表。

| method  | App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | 快手小程序 | 京东小程序 |
| :-----: | :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :--------: | :--------: |
|   GET   |  √   |  √   |     √      |      √       |     √      |             √              |     √      |     √      |
|  POST   |  √   |  √   |     √      |      √       |     √      |             √              |     √      |     √      |
|   PUT   |  √   |  √   |     √      |      x       |     √      |             √              |     x      |     x      |
| DELETE  |  √   |  √   |     √      |      x       |     √      |             x              |     x      |     x      |
| CONNECT |  x   |  √   |     √      |      x       |     x      |             x              |     x      |     x      |
|  HEAD   |  √   |  √   |     √      |      x       |     √      |             x              |     x      |     x      |
| OPTIONS |  √   |  √   |     √      |      x       |     √      |             x              |     x      |     x      |
|  TRACE  |  x   |  √   |     √      |      x       |     x      |             x              |     x      |     x      |

**success 返回参数说明**

| 参数       | 类型                      | 说明                                         |
| :--------- | :------------------------ | :------------------------------------------- |
| data       | Object/String/ArrayBuffer | 开发者服务器返回的数据                       |
| statusCode | Number                    | 开发者服务器返回的 HTTP 状态码               |
| header     | Object                    | 开发者服务器返回的 HTTP Response Header      |
| cookies    | `Array<string>`           | 开发者服务器返回的 cookies，格式为字符串数组 |

**data 数据说明**

最终发送给服务器的数据是 String 类型，如果传入的 data 不是 String 类型，会被转换成 String。转换规则如下：

- 对于 `GET` 方法，会将数据转换为 query string。例如 `{ name: 'name', age: 18 }` 转换后的结果是 `name=name&age=18`。
- 对于 `POST` 方法且 `header['content-type']` 为 `application/json` 的数据，会进行 JSON 序列化。
- 对于 `POST` 方法且 `header['content-type']` 为 `application/x-www-form-urlencoded` 的数据，会将数据转换为 query string。

```javascript
uni.request({
    url: 'https://www.example.com/request', //仅为示例，并非真实接口地址。
    data: {
        text: 'uni.request'
    },
    header: {
        'custom-header': 'hello' //自定义请求头信息
    },
    success: (res) => {
        console.log(res.data);
        this.text = 'request success';
    }
});
```

**返回值**

如果希望返回一个 `requestTask` 对象，需要至少传入 success / fail / complete 参数中的一个。例如：

```javascript
var requestTask = uni.request({
	url: 'https://www.example.com/request', //仅为示例，并非真实接口地址。
	complete: ()=> {}
});
requestTask.abort();
```

如果没有传入 success / fail / complete 参数，则会返回封装后的 Promise 对象：[Promise 封装](https://uniapp.dcloud.net.cn/api/#promise-封装)

通过 `requestTask`，可中断请求任务。

**requestTask 对象的方法列表**

| 方法               | 参数 | 说明                                                         |
| :----------------- | :--- | :----------------------------------------------------------- |
| abort              |      | 中断请求任务                                                 |
| offHeadersReceived |      | 取消监听 HTTP Response Header 事件，仅`微信小程序平台`支持，[文档详情](https://developers.weixin.qq.com/miniprogram/dev/api/RequestTask.offHeadersReceived.html) |
| onHeadersReceived  |      | 监听 HTTP Response Header 事件。会比请求完成事件更早，仅`微信小程序平台`支持，[文档详情](https://developers.weixin.qq.com/miniprogram/dev/api/RequestTask.onHeadersReceived.html) |

```javascript
const requestTask = uni.request({
	url: 'https://www.example.com/request', //仅为示例，并非真实接口地址。
	data: {
        name: 'name',
        age: 18
	},
	success: function(res) {
		console.log(res.data);
	}
});

// 中断请求任务
requestTask.abort();
```

- 请求的 `header` 中 `content-type` 默认为 `application/json`。
- 避免在 `header` 中使用中文，或者使用 encodeURIComponent 进行编码，否则在百度小程序报错。（来自：[快狗打车前端团队](https://juejin.im/user/2612095359650712)）
- 网络请求的 `超时时间` 可以统一在 `manifest.json` 中配置 [networkTimeout](https://uniapp.dcloud.net.cn/collocation/manifest#networktimeout)。
- H5 端本地调试需注意跨域问题，参考：[调试跨域问题解决方案](https://ask.dcloud.net.cn/article/35267)
- 注意由于百度小程序iOS客户端，请求失败时会进入fail回调，需要针对百度增加相应的处理以解决该问题。
- 注意小程序端不支持自动保持 cookie，服务器应避免验证 cookie。如果服务器无法修改，也可以使用一些模拟手段，比如这样的工具https://github.com/charleslo1/weapp-cookie 可以请求时带上 cookie 并将响应的 cookie 保存在本地。
- H5端 cookie 受跨域限制（和平时开发网站时一样），旧版的 uni.request 未支持 withCredentials 配置，可以直接使用 xhr 对象或者其他类库。
- 根据 W3C 规范，H5 端无法获取 response header 中 Set-Cookie、Set-Cookie2 这2个字段，对于跨域请求，允许获取的 response header 字段只限于“simple response header”和“Access-Control-Expose-Headers”（[详情](https://www.w3.org/TR/cors/#access-control-allow-credentials-response-header)）
- [uni-app 插件市场](https://ext.dcloud.net.cn/search?q=拦截器)有flyio、axios等三方封装的拦截器可用
- 低版本手机自身不支持 ipv6，如果服务器仅允许 ipv6，会导致老手机无法正常运行或访问速度非常慢
- localhost、127.0.0.1等服务器地址，只能在电脑端运行，手机端连接时不能访问。请使用标准IP并保证手机能连接电脑网络
- debug 模式，安卓端暂时无法获取响应头，url中含有非法字符（如未编码为%20的空格）时会请求失败
- iOS App第一次安装启动后，会弹出是否允许联网的询问框，在用户点击同意前，调用联网API会失败。请注意判断这种情况。比如官方提供的新闻模板示例（HBuilderX新建项目可选择），会判断如果无法联网，则提供一个错误页，提示用户设置网络及下拉刷新重试。
- 良好体验的App，还会判断当前是否处于飞行模式（[参考](https://ext.dcloud.net.cn/plugin?id=594)）、是wifi还是3G（[参考](https://uniapp.dcloud.io/api/system/network)）
- 部分安卓设备，真机运行或debug模式下的网速，低于release模式很多。
- 使用一些比较小众的证书机构（如：CFCA OV OCA）签发的 ssl 证书在安卓设备请求会失败，因为这些机构的根证书不在系统内置根证书库，可以更换其他常见机构签发的证书（如：Let's Encrypt），或者配置 sslVerify 为 false 关闭 ssl 证书验证（不推荐）。
- 离线打包不支持 `sslVerify` 配置
- 单次网络请求数据量建议控制在50K以下（仅指json数据，不含图片），过多数据应分页获取，以提升应用体验。



#### [3.2 uni.uploadFile(OBJECT) - 上传](https://uniapp.dcloud.net.cn/api/request/network-file.html#uploadfile)

将本地资源上传到开发者服务器，客户端发起一个 `POST` 请求，其中 `content-type` 为 `multipart/form-data`。
如页面通过 [uni.chooseImage](https://uniapp.dcloud.net.cn/api/media/image#chooseimage) 等接口获取到一个本地资源的临时文件路径后，可通过此接口将本地资源上传到指定服务器。另外选择和上传非图像、视频文件参考：https://ask.dcloud.net.cn/article/35547。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填                        | 说明                                                         | 平台差异说明                                |
| :------- | :------- | :-------------------------- | :----------------------------------------------------------- | :------------------------------------------ |
| url      | String   | 是                          | 开发者服务器 url                                             |                                             |
| files    | Array    | 是（files和filePath选其一） | 需要上传的文件列表。**使用 files 时，filePath 和 name 不生效。** | App、H5（ 2.6.15+）                         |
| fileType | String   | 见平台差异说明              | 文件类型，image/video/audio                                  | 仅支付宝小程序，且必填。                    |
| file     | File     | 否                          | 要上传的文件对象。                                           | 仅H5（2.6.15+）支持                         |
| filePath | String   | 是（files和filePath选其一） | 要上传文件资源的路径。                                       |                                             |
| name     | String   | 是                          | 文件对应的 key , 开发者在服务器端通过这个 key 可以获取到文件二进制内容 |                                             |
| header   | Object   | 否                          | HTTP 请求 Header, header 中不能设置 Referer。                |                                             |
| timeout  | Number   | 否                          | 超时时间，单位 ms                                            | H5(HBuilderX 2.9.9+)、APP(HBuilderX 2.9.9+) |
| formData | Object   | 否                          | HTTP 请求中其他额外的 form data                              |                                             |
| success  | Function | 否                          | 接口调用成功的回调函数                                       |                                             |
| fail     | Function | 否                          | 接口调用失败的回调函数                                       |                                             |
| complete | Function | 否                          | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                             |

**注意**：

- App支持多文件上传，微信小程序只支持单文件上传，传多个文件需要反复调用本API。所以跨端的写法就是循环调用本API。
- hello uni-app中的客服反馈，支持多图上传。[uni-app插件市场](https://ext.dcloud.net.cn/)中也有多个封装的组件。
- App平台选择和上传非图像、视频文件，参考https://ask.dcloud.net.cn/article/35547
- 网络请求的 `超时时间` 可以统一在 `manifest.json` 中配置 [networkTimeout](https://uniapp.dcloud.net.cn/collocation/manifest#networktimeout)。
- 支付宝小程序开发工具上传文件返回的http状态码为字符串形式，支付宝小程序真机返回的状态码为数字形式

**files参数说明**

files 参数是一个 file 对象的数组，file 对象的结构如下：

| 参数名 | 类型   | 必填 | 说明                                        |
| :----- | :----- | :--- | :------------------------------------------ |
| name   | String | 否   | multipart 提交时，表单的项目名，默认为 file |
| file   | File   | 否   | 要上传的文件对象，仅H5（2.6.15+）支持       |
| uri    | String | 是   | 文件的本地地址                              |

Tip:

- 如果 `name` 不填或填的值相同，可能导致服务端读取文件时只能读取到一个文件。

**success 返回参数说明**

| 参数       | 类型   | 说明                           |
| :--------- | :----- | :----------------------------- |
| data       | String | 开发者服务器返回的数据         |
| statusCode | Number | 开发者服务器返回的 HTTP 状态码 |

```javascript
uni.chooseImage({
	success: (chooseImageRes) => {
		const tempFilePaths = chooseImageRes.tempFilePaths;
		uni.uploadFile({
			url: 'https://www.example.com/upload', //仅为示例，非真实的接口地址
			filePath: tempFilePaths[0],
			name: 'file',
			formData: {
				'user': 'test'
			},
			success: (uploadFileRes) => {
				console.log(uploadFileRes.data);
			}
		});
	}
});
```

**返回值**

如果希望返回一个 `uploadTask` 对象，需要至少传入 success / fail / complete 参数中的一个。例如：

```javascript
var uploadTask = uni.uploadFile({
	url: 'https://www.example.com/upload', //仅为示例，并非真实接口地址。
	complete: ()=> {}
});
uploadTask.abort();
```

如果没有传入 success / fail / complete 参数，则会返回封装后的 Promise 对象：[Promise 封装](https://uniapp.dcloud.net.cn/api/#promise-封装)

通过 `uploadTask`，可监听上传进度变化事件，以及取消上传任务。

**uploadTask 对象的方法列表**

| 方法               | 参数     | 说明                                                         |
| :----------------- | :------- | :----------------------------------------------------------- |
| abort              |          | 中断上传任务                                                 |
| onProgressUpdate   | callback | 监听上传进度变化                                             |
| onHeadersReceived  | callback | 监听 HTTP Response Header 事件。会比请求完成事件更早,仅`微信小程序平台`支持，[规范详情](https://developers.weixin.qq.com/miniprogram/dev/api/UploadTask.onHeadersReceived.html) |
| offProgressUpdate  | callback | 取消监听上传进度变化事件，仅`微信小程序平台`支持，[规范详情](https://developers.weixin.qq.com/miniprogram/dev/api/UploadTask.offProgressUpdate.html) |
| offHeadersReceived | callback | 取消监听 HTTP Response Header 事件，仅`微信小程序平台`支持，[规范详情](https://developers.weixin.qq.com/miniprogram/dev/api/UploadTask.offHeadersReceived.html) |

**onProgressUpdate 返回参数说明**

| 参数                     | 类型   | 说明                                 |
| :----------------------- | :----- | :----------------------------------- |
| progress                 | Number | 上传进度百分比                       |
| totalBytesSent           | Number | 已经上传的数据长度，单位 Bytes       |
| totalBytesExpectedToSend | Number | 预期需要上传的数据总长度，单位 Bytes |

```javascript
uni.chooseImage({
	success: (chooseImageRes) => {
		const tempFilePaths = chooseImageRes.tempFilePaths;
		const uploadTask = uni.uploadFile({
			url: 'https://www.example.com/upload', //仅为示例，非真实的接口地址
			filePath: tempFilePaths[0],
			name: 'file',
			formData: {
				'user': 'test'
			},
			success: (uploadFileRes) => {
				console.log(uploadFileRes.data);
			}
		});

		uploadTask.onProgressUpdate((res) => {
			console.log('上传进度' + res.progress);
			console.log('已经上传的数据长度' + res.totalBytesSent);
			console.log('预期需要上传的数据总长度' + res.totalBytesExpectedToSend);

			// 测试条件，取消上传任务。
			if (res.progress > 50) {
				uploadTask.abort();
			}
		});
	}
});
```



#### [3.3 uni.downloadFile(OBJECT) - 下载](https://uniapp.dcloud.net.cn/api/request/network-file.html#downloadfile)

下载文件资源到本地，客户端直接发起一个 HTTP GET 请求，返回文件的本地临时路径。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                                         | 平台差异说明                                                 |
| :------- | :------- | :--- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| url      | String   | 是   | 下载资源的 url                                               |                                                              |
| header   | Object   | 否   | HTTP 请求 Header, header 中不能设置 Referer。                |                                                              |
| timeout  | Number   | 否   | 超时时间，单位 ms                                            | H5(HBuilderX 2.9.9+)、APP(HBuilderX 2.9.9+)                  |
| success  | Function | 否   | 下载成功后以 tempFilePath 的形式传给页面，res = {tempFilePath: '文件的临时路径'} |                                                              |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |                                                              |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                                              |
| filePath | string   | 否   | 指定文件下载后存储的路径 (本地路径)                          | 微信小程序（IOS小程序保存到相册需要添加此字段才可以正常保存） |

**注：文件的临时路径，在应用本次启动期间可以正常使用，如需持久保存，需在主动调用 [uni.saveFile](https://uniapp.dcloud.net.cn/api/file/file#savefile)，才能在应用下次启动时访问得到。**

**success 返回参数说明**

| 参数         | 类型   | 说明                                           |
| :----------- | :----- | :--------------------------------------------- |
| tempFilePath | String | 临时文件路径，下载后的文件会存储到一个临时文件 |
| statusCode   | Number | 开发者服务器返回的 HTTP 状态码                 |

**注意**

- 网络请求的 `超时时间` 可以统一在 `manifest.json` 中配置 [networkTimeout](https://uniapp.dcloud.net.cn/collocation/manifest#networktimeout)。

```javascript
uni.downloadFile({
	url: 'https://www.example.com/file/test', //仅为示例，并非真实的资源
	success: (res) => {
		if (res.statusCode === 200) {
			console.log('下载成功');
		}
	}
});
```

**返回值**

如果希望返回一个 `downloadTask` 对象，需要至少传入 success / fail / complete 参数中的一个。例如：

```javascript
var downloadTask = uni.downloadFile({
	url: 'https://www.example.com/file/test', //仅为示例，并非真实接口地址。
	complete: ()=> {}
});
downloadTask.abort();
```

如果没有传入 success / fail / complete 参数，则会返回封装后的 Promise 对象：[Promise 封装](https://uniapp.dcloud.net.cn/api/#promise-封装)

通过 `downloadTask`，可监听下载进度变化事件，以及取消下载任务。

**downloadTask 对象的方法列表**

| 方法               | 参数     | 说明                                                         | 最低版本 |
| :----------------- | :------- | :----------------------------------------------------------- | :------- |
| abort              |          | 中断下载任务                                                 | *        |
| onProgressUpdate   | callback | 监听下载进度变化                                             | *        |
| onHeadersReceived  | callback | 监听 HTTP Response Header 事件，会比请求完成事件更早,仅`微信小程序平台`支持，[规范详情](https://developers.weixin.qq.com/miniprogram/dev/api/DownloadTask.onHeadersReceived.html) |          |
| offProgressUpdate  | callback | 取消监听下载进度变化事件，仅`微信小程序平台`支持，[规范详情](https://developers.weixin.qq.com/miniprogram/dev/api/DownloadTask.offProgressUpdate.html) |          |
| offHeadersReceived | callback | 取消监听 HTTP Response Header 事件，仅`微信小程序平台`支持，[规范详情](https://developers.weixin.qq.com/miniprogram/dev/api/DownloadTask.offHeadersReceived.html) |          |

**onProgressUpdate 返回参数说明**

| 参数                      | 类型   | 说明                                 |
| :------------------------ | :----- | :----------------------------------- |
| progress                  | Number | 下载进度百分比                       |
| totalBytesWritten         | Number | 已经下载的数据长度，单位 Bytes       |
| totalBytesExpectedToWrite | Number | 预期需要下载的数据总长度，单位 Bytes |

```javascript
const downloadTask = uni.downloadFile({
	url: 'http://www.example.com/file/test', //仅为示例，并非真实的资源
	success: (res) => {
		if (res.statusCode === 200) {
			console.log('下载成功');
		}
	}
});

downloadTask.onProgressUpdate((res) => {
	console.log('下载进度' + res.progress);
	console.log('已经下载的数据长度' + res.totalBytesWritten);
	console.log('预期需要下载的数据总长度' + res.totalBytesExpectedToWrite);

	// 满足测试条件，取消下载任务。
	if (res.progress > 50) {
		downloadTask.abort();
	}
});
```



#### [3.4 WebSocket](https://uniapp.dcloud.net.cn/api/request/websocket.html)

用到再看。



#### [3.5 SocketTask](https://uniapp.dcloud.net.cn/api/request/socket-task.html)

用到再看。



### `4. 页面和路由`

#### [4.1 uni.navigateTo(OBJECT)](https://uniapp.dcloud.net.cn/api/router.html#navigateto)

* 保留当前页面，跳转到应用内的某个页面，使用`uni.navigateBack`可以返回到原页面。

**OBJECT参数说明**

| 参数              | 类型     | 必填 | 默认值 | 说明                                                         | 平台差异说明 |
| :---------------- | :------- | :--- | :----- | :----------------------------------------------------------- | :----------- |
| url               | String   | 是   |        | 需要跳转的应用内非 tabBar 的页面的路径 , 路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2'，path为下一个页面的路径，下一个页面的onLoad函数可得到传递的参数 |              |
| animationType     | String   | 否   | pop-in | 窗口显示的动画效果，详见：[窗口动画](https://uniapp.dcloud.net.cn/api/router#animation) | App          |
| animationDuration | Number   | 否   | 300    | 窗口动画持续时间，单位为 ms                                  | App          |
| events            | Object   | 否   |        | 页面间通信接口，用于监听被打开页面发送到当前页面的数据。2.8.9+ 开始支持。 |              |
| success           | Function | 否   |        | 接口调用成功的回调函数                                       |              |
| fail              | Function | 否   |        | 接口调用失败的回调函数                                       |              |
| complete          | Function | 否   |        | 接口调用结束的回调函数（调用成功、失败都会执行）             |              |

**object.success 回调函数**

**参数**

**Object res**

| 属性         | 类型                                                         | 说明                 |
| :----------- | :----------------------------------------------------------- | :------------------- |
| eventChannel | [EventChannel](https://uniapp.dcloud.net.cn/api/router#event-channel) | 和被打开页面进行通信 |

```javascript
// 在起始页面跳转到test.vue页面，并监听test.vue发送过来的事件数据
uni.navigateTo({
  url: 'pages/test?id=1',
  events: {
    // 为指定事件添加一个监听器，获取被打开页面传送到当前页面的数据
    acceptDataFromOpenedPage: function(data) {
      console.log(data)
    },
    someEvent: function(data) {
      console.log(data)
    }
    ...
  },
  success: function(res) {
    // 通过eventChannel向被打开页面传送数据
    res.eventChannel.emit('acceptDataFromOpenerPage', { data: 'data from starter page' })
  }
})

// 在test.vue页面，向起始页通过事件传递数据
onLoad: function(option) {
  const eventChannel = this.getOpenerEventChannel();
  eventChannel.emit('acceptDataFromOpenedPage', {data: 'data from test page'});
  eventChannel.emit('someEvent', {data: 'data from test page for someEvent'});
  // 监听acceptDataFromOpenerPage事件，获取上一页面通过eventChannel传送到当前页面的数据
  eventChannel.on('acceptDataFromOpenerPage', function(data) {
    console.log(data)
  })
}
```

* url有长度限制，太长的字符串会传递失败，可改用[窗体通信](https://uniapp.dcloud.io/collocation/frame/communication)、[全局变量](https://ask.dcloud.net.cn/article/35021)，另外参数中出现空格等特殊字符时需要对参数进行编码，如下为使用`encodeURIComponent`对参数进行编码的示例。

```javascript
<navigator :url="'/pages/test/test?item='+ encodeURIComponent(JSON.stringify(item))"></navigator>

// 在test.vue页面接受参数
onLoad: function (option) {
	const item = JSON.parse(decodeURIComponent(option.item));
}
```

- 页面跳转路径有层级限制，不能无限制跳转新页面
- 跳转到 tabBar 页面只能使用 switchTab 跳转
- 路由API的目标页面必须是在pages.json里注册的vue页面。如果想打开web url，在App平台可以使用 [plus.runtime.openURL](http://www.html5plus.org/doc/zh_cn/runtime.html#plus.runtime.openURL)或web-view组件；H5平台使用 window.open；小程序平台使用web-view组件（url需在小程序的联网白名单中）。在hello uni-app中有个组件ulink.vue已对多端进行封装，可参考。



#### [4.2 uni.redirectTo(OBJECT)](https://uniapp.dcloud.net.cn/api/router.html#redirectto)

* 关闭当前页面，跳转到应用内的某个页面。

- 跳转到 tabBar 页面只能使用 switchTab 跳转

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| url      | String   | 是   | 需要跳转的应用内非 tabBar 的页面的路径，路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2' |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

```javascript
uni.redirectTo({
	url: 'test?id=1'
});
```



#### [4.3 uni.reLaunch(OBJECT)](https://uniapp.dcloud.net.cn/api/router.html#relaunch)

* 关闭所有页面，打开到应用内的某个页面。
* 如果调用了 [uni.preloadPage(OBJECT)](https://uniapp.dcloud.net.cn/api/preload-page) 不会关闭，仅触发生命周期 `onHide`
* H5端调用`uni.reLaunch`之后之前页面栈会销毁，但是无法清空浏览器之前的历史记录，此时`navigateBack`不能返回，如果存在历史记录的话点击浏览器的返回按钮或者调用`history.back()`仍然可以导航到浏览器的其他历史记录。

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| url      | String   | 是   | 需要跳转的应用内页面路径 , 路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2'，如果跳转的页面路径是 tabBar 页面则不能带参数 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

```javascript
uni.reLaunch({
	url: 'test?id=1'
});
```



#### [4.4 uni.switchTab(OBJECT)](https://uniapp.dcloud.net.cn/api/router.html#switchtab)

* 跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面。
*  如果调用了 [uni.preloadPage(OBJECT)](https://uniapp.dcloud.net.cn/api/preload-page) 不会关闭，仅触发生命周期 `onHide`

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| url      | String   | 是   | 需要跳转的 tabBar 页面的路径（需在 pages.json 的 tabBar 字段定义的页面），路径后不能带参数 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

```json
{
  "tabBar": {
    "list": [{
      "pagePath": "pages/index/index",
      "text": "首页"
    },{
      "pagePath": "pages/other/other",
      "text": "其他"
    }]
  }
}
```

```javascript
uni.switchTab({
	url: '/pages/index/index'
});
```



#### [4.5 uni.navigateBack(OBJECT)](https://uniapp.dcloud.net.cn/api/router.html#navigateback)

* 关闭当前页面，返回上一页面或多级页面。可通过 `getCurrentPages()` 获取当前的页面栈，决定需要返回几层。

**OBJECT参数说明**

| 参数              | 类型     | 必填 | 默认值                                           | 说明                                                         | 平台差异说明 |
| :---------------- | :------- | :--- | :----------------------------------------------- | :----------------------------------------------------------- | :----------- |
| delta             | Number   | 否   | 1                                                | 返回的页面数，如果 delta 大于现有页面数，则返回到首页。      |              |
| animationType     | String   | 否   | pop-out                                          | 窗口关闭的动画效果，详见：[窗口动画](https://uniapp.dcloud.net.cn/api/router#animation) | App          |
| animationDuration | Number   | 否   | 300                                              | 窗口关闭动画的持续时间，单位为 ms                            | App          |
| success           | Function | 否   | 接口调用成功的回调函数                           |                                                              |              |
| fail              | Function | 否   | 接口调用失败的回调函数                           |                                                              |              |
| complete          | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |                                                              |              |

```javascript
// 注意：调用 navigateTo 跳转时，调用该方法的页面会被加入堆栈，而 redirectTo 方法则不会。见下方示例代码

// 此处是A页面
uni.navigateTo({
	url: 'B?id=1'
});

// 此处是B页面
uni.navigateTo({
	url: 'C?id=1'
});

// 在C页面内 navigateBack，将返回A页面
uni.navigateBack({
	delta: 2
});
```



#### [4.6 uni.preloadPage(OBJECT)](https://uniapp.dcloud.net.cn/api/preload-page.html#preloadpage)

预加载页面，是一种性能优化技术。被预载的页面，在打开时速度更快。

**平台差异说明**

|  App-nvue  |     H5     | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 |
| :--------: | :--------: | :--------: | :----------: | :--------: | :------------------------: | :------: |
| √(2.7.12+) | √(2.7.12+) |     x      |      x       |     x      |             x              |    x     |

**OBJECT参数说明**

|   属性   |   类型   | 必填 |                       说明                       |
| :------: | :------: | :--: | :----------------------------------------------: |
|   url    |  string  |  是  |                  预加载页面url                   |
| success  | Function |  否  |                预加载成功完成回调                |
|   fail   | Function |  否  |                  预加载失败回调                  |
| complete | Function |  否  | 接口调用结束的回调函数（调用成功、失败都会执行） |

* H5 平台

预加载 /pages/test/test 对应的js文件，不执行页面预渲染逻辑

```js
uni.preloadPage({url: "/pages/test/test"});
```

* App-nvue 平台

预加载nvue页面 /pages/test/test

```js
uni.preloadPage({url: "/pages/test/test"});
```

注意事项

1. App平台仅支持预加载 nvue 页面，执行页面预渲染，预载时触发生命周期 `onLoad`，`onReady`，不触发 `onShow`
2. 打开新页面时，url 完全相同（包含参数）时，优先使用预加载页面，触发生命周期 onShow
3. tabbar页面，仅支持预加载尚未显示过的页面，否则返回 fail，提示 already exists
4. 同一时间，相同 url 仅 preloadPage 一次
5. 当同一个预载页面已被打开(在路由栈)，再次打开相同url时，不再使用该预加载页面，而是打开新的非预载页面
6. `uni.reLanuch`, `uni.switchTab`, `uni.navigateBack`(含Android返回键) 切换页面时，预加载页面不会被销毁，仅触发生命周期 `onHide`
7. 在预载页面使用 `uni.redirectTo` 时，预加载页面会被销毁，触发生命周期 `onUnload`

示例

```js
uni.preloadPage({url: "/pages/test/test"}); // 预加载 /pages/test/test 页面（仅触发onLoad，onReady)
uni.navigateTo({url: "/pages/test/test"}); // url匹配，跳转预加载页面（仅触发onShow)
uni.navigateTo({url: "/pages/test/test?a=b"}); // url不匹配，正常打开新页面
```

* HBuilderX 2.7.12+的hello uni-app，在navigator示例和uni ui的日历示例中增加了页面预载示例。



#### [4.7 uni.unPreloadPage(OBJECT)](https://uniapp.dcloud.net.cn/api/preload-page.html#unpreloadpage)

取消预载页面。

1. 仅App-nvue支持
2. 当预载页面未被打开时，使用 `unPreloadPage`时会销毁该页面，触发生命周期 `onUnload`
3. 当预载页面已被打开时，使用 `unPreloadPage`时不销毁该页面，但该预加载页面不再继续存在，会随着路由变化而销毁



#### [4.8 窗口动画](https://uniapp.dcloud.net.cn/api/router.html#animation)

窗口的显示/关闭动画效果，支持在 API、组件、pages.json 中配置，优先级为：`(API == 组件) > pages.json`。

##### `4.8.1 API`

有效的路由 API

- navigateTo
- navigateBack

```javascript
uni.navigateTo({
	url: '../test/test',
	animationType: 'pop-in',
	animationDuration: 200
});
uni.navigateBack({
	delta: 1,
	animationType: 'pop-out',
	animationDuration: 200
});
```

##### `4.8.2 组件`

open-type 有效值

- navigateTo
- navigateBack

```html
<navigator animation-type="pop-in" animation-duration="300" url="../test/test">navigator</navigator>
<navigator animation-type="pop-out" animation-duration="300" open-type="navigateBack" >navigator</navigator>
```

##### `4.8.3 pages.json`

```json
"style": {
	"app-plus": {
		"animationType": "fade-in",
		"animationDuration": 300
	}
}
```

显示动画与关闭动画，会有默认的对应规则。但是如果通过 API 或组件配置了窗口关闭的动画类型，则不会使用默认的类型。

| 显示动画        | 关闭动画         | 显示动画描述（关闭动画与之相反）                 |
| :-------------- | :--------------- | :----------------------------------------------- |
| slide-in-right  | slide-out-right  | 新窗体从右侧进入                                 |
| slide-in-left   | slide-out-left   | 新窗体从左侧进入                                 |
| slide-in-top    | slide-out-top    | 新窗体从顶部进入                                 |
| slide-in-bottom | slide-out-bottom | 新窗体从底部进入                                 |
| pop-in          | pop-out          | 新窗体从左侧进入，且老窗体被挤压而出             |
| fade-in         | fade-out         | 新窗体从透明到不透明逐渐显示                     |
| zoom-out        | zoom-in          | 新窗体从小到大缩放显示                           |
| zoom-fade-out   | zoom-fade-in     | 新窗体从小到大逐渐放大并且从透明到不透明逐渐显示 |
| none            | none             | 无动画                                           |

- 纯nvue项目（render为native），窗体动画默认进入动画为popin，返回为pop-out。如果想修改动画类型，只能通过uni.navigateTo API修改，在组件或pages.json里配置动画类型无效
- 非纯nvue项目，App端窗体动画，默认进入动画为slider-in-right，默认返回动画为pop-out
- webview 中嵌入 uni-app H5时，使用 uni.webView.navigateTo... 跳转页面



#### `4.9 页面`

##### [4.9.1 getCurrentPages](https://uniapp.dcloud.net.cn/api/window/window.html#getcurrentpages)

* `getCurrentPages()` 函数用于获取当前页面栈的实例，以数组形式按栈的顺序给出，第一个元素为首页，最后一个元素为当前页面。
* `getCurrentPages()`仅用于展示页面栈的情况，请勿修改页面栈，以免造成页面状态错误。

每个页面实例的方法属性列表：

| 方法                  | 描述                          | 平台说明 |
| --------------------- | ----------------------------- | -------- |
| page.$getAppWebview() | 获取当前页面的webview对象实例 | App      |
| page.$vm              | 当前页面的 Vue 实例           |          |
| page.route            | 获取当前页面的路由            |          |

- `navigateTo`, `redirectTo` 只能打开非 tabBar 页面。
- `switchTab` 只能打开 `tabBar` 页面。
- `reLaunch` 可以打开任意页面。
- 页面底部的 `tabBar` 由页面决定，即只要是定义为 `tabBar` 的页面，底部都有 `tabBar`。
- 不能在 `App.vue` 里面进行页面跳转。



##### [4.9.2 $getAppWebview()](https://uniapp.dcloud.net.cn/api/window/window.html#getappwebview)

`uni-app` 在 `getCurrentPages()`获得的页面里内置了一个方法 `$getAppWebview()` 可以得到当前webview的对象实例，从而实现对 webview 更强大的控制。在 html5Plus 中，plus.webview具有强大的控制能力，可参考：[WebviewObject](http://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject)。

但`uni-app`框架有自己的窗口管理机制，请不要自己创建和销毁webview，如有需求覆盖子窗体上去，请使用[原生子窗体subNvue](https://uniapp.dcloud.net.cn/api/window/subNVues)。

* 获取当前页面 webview 的对象实例

```javascript
export default {
  data() {
    return {
      title: 'Hello'
    }
  },
  onLoad() {
    // #ifdef APP-PLUS
    const currentWebview = this.$scope.$getAppWebview(); //此对象相当于html5plus里的plus.webview.currentWebview()。在uni-app里vue页面直接使用plus.webview.currentWebview()无效
    currentWebview.setBounce({position:{top:'100px'},changeoffset:{top:'0px'}}); //动态重设bounce效果
    // #endif
  }
}
```

* 获取指定页面 webview 的对象实例

```javascript
var pages = getCurrentPages();
var page = pages[pages.length - 1];
// #ifdef APP-PLUS
var currentWebview = page.$getAppWebview();
console.log(currentWebview.id);//获得当前webview的id
console.log(currentWebview.isVisible());//查询当前webview是否可见
// #endif
```



##### [4.9.3 $vm](https://uniapp.dcloud.net.cn/api/window/window.html#vm)

通过页面的 Vue 实例可以获取页面的数据、调用页面上的方法以及监听页面的生命周期等

```javascript
const page = getCurrentPages()[0];
const vm = page.$vm;
// 监听生命周期，小程序端部分其他生命周期需在页面选项中配置过才可生效
vm.$on('hook:onHide', () => {
  console.log('onHide');
});
// 获取页面数据
console.log(vm.$data.title);
// 调用页面方法
vm.test();
```



#### [4.10 EventChannel](https://uniapp.dcloud.net.cn/api/router.html#event-channel)

* #### `EventChannel.emit(string eventName, any args)`

* #### `EventChannel.off(string eventName, function fn)`

* `EventChannel.on(string eventName, function fn)`

* #### `EventChannel.once(string eventName, function fn)`

```javascript
uni.navigateTo({
  url: 'pages/test?id=1',
  events: {
    // 为指定事件添加一个监听器，获取被打开页面传送到当前页面的数据
    acceptDataFromOpenedPage: function(data) {
      console.log(data)
    },
    someEvent: function(data) {
      console.log(data)
    }
    ...
  },
  success: function(res) {
    // 通过eventChannel向被打开页面传送数据
    res.eventChannel.emit('acceptDataFromOpenerPage', { data: 'test' })
  }
})

// uni.navigateTo 目标页面 pages/test.vue
onLoad: function(option) {
  console.log(option.query)
  const eventChannel = this.getOpenerEventChannel()
  eventChannel.emit('acceptDataFromOpenedPage', {data: 'test'});
  eventChannel.emit('someEvent', {data: 'test'});
  // 监听acceptDataFromOpenerPage事件，获取上一页面通过eventChannel传送到当前页面的数据
  eventChannel.on('acceptDataFromOpenerPage', function(data) {
    console.log(data)
  })
}
```



#### [4.11 页面通讯](https://uniapp.dcloud.net.cn/api/window/communication.html)

* `uni.$emit(eventName,OBJECT)`
* `uni.$on(eventName,callback)`
* `uni.$once(eventName,callback)`
* `uni.$off([eventName, callback])`

* **Tip:**

  - uni.$emit、 uni.$on 、 uni.$once 、uni.$off 触发的事件都是 App 全局级别的，跨任意组件，页面，nvue，vue 等

  - 使用时，注意及时销毁事件监听，比如，页面 onLoad 里边 uni.$on 注册监听，onUnload 里边 uni.$off 移除，或者一次性的事件，直接使用 uni.$once 监听

  - 注意 uni.$on 定义完成后才能接收到 uni.$emit 传递的数据
  - `和EventChannel的区别`: EventChannel只能用在(N)Vue页面, 通过this.getOpenerEventChannel()来获取EventChannel对象, 而uni.$emit可以作用于全局。



#### [4.12 subNvue 原生子窗体](https://uniapp.dcloud.net.cn/api/window/subNVues.html)

用到再看。



### [5. 数据缓存](https://uniapp.dcloud.net.cn/api/storage/storage.html#)

#### `5.1 异步操作`

* `uni.setStorage(OBJECT)`

将数据存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个异步接口。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| key      | String   | 是   | 本地缓存中的指定的 key                                       |
| data     | Any      | 是   | 需要存储的内容，只支持原生类型、及能够通过 JSON.stringify 序列化的对象 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

```javascript
uni.setStorage({
	key: 'storage_key',
	data: 'hello',
	success: function () {
		console.log('success');
	}
});
```

* `uni.getStorage(OBJECT)`

从本地缓存中异步获取指定 key 对应的内容。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| key      | String   | 是   | 本地缓存中的指定的 key                           |
| success  | Function | 是   | 接口调用的回调函数，res = {data: key对应的内容}  |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**success 返回参数说明**

| 参数 | 类型 | 说明           |
| :--- | :--- | :------------- |
| data | Any  | key 对应的内容 |

```javascript
uni.getStorage({
	key: 'storage_key',
	success: function (res) {
		console.log(res.data);
	}
});
```

* `uni.getStorageInfo(OBJECT)`

异步获取当前 storage 的相关信息。

**平台差异说明**

|       App        |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 |
| :--------------: | :--: | :--------: | :----------: | :--------: |
| HBuilderX 2.0.3+ |  √   |     √      |      √       |     √      |

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| success  | Function | 是   | 接口调用的回调函数，详见返回参数说明             |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**success 返回参数说明**

| 参数        | 类型            | 说明                         |
| :---------- | :-------------- | :--------------------------- |
| keys        | Array＜String＞ | 当前 storage 中所有的 key    |
| currentSize | Number          | 当前占用的空间大小, 单位：kb |
| limitSize   | Number          | 限制的空间大小, 单位：kb     |

```javascript
uni.getStorageInfo({
	success: function (res) {
		console.log(res.keys);
		console.log(res.currentSize);
		console.log(res.limitSize);
	}
});
```

* `uni.removeStorage(OBJECT)`

从本地缓存中异步移除指定 key。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| key      | String   | 是   | 本地缓存中的指定的 key                           |
| success  | Function | 是   | 接口调用的回调函数                               |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.removeStorage({
	key: 'storage_key',
	success: function (res) {
		console.log('success');
	}
});
```

* `uni.clearStorage()`

清理本地数据缓存。

```javascript
uni.clearStorage();
```



#### `5.2 同步操作`

* `uni.setStorageSync(KEY,DATA)`

  将 data 存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个同步接口。

  **参数说明**

  | 参数 | 类型   | 必填 | 说明                                                         |
  | :--- | :----- | :--- | :----------------------------------------------------------- |
  | key  | String | 是   | 本地缓存中的指定的 key                                       |
  | data | Any    | 是   | 需要存储的内容，只支持原生类型、及能够通过 JSON.stringify 序列化的对象 |

  ```javascript
  try {
  	uni.setStorageSync('storage_key', 'hello');
  } catch (e) {
  	// error
  }
  ```

* `uni.getStorageSync(KEY)`

从本地缓存中同步获取指定 key 对应的内容。

**参数说明**

| 参数 | 类型   | 必填 | 说明                   |
| :--- | :----- | :--- | :--------------------- |
| key  | String | 是   | 本地缓存中的指定的 key |

```javascript
try {
	const value = uni.getStorageSync('storage_key');
	if (value) {
		console.log(value);
	}
} catch (e) {
	// error
}
```

* `uni.getStorageInfoSync()`

同步获取当前 storage 的相关信息。

```javascript
try {
	const res = uni.getStorageInfoSync();
	console.log(res.keys);
	console.log(res.currentSize);
	console.log(res.limitSize);
} catch (e) {
	// error
}
```

* `uni.removeStorageSync(KEY)`

从本地缓存中同步移除指定 key。

```javascript
try {
	uni.removeStorageSync('storage_key');
} catch (e) {
	// error
}
```

* `uni.clearStorageSync()`

同步清理本地数据缓存。

```javascript
try {
	uni.clearStorageSync();
} catch (e) {
	// error
}
```

- H5端为localStorage，浏览器限制5M大小，是缓存概念，可能会被清理
- App端为原生的plus.storage，无大小限制，不是缓存，是持久化的
- 各个小程序端为其自带的storage api，数据存储生命周期跟小程序本身一致，即除用户主动删除或超过一定时间被自动清理，否则数据都一直可用。
- 微信小程序单个 key 允许存储的最大数据长度为 1MB，所有数据存储上限为 10MB。
- 支付宝小程序单条数据转换成字符串后，字符串长度最大200*1024。同一个支付宝用户，同一个小程序缓存总上限为10MB。
- 百度小程序策略[详见](https://smartprogram.baidu.com/docs/develop/api/storage/save_process/)、字节跳动小程序策略[详见](https://microapp.bytedance.com/docs/zh-CN/mini-app/develop/api/data-caching/tt-get-storage)
- 非App平台清空Storage会导致uni.getSystemInfo获取到的deviceId改变

除此之外，其他数据存储方案：

- H5端还支持websql、indexedDB、sessionStorage
- App端还支持[SQLite](https://www.html5plus.org/doc/zh_cn/sqlite.html)、[IO文件](https://www.html5plus.org/doc/zh_cn/io.html)等本地存储方案。



### `6. 位置`

#### [6.1 获取位置信息 uni.getLocation(OBJECT)](https://uniapp.dcloud.net.cn/api/location/location.html)

获取当前的地理位置、速度。



#### [6.2 查看位置 uni.openLocation(OBJECT)](https://uniapp.dcloud.net.cn/api/location/open-location.html)

使用应用内置地图查看位置。



#### [6.3 位置更新 uni.onLocationChange(FUNCTION CALLBACK)](https://uniapp.dcloud.net.cn/api/location/location-change.html)

监听实时地理位置变化事件，需结合 `uni.startLocationUpdate` 或 `uni.startLocationUpdateBackground` 使用



#### [6.4 地图组件控制 uni.createMapContext(mapId,this)](https://uniapp.dcloud.net.cn/api/location/map.html)

创建并返回 map 上下文 `mapContext` 对象。在自定义组件下，第二个参数传入组件实例this，以操作组件内 `<map>` 组件。





### `7. 媒体`

#### [7.1 图片](https://uniapp.dcloud.net.cn/api/media/image.html)

##### `7.1.1 uni.chooseImage(OBJECT)`

* 从本地相册选择图片或使用相机拍照。

* App端如需要更丰富的相机拍照API（如直接调用前置摄像头），参考[plus.camera](https://www.html5plus.org/doc/zh_cn/camera.html)

**OBJECT 参数说明**

| 参数名     | 类型          | 必填 | 说明                                                         | 平台差异说明                              |
| :--------- | :------------ | :--- | :----------------------------------------------------------- | :---------------------------------------- |
| count      | Number        | 否   | 最多可以选择的图片张数，默认9                                | 见下方说明                                |
| sizeType   | Array<String> | 否   | original 原图，compressed 压缩图，默认二者都有               | App、微信小程序、支付宝小程序、百度小程序 |
| extension  | Array<String> | 否   | 根据文件拓展名过滤，每一项都不能是空字符串。默认不过滤。     | H5(HBuilder X2.9.9+)                      |
| sourceType | Array<String> | 否   | album 从相册选图，camera 使用相机，默认二者都有。如需直接开相机或直接选相册，请只使用一个选项 |                                           |
| crop       | Object        | 否   | 图像裁剪参数，设置后 sizeType 失效                           | App 3.1.19+                               |
| success    | Function      | 是   | 成功则返回图片的本地文件路径列表 tempFilePaths               |                                           |
| fail       | Function      | 否   | 接口调用失败的回调函数                                       | 小程序、App                               |
| complete   | Function      | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                           |

**crop 参数说明**

| 参数名  | 类型    | 必填 | 说明                                                         | 平台差异说明 |
| :------ | :------ | :--- | :----------------------------------------------------------- | :----------- |
| quality | Number  | 否   | 取值范围为1-100，数值越小，质量越低（仅对jpg格式有效）。默认值为80。 |              |
| width   | Number  | 是   | 裁剪的宽度，单位为px，用于计算裁剪宽高比。                   |              |
| height  | Number  | 是   | 裁剪的高度，单位为px，用于计算裁剪宽高比。                   |              |
| resize  | Boolean | 否   | 是否将width和height作为裁剪保存图片真实的像素值。默认值为true。注：设置为false时在裁剪编辑界面显示图片的像素值，设置为true时不显示 |              |

**Tips**

- count 值在 H5 平台的表现，基于浏览器本身的规范。目前测试的结果来看，只能限制单选/多选，并不能限制数量。并且，在实际的手机浏览器很少有能够支持多选的。
- sourceType 值在 H5 平台根据浏览器的不同而表现不同，一般不可限制仅使用相册，部分浏览器也无法限制是否使用相机。
- 可以通过用户授权API来判断用户是否给应用授予相册或摄像头的访问权限https://uniapp.dcloud.io/api/other/authorize
- App端如需选择非媒体文件，可在插件市场搜索[文件选择](https://ext.dcloud.net.cn/search?q=文件选择)，其中Android端可以使用Native.js，无需原生插件，而iOS端需要原生插件。
- 选择照片大多为了上传，uni ui封装了更完善的[uni-file-picker组件](https://ext.dcloud.net.cn/plugin?id=4079)，文件选择、上传到uniCloud的免费存储和cdn中，一站式集成。强烈推荐使用。

**注：文件的临时路径，在应用本次启动期间可以正常使用，如需持久保存，需在主动调用 [uni.saveFile](https://uniapp.dcloud.net.cn/api/file/file#savefile)，在应用下次启动时才能访问得到。**

**success 返回参数说明**

| 参数          | 类型                       | 说明                                       |
| :------------ | :------------------------- | :----------------------------------------- |
| tempFilePaths | Array<String>              | 图片的本地文件路径列表                     |
| tempFiles     | Array<Object>、Array<File> | 图片的本地文件列表，每一项是一个 File 对象 |

**File 对象结构如下**

| 参数 | 类型   | 说明                           |
| :--- | :----- | :----------------------------- |
| path | String | 本地文件路径                   |
| size | Number | 本地文件大小，单位：B          |
| name | String | 包含扩展名的文件名称，仅H5支持 |
| type | String | 文件类型，仅H5支持             |

```javascript
uni.chooseImage({
	count: 6, //默认9
	sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
	sourceType: ['album'], //从相册选择
	success: function (res) {
		console.log(JSON.stringify(res.tempFilePaths));
	}
});
```



##### `7.1.2 uni.previewImage(OBJECT)`

预览图片。

**OBJECT 参数说明**

| 参数名           | 类型          | 必填         | 说明                                                         | 平台差异说明 |
| :--------------- | :------------ | :----------- | :----------------------------------------------------------- | :----------- |
| current          | String/Number | 详见下方说明 | 详见下方说明                                                 |              |
| urls             | Array<String> | 是           | 需要预览的图片链接列表                                       |              |
| indicator        | String        | 否           | 图片指示器样式，可取值："default" - 底部圆点指示器； "number" - 顶部数字指示器； "none" - 不显示指示器。 | App          |
| loop             | Boolean       | 否           | 是否可循环预览，默认值为 false                               | App          |
| longPressActions | Object        | 否           | 长按图片显示操作菜单，如不填默认为**保存相册**               | App 1.9.5+   |
| success          | Function      | 否           | 接口调用成功的回调函数                                       |              |
| fail             | Function      | 否           | 接口调用失败的回调函数                                       |              |
| complete         | Function      | 否           | 接口调用结束的回调函数（调用成功、失败都会执行）             |              |

**current 参数说明**

current 为当前显示图片的链接/索引值，不填或填写的值无效则为 urls 的第一张。**App平台在 1.9.5至1.9.8之间，current为必填。不填会报错**

注意，当 urls 中有重复的图片链接时：

- 传链接，预览结果始终显示该链接在 urls 中第一次出现的位置。
- 传索引值，在微信/百度/字节跳动小程序平台，会过滤掉传入的 urls 中该索引值之前与其对应图片链接重复的值。其它平台会保留原始的 urls 不会做去重处理。

举例说明：

一组图片 `[A, B1, C, B2, D]`，其中 B1 与 B2 的图片链接是一样的。

- 传 B2 的链接，预览的结果是 B1，前一张是 A，下一张是 C。
- 传 B2 的索引值 3，预览的结果是 B2，前一张是 C，下一张是 D。此时在微信/百度/字节跳动小程序平台，最终传入的 urls 是 `[A, C, B2, D]`，过滤掉了与 B2 重复的 B1。

**longPressActions 参数说明**

| 参数      | 类型          | 必填 | 说明                                             |
| :-------- | :------------ | :--- | :----------------------------------------------- |
| itemList  | Array<String> | 是   | 按钮的文字数组                                   |
| itemColor | String        | 否   | 按钮的文字颜色，字符串格式，默认为"#000000"      |
| success   | Function      | 否   | 接口调用成功的回调函数，详见返回参数说明         |
| fail      | Function      | 否   | 接口调用失败的回调函数                           |
| complete  | Function      | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**success 返回参数说明**

| 参数     | 类型   | 说明                     |
| :------- | :----- | :----------------------- |
| index    | Number | 用户长按图片的索引值     |
| tapIndex | Number | 用户点击按钮列表的索引值 |

```javascript
// 从相册选择6张图
uni.chooseImage({
	count: 6,
	sizeType: ['original', 'compressed'],
	sourceType: ['album'],
	success: function(res) {
		// 预览图片
		uni.previewImage({
			urls: res.tempFilePaths,
			longPressActions: {
				itemList: ['发送给朋友', '保存图片', '收藏'],
				success: function(data) {
					console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
				},
				fail: function(err) {
					console.log(err.errMsg);
				}
			}
		});
	}
	});
```

- 在非H5端，previewImage是原生实现的，界面自定义灵活度较低。
- 插件市场有前端实现的previewImage，性能低于原生实现，但界面可随意定义；插件市场也有适于App端的previewImage原生插件，提供了更多功能。



##### `7.1.3 uni.closePreviewImage(OBJECT)`

关闭预览图片。

|      App      |      H5       | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序 | 飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :-----------: | :-----------: | :--------: | :----------: | :--------: | :------------: | :--------: | :------: | :--------: | :--------: |
| √ `(3.2.15+)` | √ `(3.2.15+)` |     x      |      x       |     x      |       x        |     x      |    x     |     x      |     x      |

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |



##### `7.1.4 uni.getImageInfo(OBJECT)`

获取图片信息。

小程序下获取网络图片信息需先配置download域名白名单才能生效。

**平台差异说明**

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  √   |     √      |      √       |     √      |             √              |    √     |     √      |     √      |

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| src      | String   | 是   | 图片的路径，可以是相对路径，临时文件路径，存储文件路径，网络图片路径 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

**success 返回参数说明**

| 参数名      | 类型   | 说明                         | 平台差异说明            |
| :---------- | :----- | :--------------------------- | :---------------------- |
| width       | Number | 图片宽度，单位px             |                         |
| height      | Number | 图片高度，单位px             |                         |
| path        | String | 返回图片的本地路径           |                         |
| orientation | String | 返回图片的方向，有效值见下表 | App、小程序、京东小程序 |
| type        | String | 返回图片的格式               | App、小程序、京东小程序 |

**orientation 参数说明**

| 枚举值         | 说明                |
| :------------- | :------------------ |
| up             | 默认                |
| down           | 180度旋转           |
| left           | 逆时针旋转90度      |
| right          | 顺时针旋转90度      |
| up-mirrored    | 同up，但水平翻转    |
| down-mirrored  | 同down，但水平翻转  |
| left-mirrored  | 同left，但垂直翻转  |
| right-mirrored | 同right，但垂直翻转 |

```javascript
uni.chooseImage({
	count: 1,
	sourceType: ['album'],
	success: function (res) {
		uni.getImageInfo({
			src: res.tempFilePaths[0],
			success: function (image) {
				console.log(image.width);
				console.log(image.height);
			}
		});
	}
});
```



##### `7.1.5 uni.saveImageToPhotosAlbum(OBJECT)`

保存图片到系统相册。

**平台差异说明**

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  x   |     √      |      √       |     √      |             √              |    √     |     √      |     √      |

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| filePath | String   | 是   | 图片文件路径，可以是临时文件路径也可以是永久文件路径，不支持网络图片路径 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

**success 返回参数说明**

| 参数名 | 类型   | 说明                                     |
| :----- | :----- | :--------------------------------------- |
| path   | String | 保存到相册的图片路径，仅 App 3.0.5+ 支持 |
| errMsg | String | 调用结果                                 |

**注意**

- 可以通过用户授权API来判断用户是否给应用授予相册的访问权限https://uniapp.dcloud.io/api/other/authorize
- H5没有API可触发保存到相册行为，下载图片时浏览器会询问图片存放地址。

```javascript
uni.chooseImage({
	count: 1,
	sourceType: ['camera'],
	success: function (res) {
		uni.saveImageToPhotosAlbum({
			filePath: res.tempFilePaths[0],
			success: function () {
				console.log('save success');
			}
		});
	}
});
```



##### `7.1.6 uni.compressImage(OBJECT)`

压缩图片接口，可选压缩质量

**平台差异说明**

| App  |  H5  | 微信小程序 | 支付宝小程序 |       百度小程序       | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------------------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  x   |     √      |      √       | √(基础库版本>=3.110.3) |             √              |    √     |     √      |     √      |

**OBJECT 参数说明**

| 属性            | 类型     | 默认值 | 必填 | 说明                                                         | 平台差异说明       |
| :-------------- | :------- | :----- | :--- | :----------------------------------------------------------- | :----------------- |
| src             | String   |        | 是   | 图片路径，图片的路径，可以是相对路径、临时文件路径、存储文件路径 |                    |
| quality         | Number   | 80     | 否   | 压缩质量，范围0～100，数值越小，质量越低，压缩率越高（仅对jpg有效） |                    |
| width           | String   | auto   | 否   | 缩放图片的宽度，支持像素值（如"100px"）、百分比（如"50%"）、自动计算（如"auto"，即根据width与源图宽的缩放比例计算，若未设置width则使用源图宽度） | App 3.0.0+         |
| height          | String   | auto   | 否   | 缩放图片的高度，支持像素值（如"100px"）、百分比（如"50%"）、自动计算（如"auto"，即根据height与源图高的缩放比例计算，若未设置height则使用源图高度） | App 3.0.0+         |
| compressedWidth | Number   | -      | 否   | 压缩后图片的宽度，单位为px，若不填写则默认以 compressHeight 为准等比缩放 | 微信小程序2.26.0 + |
| compressHeight  | Number   | -      | 否   | 压缩后图片的高度，单位为px，若不填写则默认以 compressedWidth 为准等比缩放 | 微信小程序2.26.0 + |
| rotate          | Number   | 0      | 否   | 旋转度数，范围0～360                                         | App 3.0.0+         |
| success         | Function |        | 否   | 接口调用成功的回调函数                                       |                    |
| fail            | Function |        | 否   | 接口调用失败的回调函数                                       |                    |
| complete        | Function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                    |

**success 返回参数说明**

| 属性         | 类型   | 说明                     |
| :----------- | :----- | :----------------------- |
| tempFilePath | String | 压缩后图片的临时文件路径 |

```javascript
uni.compressImage({
  src: '/static/logo.jpg',
  quality: 80,
  success: res => {
    console.log(res.tempFilePath)
  }
})
```



#### `7.2 文件`

##### `7.2.1 uni.chooseFile(OBJECT)`

从本地选择文件。

本API主要用于选择非媒体文件，如果选择的文件是媒体文件，另有3个专用API：

- [图片选择](https://uniapp.dcloud.io/api/media/image?id=chooseimage)
- [视频选择](https://uniapp.dcloud.io/api/media/video?id=choosevideo)
- [多媒体文件选择(含图片视频)](https://uniapp.dcloud.io/api/media/video?id=choosemedia)

**平台差异说明**

| App  |          H5           |           微信小程序            | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :-------------------: | :-----------------------------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  x   | √`(HBuilder X2.9.9+)` | x`(可使用wx.chooseMessageFile)` |      x       |     x      |             x              |    x     |     x      |     x      |

- App端如需选择非媒体文件，可在插件市场搜索[文件选择](https://ext.dcloud.net.cn/search?q=文件选择)，其中Android端可以使用Native.js，无需原生插件，而iOS端需要原生插件。
- App端如果想选择下载到`_doc`、`_downloads`、`_documents`等plus.io控制的目录下的文件，可通过[plus.io Api](https://www.html5plus.org/doc/zh_cn/io.html)，自己做选择框。
- 选择文件大多为了上传，uni ui封装了更完善的[uni-file-picker组件](https://ext.dcloud.net.cn/plugin?id=4079)，文件选择、上传到uniCloud的免费存储和cdn中，一站式集成。强烈推荐使用。

**OBJECT 参数说明**



| 参数名     | 类型          | 默认值             | 必填 | 说明                                                         | 平台差异说明 |
| :--------- | :------------ | :----------------- | :--- | :----------------------------------------------------------- | :----------- |
| count      | Number        | 100                | 否   | 最多可以选择的文件数量                                       | 见下方说明   |
| type       | String        | 'all'              | 否   | 所选的文件的类型                                             | 见下方说明   |
| extension  | Array<String> |                    | 否   | 根据文件拓展名过滤，每一项都不能是空字符串。默认不过滤。     | 见下方说明   |
| sourceType | Array<String> | ['album','camera'] | 否   | （仅在type为`image`或`video`时可用）`album` 从相册选图，`camera` 使用相机，默认二者都有。如需直接开相机或直接选相册，请只使用一个选项 |              |
| success    | Function      |                    | 是   | 成功则返回图片的本地文件路径列表 `tempFilePaths`             |              |
| fail       | Function      |                    | 否   | 接口调用失败的回调函数                                       |              |
| complete   | Function      |                    | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |              |

**Tips**

- count 值在 H5 平台的表现，基于浏览器本身的规范。目前测试的结果来看，只能限制单选/多选，并不能限制数量。并且，在实际的手机浏览器很少有能够支持多选的。
- sourceType 值在 H5 平台根据浏览器的不同而表现不同，一般不可限制仅使用相册，部分浏览器也无法限制是否使用相机。
- extension暂只支持文件后缀名，例如`['.zip','.exe','.js']`，不支持`application/msword`等类似值

**注：文件的临时路径，在应用本次启动期间可以正常使用，如需持久保存，需在主动调用 [uni.saveFile](https://uniapp.dcloud.net.cn/api/file/file#savefile)，在应用下次启动时才能访问得到。**

**OBJECT.type 的合法值**

| 值    | 说明             |
| :---- | :--------------- |
| all   | 从所有文件选择   |
| video | 只能选择视频文件 |
| image | 只能选择图片文件 |

**Tips**

- 如果type属性和extension同时存在，例如`{type:'image',extension:['.png','.jpg']}`，则会选择`image/png,image/jpg`文件
- 如果只配置extension属性，例如`{extension:['.doc','.xlsx','.docx']}`，则会选择`.doc,.xlsx,.docx`文件，详情见[`accept属性`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes/accept)
- 在微信环境中，如果`type="all"`，则`extension`属性失效

**success 返回参数说明**

| 参数          | 类型                       | 说明                                       |
| :------------ | :------------------------- | :----------------------------------------- |
| tempFilePaths | Array<String>              | 文件的本地文件路径列表                     |
| tempFiles     | Array<Object>、Array<File> | 文件的本地文件列表，每一项是一个 File 对象 |

**File 对象结构如下**

| 参数 | 类型   | 说明                           |
| :--- | :----- | :----------------------------- |
| path | String | 本地文件路径                   |
| size | Number | 本地文件大小，单位：B          |
| name | String | 包含扩展名的文件名称，仅H5支持 |
| type | String | 文件类型，仅H5支持             |

```javascript
uni.chooseFile({
  count: 6, //默认100
  extension:['.zip','.doc'],
	success: function (res) {
		console.log(JSON.stringify(res.tempFilePaths));
	}
});

// 选择图片文件
uni.chooseFile({
  count: 10,
  type: 'image',
  success (res) {
    // tempFilePath可以作为img标签的src属性显示图片
    const tempFilePaths = res.tempFiles
  }
})
```



#### [7.3 录音功能](https://uniapp.dcloud.net.cn/api/media/record-manager.html)



#### [7.4 背景音频播放管理](https://uniapp.dcloud.net.cn/api/media/background-audio-manager.html)



#### [7.5 音频组件控制](https://uniapp.dcloud.net.cn/api/media/audio-context.html)



#### [7.6 视频](https://uniapp.dcloud.net.cn/api/media/video.html)



#### [7.7 视频组件控制](https://uniapp.dcloud.net.cn/api/media/video-context.html)



#### [7.8 相机组件控制](https://uniapp.dcloud.net.cn/api/media/camera-context.html)



#### [7.9 直播组件控制](https://uniapp.dcloud.net.cn/api/media/live-player-context.html)



#### [7.10 富文本](https://uniapp.dcloud.net.cn/api/media/editor-context.html)



#### [7.11 音视频合成](https://uniapp.dcloud.net.cn/api/media/media-container.html)



### `8. 设备`

#### `8.1 系统`

##### [8.1.1 uni.getSystemInfo(OBJECT), uni.getSystemInfoSync(OBJECT)](https://uniapp.dcloud.net.cn/api/system/info.html)

* uni-app提供了异步(`uni.getSystemInfo`)和同步(`uni.getSystemInfoSync`)的2个API获取系统信息。
* 按照运行环境层级排序，从底层向上，uni-app有6个概念：
  - `device`：运行应用的设备，如iphone、huawei
  - `os`：设备的操作系统，如 ios、andriod、windows、mac、linux
  - `rom`：基于操作系统的定制，Android系统特有概念，如miui、鸿蒙
  - `host`：运行应用的宿主程序，即OS和应用之间的运行环境，如浏览器、微信等小程序宿主、集成uniMPSDK的App。uni-app直接开发的app没有host概念
  - `uni`：uni-app框架相关的信息，如uni-app框架的编译器版本、运行时版本
  - `app`：开发者的应用相关的信息，如应用名称、版本

**OBJECT 参数说明：**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| success  | Function | 是   | 接口调用成功的回调                               |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

[#](https://uniapp.dcloud.net.cn/api/system/info.html#success-返回参数说明)success 返回参数说明

| 参数分类    | 参数getSystemInfoSync | 说明                                                         | App平台值域                                                  | Web平台值域                            | 小程序平台值域                                               | 备注                                                         | uni框架最低版本要求 |
| :---------- | :-------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :------------------ |
| device      | deviceId              | 设备 id 。由 uni-app 框架生成并存储，清空 Storage 会导致改变 |                                                              |                                        |                                                              |                                                              |                     |
|             | deviceType            | 设备类型。如`phone`、`pad`、`pc`、`unknow`                   | [详见](https://uniapp.dcloud.net.cn/api/system/info.html#tips) | `phone`、`pad`、`pc`、`unknow`         | `phone`、`pad`、`pc`                                         |                                                              | uni-app 3.4.10+     |
|             | deviceBrand           | 设备品牌。如：`apple`、`huawei`                              |                                                              | 不支持                                 |                                                              |                                                              | uni-app 3.4.10+     |
|             | deviceModel           | 设备型号                                                     |                                                              | 部分设备无法获取                       |                                                              |                                                              | uni-app 3.4.10+     |
|             | deviceOrientation     | 设备方向                                                     | `竖屏 portrait`、`横屏 landscape`                            | `竖屏 portrait`、`横屏 landscape`      | `竖屏 portrait`、`横屏 landscape`。仅微信百度小程序支持      |                                                              | uni-app 3.4.13+     |
|             | devicePixelRatio      | 设备像素比                                                   |                                                              |                                        |                                                              |                                                              | uni-app 3.4.13+     |
| os          | osName                | 系统名称                                                     | ios、android                                                 | ios、android、windows、macos、linux    | ios、android、windows、macos                                 |                                                              | uni-app 3.4.10+     |
|             | osVersion             | 操作系统版本。如 ios 版本，andriod 版本                      |                                                              |                                        |                                                              |                                                              | uni-app 3.4.10+     |
|             | osLanguage            | 操作系统语言[详见](https://uniapp.dcloud.net.cn/api/system/info.html#tips) | Android仅支持主语言+地区：`zh-CN 中文简体`、iOS支持主语言+次语言+地区`zh-Hans-CN 中文简体` | 与浏览器语言一致                       | 不支持                                                       |                                                              | uni-app 3.4.10+     |
|             | osTheme               | 操作系统主题                                                 | light、dark。iOS平台只有将应用主题设置为跟随系统时才能获取到系统的主题 | 不支持                                 | 不支持                                                       |                                                              | uni-app 3.4.10+     |
|             | osAndroidAPILevel     | Android 系统API库的版本。详情参考[Android 官方文档](https://developer.android.google.cn/guide/topics/manifest/uses-sdk-element?hl=en#ApiLevels) | `仅 Android 支持`                                            | 不支持                                 | 不支持                                                       |                                                              | uni-app 3.4.10+     |
| rom         | romName               | rom 名称                                                     | Android 部分机型获取不到值，[详见](https://uniapp.dcloud.net.cn/api/system/info.html#romname)。iOS 不支持 | 不支持                                 | 不支持                                                       |                                                              | uni-app 3.4.13+     |
|             | romVersion            | rom 版本                                                     | Android 部分机型获取不到值，[详见](https://uniapp.dcloud.net.cn/api/system/info.html#romname)。iOS 不支持 | 不支持                                 | 不支持                                                       |                                                              | uni-app 3.4.13+     |
| browser     | browserName           | 浏览器名称或App的webview名称                                 | chrome(android)、wkwebview(ios)、x5webview(app打包x5引擎)    | chrome、edge、safari、firefox          | 不支持                                                       |                                                              | uni-app 3.4.10+     |
|             | browserVersion        | 浏览器版本、webview 版本                                     |                                                              |                                        | 不支持                                                       |                                                              | uni-app 3.4.10+     |
| host        | hostName              | 小程序宿主或uniMPSDK的集成宿主名称，如：`WeChat`、`FeiShu`   | 仅 UniMPSDK 支持                                             | 不支持                                 | [详见](https://uniapp.dcloud.net.cn/api/system/info.html#hostname) | 微信小程序真机运行才有真值                                   | uni-app 3.4.10+     |
|             | hostVersion           | 宿主版本。如：微信版本号                                     | 仅 UniMPSDK 支持                                             | 不支持                                 | 小程序宿主版本                                               |                                                              | uni-app 3.4.10+     |
|             | hostLanguage          | 宿主语言                                                     | 仅 UniMPSDK 支持                                             | 不支持                                 | 小程序宿主语言                                               |                                                              | uni-app 3.4.10+     |
|             | hostTheme             | 宿主主题                                                     | `light`、`dark`。仅 UniMPSDK 支持                            | 不支持                                 | `light`、`dark`。前提是微信小程序全局配置"darkmode":true时才能获取 |                                                              | uni-app 3.4.10+     |
|             | hostFontSizeSetting   | 用户字体大小设置。以“我-设置-通用-字体大小”中的设置为准，单位：px | 不支持                                                       | 不支持                                 | 微信小程序、支付宝小程序、百度小程序、QQ小程序、字节小程序(2.53.0+) |                                                              | uni-app 3.4.13+     |
|             | hostPackageName       | 小程序宿主包名                                               | 仅 UniMPSDK 支持                                             | 不支持                                 | 不支持                                                       |                                                              | uni-app 3.4.10+     |
|             | hostSDKVersion        | uni小程序SDK版本、小程序客户端基础库版本                     | 仅 UniMPSDK 支持                                             | 不支持                                 |                                                              |                                                              | uni-app 3.4.13+     |
| uni-app框架 | uniPlatform           | uni-app 运行平台，与条件编译平台相同。[详见](https://uniapp.dcloud.net.cn/api/system/info.html#uniplatform) | app                                                          | `web`或`h5`                            | 各家小程序，如`mp-weixin`                                    |                                                              | uni-app 3.4.10+     |
|             | uniCompileVersion     | uni 编译器版本号。[详见](https://uniapp.dcloud.net.cn/api/system/info.html#uniplatform) | `3.4.10`、`3.2.9` 等                                         | `3.4.10`、`3.2.9` 等                   | `3.4.10`、`3.2.9` 等                                         |                                                              | uni-app 3.4.10+     |
|             | uniRuntimeVersion     | uni 运行时版本。[详见](https://uniapp.dcloud.net.cn/api/system/info.html#uniplatform) | `3.4.10`、`3.2.9` 等                                         | `3.4.10`、`3.2.9` 等                   | `3.4.10`、`3.2.9` 等                                         |                                                              | uni-app 3.4.10+     |
| app         | appId                 | `manifest` 中应用appid，即DCloud appid。                     |                                                              |                                        |                                                              |                                                              | uni-app 3.4.10+     |
|             | appName               | `manifest` 中应用名称                                        |                                                              |                                        |                                                              | 和`字节跳动小程序`字段冲突，`字节跳动小程序`原字段与`hostName`一致 | uni-app 3.4.10+     |
|             | appVersion            | `manifest` 中应用版本名称。                                  |                                                              |                                        |                                                              |                                                              | uni-app 3.4.10+     |
|             | appVersionCode        | `manifest` 中应用版本名号。                                  |                                                              |                                        |                                                              |                                                              | uni-app 3.4.10+     |
|             | appWgtVersion         | 应用资源（wgt）的版本名称。                                  |                                                              |                                        |                                                              |                                                              | uni-app 3.4.15+     |
|             | appLanguage           | 应用设置的语言                                               | `en`、`zh-Hans`、`zh-Hant`、`fr`、`es`                       | `en`、`zh-Hans`、`zh-Hant`、`fr`、`es` | `en`、`zh-Hans`、`zh-Hant`、`fr`、`es`                       |                                                              | uni-app 3.4.13+     |
| 其他        | ua                    | userAgent标识                                                |                                                              |                                        | 不支持                                                       |                                                              | uni-app 3.4.10+     |
|             | screenWidth           | 屏幕宽度                                                     |                                                              |                                        |                                                              |                                                              |                     |
|             | screenHeight          | 屏幕高度                                                     |                                                              |                                        |                                                              |                                                              |                     |
|             | windowWidth           | 可使用窗口宽度                                               |                                                              |                                        |                                                              |                                                              |                     |
|             | windowHeight          | 可使用窗口高度                                               |                                                              |                                        |                                                              |                                                              |                     |
|             | windowTop             | 可使用窗口的顶部位置                                         |                                                              |                                        |                                                              |                                                              |                     |
|             | windowBottom          | 可使用窗口的底部位置                                         |                                                              |                                        |                                                              |                                                              |                     |
|             | statusBarHeight       | 手机状态栏的高度                                             |                                                              |                                        |                                                              |                                                              |                     |
|             | safeArea              | 在竖屏正方向下的安全区域。由于此属性理解和使用比较困难，更推荐使用 safeAreaInsets 属性。[详见](https://uniapp.dcloud.net.cn/api/system/info.html#safearea) |                                                              |                                        | 微信、百度（开发者工具暂不支持，真机有效）、字节跳动、飞书、支付宝（iOS真机）、快手、QQ小程序、华为快应用 |                                                              |                     |
|             | safeAreaInsets        | 在竖屏正方向下的安全区域插入位置。与小程序定义的 safeArea 用途相同，但是规范参考 iOS 平台的 [safeAreaInsets](https://developer.apple.com/documentation/uikit/uiview/2891103-safeareainsets) 更利于理解和使用。[详见](https://uniapp.dcloud.net.cn/api/system/info.html#safearea) |                                                              |                                        | 微信、百度（开发者工具暂不支持，真机有效）、字节跳动、飞书、支付宝小程序（iOS真机）、华为快应用 |                                                              | uni-app 2.5.3+      |

```javascript
uni.getSystemInfo({
	success: function (res) {
		console.log(res.appName)
	}
});
```



##### [8.1.2 uni.getDeviceInfo()](https://uniapp.dcloud.net.cn/api/system/getDeviceInfo.html)

获取设备基础信息

| App           | H5            | 微信小程序    | 支付宝小程序 | 字节跳动小程序 | 快手小程序 | QQ小程序 | 百度小程序 | 京东小程序 | 钉钉小程序 | 飞书小程序 |
| :------------ | :------------ | :------------ | :----------- | :------------- | :--------- | :------- | :--------- | :--------- | :--------- | :--------- |
| √ `(3.4.13+)` | √ `(3.4.13+)` | √ `(2.20.1+)` | x            | x              | x          | x        | x          | x          | x          | x          |

**返回参数说明**

| 参数名            | 类型       | 说明                                                         | 平台差异说明                                                 |
| :---------------- | :--------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| deviceBrand       | string     | 设备品牌。如：`apple`、`huawei`                              | `H5 不支持`                                                  |
| deviceId          | string     | 设备 id 。由 uni-app 框架生成并存储，清空 Storage 会导致改变 |                                                              |
| deviceModel       | string     | 设备型号                                                     |                                                              |
| deviceType        | string     | 设备类型`phone`、`pad`、`pc`                                 |                                                              |
| deviceOrientation | string     | 设备方向 `竖屏 portrait`、`横屏 landscape`                   | `App、H5`。微信小程序请使用 `(getSystemInfo Api)[/api/system/info.html]` 获取 |
| devicePixelRatio  | string     | 设备像素比                                                   | `App、H5`。微信小程序请使用 `(getSystemInfo Api)[/api/system/info.html]` 获取 |
| system            | string     | 操作系统及版本                                               |                                                              |
| platform          | 客户端平台 |                                                              |                                                              |

小程序特殊的返回参数

| 参数名         | 类型   | 说明                                                         | 平台差异说明   |
| :------------- | :----- | :----------------------------------------------------------- | :------------- |
| abi            | String | 应用二进制接口类型（仅 Android 支持）                        | `仅微信小程序` |
| benchmarkLevel | Number | 设备性能等级（仅 Android 支持）。取值为：-2 或 0（该设备无法运行小游戏），-1（性能未知），>=1（设备性能值，该值越高，设备性能越好，目前最高不到50） | `仅微信小程序` |

不推荐使用的返回参数，仅为向下兼容保留

| 参数名 | 类型   | 说明                                                         | 平台差异说明 |
| :----- | :----- | :----------------------------------------------------------- | :----------- |
| brand  | string | 设备品牌                                                     | `H5 不支持`  |
| model  | string | 设备型号。新机型刚推出一段时间会显示unknown，微信会尽快进行适配。 |              |

**Tips**

- `deviceId`：`android 平台` 根据优先使用imei、mac，如果没有获取到就使用随机生成的标识。`ios 平台` 是直接使用随机生成的标识



##### [8.1.3 uni.getWindowInfo()](https://uniapp.dcloud.net.cn/api/system/getWindowInfo.html)

获取窗口信息

| App           | H5            | 微信小程序    | 支付宝小程序 | 字节跳动小程序 | 快手小程序 | QQ小程序 | 百度小程序 | 京东小程序 | 钉钉小程序 | 飞书小程序 |
| :------------ | :------------ | :------------ | :----------- | :------------- | :--------- | :------- | :--------- | :--------- | :--------- | :--------- |
| √ `(3.4.13+)` | √ `(3.4.13+)` | √ `(2.20.1+)` | x            | x              | x          | x        | x          | x          | x          | x          |

**返回参数说明**



| 参数名          | 类型   | 说明                             | 平台差异说明 |
| :-------------- | :----- | :------------------------------- | :----------- |
| pixelRatio      | number | 设备像素比                       |              |
| screenWidth     | number | 屏幕宽度                         |              |
| screenHeight    | number | 屏幕高度                         |              |
| windowWidth     | number | 可使用窗口宽度                   |              |
| windowHeight    | number | 可使用窗口高度                   |              |
| windowTop       | number | 可使用窗口的顶部位置             |              |
| windowBottom    | number | 可使用窗口的底部位置             |              |
| statusBarHeight | number | 手机状态栏的高度                 |              |
| screenTop       | number | 窗口上边缘的 y 值                |              |
| safeArea        | object | 在竖屏正方向下的安全区域         |              |
| safeAreaInsets  | object | 在竖屏正方向下的安全区域插入位置 |              |



##### [8.1.4 uni.getAppBaseInfo()](https://uniapp.dcloud.net.cn/api/system/getAppBaseInfo.html)

获取微信 APP 基础信息

| App           | H5            | 微信小程序    | 支付宝小程序 | 字节跳动小程序 | 快手小程序 | QQ小程序 | 百度小程序 | 京东小程序 | 钉钉小程序 | 飞书小程序 |
| :------------ | :------------ | :------------ | :----------- | :------------- | :--------- | :------- | :--------- | :--------- | :--------- | :--------- |
| √ `(3.4.13+)` | √ `(3.4.13+)` | √ `(2.20.1+)` | x            | x              | x          | x        | x          | x          | x          | x          |

**返回参数说明**

| 参数名              | 类型   | 说明                                                         | 平台差异说明                        |
| :------------------ | :----- | :----------------------------------------------------------- | :---------------------------------- |
| appId               | string | `manifest.json` 中应用appid，即DCloud appid。                |                                     |
| appName             | string | `manifest.json` 中应用名称                                   |                                     |
| appVersion          | string | `manifest.json` 中应用版本名称。                             |                                     |
| appVersionCode      | string | `manifest.json` 中应用版本名号。                             |                                     |
| appLanguage         | string | 应用设置的语言`en`、`zh-Hans`、`zh-Hant`、`fr`、`es`         | `App`、`H5`                         |
| appWgtVersion       | string | 应用资源（wgt）的版本名称。                                  | App 3.5.5+                          |
| hostLanguage        | string | 小程序宿主语言                                               | `App 仅 UNIMPSDK 支持`、`H5 不支持` |
| hostVersion         | string | App、小程序宿主版本。如：微信版本号                          | `App 仅 UNIMPSDK 支持`、`H5 不支持` |
| hostName            | string | 小程序宿主名称                                               | `App 仅 UNIMPSDK 支持`、`H5 不支持` |
| hostPackageName     | string | 小程序宿主包名                                               | `仅 UNIMPSDK 支持`                  |
| hostSDKVersion      | string | uni小程序SDK版本、小程序客户端基础库版本                     | `App 仅 UNIMPSDK 支持`、`H5 不支持` |
| hostTheme           | string | 系统当前主题，取值为light或dark。微信小程序全局配置"darkmode":true时才能获取，否则为 undefined （不支持小游戏） | `App 仅 UNIMPSDK 支持`、`H5 不支持` |
| hostFontSizeSetting | string | 用户字体大小设置。以“我-设置-通用-字体大小”中的设置为准，单位：px | `仅 小程序 支持`                    |

小程序特殊的返回参数

| 参数名      | 类型    | 说明                                                         | 平台差异说明   |
| :---------- | :------ | :----------------------------------------------------------- | :------------- |
| SDKVersion  | string  | 客户端基础库版本                                             | `仅微信小程序` |
| enableDebug | boolean | 是否已打开调试。可通过右上角菜单或 wx.setEnableDebug 打开调试 | `仅微信小程序` |
| host        | Object  | 当前小程序运行的宿主环境                                     | `仅微信小程序` |
| theme       | string  | 系统当前主题，取值为light或dark，全局配置"darkmode":true时才能获取，否则为 undefined （不支持小游戏） | `仅微信小程序` |



##### [8.1.5 uni.getAppAuthorizeSetting()](https://uniapp.dcloud.net.cn/api/system/getappauthorizesetting.html)

获取 APP 授权设置

**平台差异说明**

|        App         |  H5  |    微信小程序    | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | 钉钉小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :----------------: | :--: | :--------------: | :----------: | :--------: | :------------------------: | :--------: | :------: | :--------: | :--------: |
| HBuilderX (3.5.2+) |  x   | 基础库 (2.20.1+) |      x       |     x      |             x              |     x      |    x     |     x      |     x      |

**返回参数说明**

| 属性                        | 类型                                                  | 说明                                                         | 平台差异说明              |
| :-------------------------- | :---------------------------------------------------- | :----------------------------------------------------------- | :------------------------ |
| albumAuthorized             | 'authorized'/'denied'/'not determined'                | 允许使用相册的开关                                           | App 端仅 iOS 支持         |
| bluetoothAuthorized         | 'authorized'/'denied'/'not determined'/'config error' | 允许使用蓝牙的开关                                           | App 端仅 iOS 支持         |
| cameraAuthorized            | 'authorized'/'denied'/'not determined'/'config error' | 允许使用摄像头的开关                                         |                           |
| locationAuthorized          | 'authorized'/'denied'/'not determined'/'config error' | 允许使用定位的开关                                           |                           |
| locationAccuracy            | String                                                | 定位准确度。`"reduced"` 表示模糊定位；`"full"` 表示精准定位；`"unsupported"` 表示不支持 | App 端仅 iOS 支持         |
| microphoneAuthorized        | 'authorized'/'denied'/'not determined'/'config error' | 允许使用麦克风的开关                                         |                           |
| notificationAuthorized      | 'authorized'/'denied'/'not determined'/'config error' | 允许通知的开关                                               |                           |
| notificationAlertAuthorized | 'authorized'/'denied'/'not determined'/'config error' | 允许通知带有提醒的开关                                       | App 端仅 iOS（10.0+）支持 |
| notificationBadgeAuthorized | 'authorized'/'denied'/'not determined'/'config error' | 允许通知带有标记的开关                                       | App 端仅 iOS（10.0+）支持 |
| notificationSoundAuthorized | 'authorized'/'denied'/'not determined'/'config error' | 允许通知带有声音的开关                                       | App 端仅 iOS（10.0+）支持 |
| phoneCalendarAuthorized     | 'authorized'/'denied'/'not determined'                | 允许读写日历的开关                                           | App 端不支持              |

不推荐使用的返回参数，仅为兼容保留

|locationReducedAccuracy|boolean|模糊定位。true 表示模糊定位，false 表示精确定位 |App 端仅 iOS 支持|

**Tips：**

- `'authorized'`：表示已经获得授权，无需再次请求授权；

- `'denied'`：表示请求授权被拒绝，无法再次请求授权；（此情况需要引导用户打开系统设置，在设置页中打开权限）

- `'not determined'`：表示尚未请求授权，会在App下一次调用系统相应权限时请求；（仅 iOS 会出现。此种情况下引导用户打开系统设置，不展示开关）

- ```
  'config error'
  ```

  ：只有在 App 端时返回

  - bluetoothAuthorized：
    - Android平台不会返回 `config error`
    - iOS平台：表示没有在 `manifest.json -> App模块配置` 中配置 `BlueTooth(低功耗蓝牙)` 模块
  - cameraAuthorized：
    - Android平台：表示没有授予 `android.permission.CAMERA` 权限
    - iOS平台不会返回 `config error`
  - locationAuthorized：
    - Android平台：表示没有授予 `android.permission.ACCESS_COARSE_LOCATION` 权限
    - iOS平台：表示没有在 `manifest.json -> App模块配置` 中配置 `Geolocation(定位)` 模块
  - microphoneAuthorized：
    - Android平台：表示没有授予 `android.permission.RECORD_AUDIO` 权限
    - iOS平台不会返回 `config error`
  - notificationAuthorized、notificationAlertAuthorized、notificationBadgeAuthorized、notificationSoundAuthorized：
    - Android平台不支持
    - iOS平台：表示没有在 `manifest.json -> App模块配置` 中配置 `Push(推送)` 模块

```javascript
const appAuthorizeSetting = uni.getAppAuthorizeSetting()

console.log(appAuthorizeSetting.albumAuthorized)
console.log(appAuthorizeSetting.bluetoothAuthorized)
console.log(appAuthorizeSetting.cameraAuthorized)
console.log(appAuthorizeSetting.locationAuthorized)
console.log(appAuthorizeSetting.locationReducedAccuracy)
console.log(appAuthorizeSetting.microphoneAuthorized)
console.log(appAuthorizeSetting.notificationAlertAuthorized)
console.log(appAuthorizeSetting.notificationAuthorized)
console.log(appAuthorizeSetting.notificationBadgeAuthorized)
console.log(appAuthorizeSetting.notificationSoundAuthorized)
console.log(appAuthorizeSetting.phoneCalendarAuthorized)
```



##### [8.1.6 uni.getSystemSetting()](https://uniapp.dcloud.net.cn/api/system/getsystemsetting.html)

获取设备设置

**平台差异说明**

|        App         |  H5  |    微信小程序    | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | 钉钉小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :----------------: | :--: | :--------------: | :----------: | :--------: | :------------------------: | :--------: | :------: | :--------: | :--------: |
| HBuilderX (3.5.2+) |  x   | 基础库 (2.20.1+) |      x       |     x      |             x              |     x      |    x     |     x      |     x      |

**返回参数说明**

| 属性              | 类型    | 说明                                                         |
| :---------------- | :------ | :----------------------------------------------------------- |
| bluetoothEnabled  | boolean | 蓝牙的系统开关。当值为 `false` 时，App端：有可能是配置不正确导致，此时会返回 `bluetoothError` 属性描述错误。 |
| bluetoothError    | String  | App端：Android平台没有权限或者iOS平台模块配置错误时返回字符串，否则不返回此属性。详情见下 |
| locationEnabled   | boolean | 地理位置的系统开关。当值为 `false` 时，App端：Android平台是准确的；iOS平台有可能是配置不正确导致，此时会返回 `locationError` 属性描述错误. |
| locationError     | String  | App端：Android平台不返回此属性；iOS平台模块配置错误时返回字符串，否则不返回此属性。详情见下 |
| wifiEnabled       | boolean | Wi-Fi 的系统开关                                             |
| deviceOrientation | string  | 设备方向。`竖屏：portrait`，`横屏：landscape`                |

```javascript
const systemSetting = uni.getSystemSetting()

console.log(systemSetting.bluetoothEnabled)
console.log(systemSetting.deviceOrientation)
console.log(systemSetting.locationEnabled)
console.log(systemSetting.wifiEnabled)
```



##### [8.1.7 uni.openAppAuthorizeSetting()](https://uniapp.dcloud.net.cn/api/system/openappauthorizesetting.html)

跳转系统授权管理页

- App端
  打开系统App的权限设置界面
- 微信小程序
  打开系统微信App的权限设置界面

**平台差异说明**

|        App         |  H5  |    微信小程序    | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | 钉钉小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :----------------: | :--: | :--------------: | :----------: | :--------: | :------------------------: | :--------: | :------: | :--------: | :--------: |
| HBuilderX (3.5.3+) |  x   | 基础库 (2.20.1+) |      x       |     x      |             x              |     x      |    x     |     x      |     x      |

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.openAppAuthorizeSetting({
  success (res) {
    console.log(res)
  }
})
```



#### [8.2 内存](https://uniapp.dcloud.net.cn/api/system/memory.html)

#### `8.3 网络状态`

##### [8.3.1 uni.getNetworkType(OBJECT)](https://uniapp.dcloud.net.cn/api/system/network.html#getnetworktype)

获取网络类型。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| success  | Function | 是   | 接口调用成功，返回网络类型 networkType           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**success 返回参数说明**

| 参数        | 说明     |
| :---------- | :------- |
| networkType | 网络类型 |

**networkType 有效值**

| 值       | 说明                       | 平台差异说明 |
| :------- | :------------------------- | :----------- |
| wifi     | wifi 网络                  |              |
| 2g       | 2g 网络                    |              |
| 3g       | 3g 网络                    |              |
| 4g       | 4g 网络                    |              |
| 5g       | 5g 网络                    |              |
| ethernet | 有线网络                   | App          |
| unknown  | Android 下不常见的网络类型 |              |
| none     | 无网络                     |              |

```javascript
uni.getNetworkType({
	success: function (res) {
		console.log(res.networkType);
	}
});
```



##### [8.3.2 uni.onNetworkStatusChange(CALLBACK)](https://uniapp.dcloud.net.cn/api/system/network.html#onnetworkstatuschange)

监听网络状态变化。可使用`uni.offNetworkStatusChange`取消监听。

**CALLBACK 返回参数**

| 参数        | 类型    | 说明               | 平台差异说明         |
| :---------- | :------ | :----------------- | :------------------- |
| isConnected | Boolean | 当前是否有网络连接 | 字节跳动小程序不支持 |
| networkType | String  | 网络类型           |                      |

```javascript
uni.onNetworkStatusChange(function (res) {
	console.log(res.isConnected);
	console.log(res.networkType);
});
```



##### [8.3.3 uni.offNetworkStatusChange(CALLBACK)](https://uniapp.dcloud.net.cn/api/system/network.html#offnetworkstatuschange)

取消监听网络状态变化。

**平台差异说明**

|       App        |        H5        |  微信小程序   | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--------------: | :--------------: | :-----------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
| HBuilderX 3.0.1+ | HBuilderX 3.0.1+ | 基础库 2.9.3+ |      x       |     x      |             x              |    x     |     √      |     x      |

**Tips**

- `CALLBACK`必须为调用`uni.onNetworkStatusChange`时传入的`CALLBACK`

```javascript
var CALLBACK = function(res) {
    // ...这里写你的业务逻辑
}
uni.offNetworkStatusChange(CALLBACK)
uni.onNetworkStatusChange(CALLBACK);
```



#### [8.4 系统主题](https://uniapp.dcloud.net.cn/api/system/theme.html)



#### [8.5 加速度计](https://uniapp.dcloud.net.cn/api/system/accelerometer.html)



#### [8.6 罗盘](https://uniapp.dcloud.net.cn/api/system/compass.html)



#### [8.7 陀螺仪](https://uniapp.dcloud.net.cn/api/system/gyroscope.html)



#### [8.8 拨打电话 uni.makePhoneCall(OBJECT)](https://uniapp.dcloud.net.cn/api/system/phone.html)

**OBJECT 参数说明**

| 参数名      | 类型     | 必填 | 说明                                             |
| :---------- | :------- | :--- | :----------------------------------------------- |
| phoneNumber | String   | 是   | 需要拨打的电话号码                               |
| success     | Function | 否   | 接口调用成功的回调                               |
| fail        | Function | 否   | 接口调用失败的回调函数                           |
| complete    | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.makePhoneCall({
	phoneNumber: '114' //仅为示例
});
```

- Android需要在 manifest.json 增加权限 `<uses-permission android:name="android.permission.CALL_PHONE"/>`
- Android不弹出询问框直接拨打电话：https://ask.dcloud.net.cn/question/4035
- 发送短信：http://www.html5plus.org/doc/zh_cn/messaging.html
- Android读取短信验证码：http://ask.dcloud.net.cn/article/676
- Android遍历读取短信：https://ask.dcloud.net.cn/article/12934 注意需要赋予相关权限。
- 钉钉小程序端拨打电话，详见https://open.dingtalk.com/document/orgapp-client/call-menu



#### [8.9 扫码 uni.scanCode(OBJECT)](https://uniapp.dcloud.net.cn/api/system/barcode.html)

调起客户端扫码界面，扫码成功后返回对应的结果。

**平台差异说明**

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  x   |     √      |      √       |     √      |             √              |    √     |     √      |     √      |

**OBJECT 参数说明**

| 参数名            | 类型     | 必填 | 说明                                                         |                     平台差异说明                     |
| :---------------- | :------- | :--- | :----------------------------------------------------------- | :--------------------------------------------------: |
| onlyFromCamera    | Boolean  | 否   | 是否只能从相机扫码，不允许从相册选择图片                     | 字节跳动小程序、百度小程序、支付宝小程序不支持此参数 |
| scanType          | Array    | 否   | 扫码类型，参考下方`scanType的合法值`                         |              字节跳动小程序不支持此参数              |
| autoDecodeCharset | Boolean  | 否   | 是否启用自动识别字符编码功能，默认为否                       |                         App                          |
| autoZoom          | Boolean  | 否   | 是否启用自动放大，默认启用                                   |             仅 App-Android (3.5.4+) 支持             |
| barCodeInput      | Boolean  | 否   | 是否支持手动输入条形码                                       |             仅飞书小程序（V3.14.0）支持              |
| hideAlbum         | Boolean  | 否   | 是否隐藏相册（不允许从相册选择图片），只能从相机扫码。默认值为 false。 |                  仅支付宝小程序支持                  |
| success           | Function | 否   | 接口调用成功的回调，返回内容详见返回参数说明。               |                                                      |
| fail              | Function | 否   | 接口调用失败的回调函数（识别失败、用户取消等情况下触发）     |                                                      |
| complete          | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                                      |

**scanType的合法值**

| 值         | 说明           |
| :--------- | :------------- |
| barCode    | 一维码         |
| qrCode     | 二维码         |
| datamatrix | Data Matrix 码 |
| pdf417     | PDF417 条码    |

**success 返回参数说明**

| 参数         | 说明                                                         | 平台差异说明                                                 |
| :----------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| result       | 所扫码的内容                                                 |                                                              |
| scanType     | 所扫码的类型                                                 | App、微信小程序、百度小程序、QQ小程序、京东小程序、支付宝小程序 |
| charSet      | 所扫码的字符集                                               | App、微信小程序、百度小程序(所扫码的字符集，仅支持 Android 系统)、QQ小程序、京东小程序 |
| path         | 当所扫的码为当前应用的合法二维码时，会返回此字段，内容为二维码携带的 path。 | 微信小程序、QQ小程序、京东小程序                             |
| rawData      | 原始数据，base64 编码                                        | 微信小程序、QQ小程序、京东小程序、支付宝小程序               |
| code         | 扫码所得数据                                                 | 支付宝小程序                                                 |
| qrCode       | 扫描二维码时返回二维码数据                                   | 支付宝小程序                                                 |
| barCode      | 扫描条形码时返回条形码数据                                   | 支付宝小程序                                                 |
| imageChannel | 来源                                                         | 支付宝小程序                                                 |

```javascript
// 允许从相机和相册扫码
uni.scanCode({
	success: function (res) {
		console.log('条码类型：' + res.scanType);
		console.log('条码内容：' + res.result);
	}
});

// 只允许通过相机扫码
uni.scanCode({
	onlyFromCamera: true,
	success: function (res) {
		console.log('条码类型：' + res.scanType);
		console.log('条码内容：' + res.result);
	}
});

// 调起条码扫描
uni.scanCode({
	scanType: ['barCode'],
	success: function (res) {
		console.log('条码类型：' + res.scanType);
		console.log('条码内容：' + res.result);
	}
});
```

- App-vue如果想自定义扫码，可参考[uni-app中如何使用5+的原生界面控件](http://ask.dcloud.net.cn/article/35036)和[plus.barcode API](https://www.html5plus.org/doc/zh_cn/barcode.html)
- App-nvue，支持barcode组件，可自定义扫码界面。[详见](https://uniapp.dcloud.io/component/barcode)。App端自定义扫码界面，建议使用nvue方式。
- App的扫码引擎，使用业内开源的通用扫码库，扫码效率比不过微信、支付宝等商业扫码库。如需更强的扫码效果，请使用支付宝提供的扫码插件：https://ext.dcloud.net.cn/plugin?id=2636
- 微信小程序自定义扫码界面，可使用camera组件。[详见](https://uniapp.dcloud.io/component/camera)
- 微信内嵌浏览器运行H5版时，可通过js sdk实现扫码，需要引入一个单独的js，[详见](https://ask.dcloud.net.cn/article/35380)
- 在扫码界面点击返回也会进入 `fail` 回调中
- 支付宝小程序不支持 `success` 回调中的`charSet`，`path`
- HX 3.4.4之后版本 android 新增 检测到 QR 码时自动放大功能，提升扫码识别率。



#### [8.10 剪贴板](https://uniapp.dcloud.net.cn/api/system/clipboard.html)

##### [8.10.1 uni.setClipboardData(OBJECT)](https://uniapp.dcloud.net.cn/api/system/clipboard.html#setclipboarddata)

设置系统剪贴板的内容。

**OBJECT 参数说明**

| 参数名    | 类型     | 必填 | 说明                                             | 平台差异说明                |
| :-------- | :------- | :--- | :----------------------------------------------- | :-------------------------- |
| data      | String   | 是   | 需要设置的内容                                   |                             |
| showToast | Boolean  | 否   | 配置是否弹出提示，默认弹出提示                   | App (3.2.13+)、H5 (3.2.13+) |
| success   | Function | 否   | 接口调用成功的回调                               |                             |
| fail      | Function | 否   | 接口调用失败的回调函数                           |                             |
| complete  | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |                             |

```javascript
uni.setClipboardData({
	data: 'hello',
	success: function () {
		console.log('success');
	}
});
```



[8.10.2 uni.getClipboardData(OBJECT)](https://uniapp.dcloud.net.cn/api/system/clipboard.html#getclipboarddata)

获取系统剪贴板内容。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| success  | Function | 否   | 接口调用成功的回调                               |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**success 返回参数说明**

| 参数 | 类型   | 说明         |
| :--- | :----- | :----------- |
| data | String | 剪贴板的内容 |

```javascript
uni.getClipboardData({
	success: function (res) {
		console.log(res.data);
	}
});
```

- 设置剪贴板内容后，小程序平台会自动弹出轻提示；（微信小程序在成功回调success里设置toast可覆盖自带的轻提示）。App平台默认与小程序保持一致策略。如不希望在App平台弹出提示，可使用Native.js自行操作剪贴板，插件市场有封装好的示例https://ext.dcloud.net.cn/plugin?id=712。也可以在设置剪切板后立即uni.hideToast()。



#### [8.11 屏幕亮度](https://uniapp.dcloud.net.cn/api/system/brightness.html)



[8.12 用户截屏事件](https://uniapp.dcloud.net.cn/api/system/capture-screen.html)

##### [8.12.1 uni.onUserCaptureScreen(CALLBACK)](https://uniapp.dcloud.net.cn/api/system/capture-screen.html#onusercapturescreen)

监听用户主动截屏事件，用户使用系统截屏按键截屏时触发此事件。

**CALLBACK返回参数：**

| 属性 | 类型   | 说明                                |
| ---- | ------ | ----------------------------------- |
| path | string | 截屏文件路径，仅App-Android平台支持 |

```javascript
uni.onUserCaptureScreen(function() {
    console.log('用户截屏了')
});
```

* Android的截屏监听原理是监听相册中截屏目录的文件新增，需赋予App本地文件读取权限。



##### [8.12.2 uni.offUserCaptureScreen(function callback)](https://uniapp.dcloud.net.cn/api/system/capture-screen.html#offusercapturescreen)

用户主动截屏事件。取消事件监听。

**参数**

| 属性     | 类型     | 说明                       |
| -------- | -------- | -------------------------- |
| 回调函数 | Function | 用户主动截屏事件的回调函数 |





#### [8.13 振动](https://uniapp.dcloud.net.cn/api/system/vibrate.html)



#### [8.14 手机联系人](https://uniapp.dcloud.net.cn/api/system/contact.html)



#### [8.15 蓝牙](https://uniapp.dcloud.net.cn/api/system/bluetooth.html)



#### [8.16 低功耗蓝牙](https://uniapp.dcloud.net.cn/api/system/ble.html)



#### [8.17 iBeacon](https://uniapp.dcloud.net.cn/api/system/ibeacon.html)



#### [8.18 wifi](https://uniapp.dcloud.net.cn/api/system/wifi.html)



#### [8.19 电量](https://uniapp.dcloud.net.cn/api/system/batteryInfo.html)



#### [8.20 NFC](https://uniapp.dcloud.net.cn/api/system/nfc.html)



#### [8.21 设备方向](https://uniapp.dcloud.net.cn/api/system/deviceMotion.html)



#### [8.22 生物认证](https://uniapp.dcloud.net.cn/api/system/authentication.html)

生物认证，包含手机的指纹识别、faceid两部分。即通过人体身体特征来进行身份认证识别。

如需要专业的活体检测、人脸识别、金融级实人认证，需另见文档[uni实人认证](https://uniapp.dcloud.net.cn/uniCloud/frv/intro)



### `9. 键盘`

#### [9.1 uni.hideKeyboard()](https://uniapp.dcloud.net.cn/api/key.html#hidekeyboard)

隐藏软键盘

隐藏已经显示的软键盘，如果软键盘没有显示则不做任何操作。



#### [9.2 uni.onKeyboardHeightChange(CALLBACK)](https://uniapp.dcloud.net.cn/api/key.html#onkeyboardheightchange)

监听键盘高度变化

**参数**

function listener

键盘高度变化事件的监听函数

**参数**

Object res

| 参数   | 类型   | 说明     |
| :----- | :----- | :------- |
| height | Number | 键盘高度 |

```javascript
uni.onKeyboardHeightChange(res => {
  console.log(res.height)
})
```



#### [9.3 uni.offKeyboardHeightChange(CALLBACK)](取消监听键盘高度变化事件)

**参数**

function listener

onKeyboardHeightChange 传入的监听函数。不传此参数则移除所有监听函数。

```javascript
const listener = function (res) { console.log(res) }

uni.onKeyboardHeightChange(listener)
uni.offKeyboardHeightChange(listener) // 需传入与监听时同一个的函数对象
```



#### [9.4 uni.getSelectedTextRange(OBJECT)](https://uniapp.dcloud.net.cn/api/key.html#getselectedtextrange)

在input、textarea等focus之后，获取输入框的光标位置。注意：只有在focus的时候调用此接口才有效。目前仅支持 vue 页面，nvue 可以直接使用 weex 的 [getSelectionRange](https://weex.apache.org/zh/docs/components/input.html#getSelectionRange)。

**OBJECT 参数说明：**

| 参数名   | 类型     | 默认值 | 必填 | 说明                                             |
| -------- | -------- | ------ | ---- | ------------------------------------------------ |
| success  | Function |        | 否   | 接口调用成功的回调函数                           |
| fail     | Function |        | 否   | 接口调用失败的回调函数                           |
| complete | Function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**success 返回参数说明：**

| 属性  | 类型   | 说明               |
| ----- | ------ | ------------------ |
| start | Number | 输入框光标起始位置 |
| end   | Number | 输入框光标结束位置 |

```javascript
uni.getSelectedTextRange({
  success: res => {
    console.log('getSelectedTextRange res', res.start, res.end)
  }
})
```



### `10. 界面`

#### `10.1 交互反馈`

##### [10.1.1 uni.showToast(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/prompt.html)

显示消息提示框

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                                         | 平台差异说明                    |
| :------- | :------- | :--- | :----------------------------------------------------------- | :------------------------------ |
| title    | String   | 是   | 提示的内容，长度与 icon 取值有关。                           |                                 |
| icon     | String   | 否   | 图标，有效值详见下方说明，默认：success。                    |                                 |
| image    | String   | 否   | 自定义图标的本地路径（app端暂不支持gif）                     | App、H5、微信小程序、百度小程序 |
| mask     | Boolean  | 否   | 是否显示透明蒙层，防止触摸穿透，默认：false                  | App、微信小程序                 |
| duration | Number   | 否   | 提示的延迟时间，单位毫秒，默认：1500                         |                                 |
| position | String   | 否   | 纯文本轻提示显示位置，填写有效值后只有 `title` 属性生效，且不支持通过 uni.hideToast 隐藏。有效值详见下方说明。 | App                             |
| success  | Function | 否   | 接口调用成功的回调函数                                       |                                 |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |                                 |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                 |

**icon 值说明**

| 值        | 说明                                                         | 平台差异说明                                                 |
| :-------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| success   | 显示成功图标，此时 title 文本在`小程序`平台最多显示 7 个汉字长度。 | 支付宝小程序无长度无限制                                     |
| error     | 显示错误图标，此时 title 文本在`小程序`平台最多显示 7 个汉字长度。 | 支付宝小程序、快手小程序、字节小程序、百度小程序、京东小程序、QQ小程序不支持 |
| fail      | 显示错误图标，此时 title 文本无长度显示。                    | 支付宝小程序、字节小程序                                     |
| exception | 显示异常图标。此时 title 文本无长度显示。                    | 支付宝小程序                                                 |
| loading   | 显示加载图标，此时 title 文本在`小程序`平台最多显示 7 个汉字长度。 | 支付宝小程序不支持                                           |
| none      | 不显示图标，此时 title 文本在`小程序`最多可显示两行，`App`仅支持单行显示。 |                                                              |

```javascript
uni.showToast({
	title: '标题',
	duration: 2000
});
```

**position 值说明（仅App生效）**

| 值     | 说明     |
| :----- | :------- |
| top    | 居上显示 |
| center | 居中显示 |
| bottom | 居底显示 |

- App端可通过[plus.nativeUI.toast API](https://www.html5plus.org/doc/zh_cn/nativeui.html#plus.nativeUI.toast)实现更多功能。



##### [10.1.2 uni.hideToast()](https://uniapp.dcloud.net.cn/api/ui/prompt.html#hidetoast)

隐藏消息提示框。

```javascript
uni.hideToast();
```



##### [10.1.3 uni.showLoading(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/prompt.html#showloading)

显示 loading 提示框, 需主动调用 [uni.hideLoading](https://uniapp.dcloud.net.cn/api/ui/prompt#hideloading) 才能关闭提示框。

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                             | 平台差异说明                    |
| :------- | :------- | :--- | :----------------------------------------------- | :------------------------------ |
| title    | String   | 是   | 提示的文字内容，显示在loading的下方              |                                 |
| mask     | Boolean  | 否   | 是否显示透明蒙层，防止触摸穿透，默认：false      | H5、App、微信小程序、百度小程序 |
| success  | Function | 否   | 接口调用成功的回调函数                           |                                 |
| fail     | Function | 否   | 接口调用失败的回调函数                           |                                 |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |                                 |

```javascript
uni.showLoading({
	title: '加载中'
});
```



##### [10.1.4 uni.hideLoading()](https://uniapp.dcloud.net.cn/api/ui/prompt.html#hideloading)

隐藏 loading 提示框。

```javascript
uni.showLoading({
	title: '加载中'
});

setTimeout(function () {
	uni.hideLoading();
}, 2000);
```



##### [10.1.5 uni.showModal(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/prompt.html#showmodal)

显示模态弹窗，可以只有一个确定按钮，也可以同时有确定和取消按钮。类似于一个API整合了 html 中：alert、confirm。

**OBJECT参数说明**

| 参数            | 类型     | 必填 | 说明                                                         | 平台差异说明                                                 |
| :-------------- | :------- | :--- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| title           | String   | 否   | 提示的标题                                                   |                                                              |
| content         | String   | 否   | 提示的内容                                                   |                                                              |
| showCancel      | Boolean  | 否   | 是否显示取消按钮，默认为 true                                |                                                              |
| cancelText      | String   | 否   | 取消按钮的文字，默认为"取消"                                 |                                                              |
| cancelColor     | HexColor | 否   | 取消按钮的文字颜色，默认为"#000000"                          | H5、微信小程序、百度小程序、字节小程序（2.62.0+）            |
| confirmText     | String   | 否   | 确定按钮的文字，默认为"确定"                                 |                                                              |
| confirmColor    | HexColor | 否   | 确定按钮的文字颜色，H5平台默认为"#007aff"，微信小程序平台默认为"#576B95"，百度小程序平台默认为"#3c76ff" | H5、微信小程序、百度小程序、字节小程序（2.62.0+）            |
| editable        | Boolean  | 否   | 是否显示输入框                                               | H5 (3.2.10+)、App (3.2.10+)、微信小程序 (2.17.1+)、字节小程序（2.62.0+） |
| placeholderText | String   | 否   | 显示输入框时的提示文本                                       | H5 (3.2.10+)、App (3.2.10+)、微信小程序 (2.17.1+)、字节小程序（2.62.0+） |
| success         | Function | 否   | 接口调用成功的回调函数                                       |                                                              |
| fail            | Function | 否   | 接口调用失败的回调函数                                       |                                                              |
| complete        | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                                              |

**success返回参数说明**

| 参数    | 类型    | 说明                                                         | 平台差异说明                                                 |
| :------ | :------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| confirm | Boolean | 为 true 时，表示用户点击了确定按钮                           |                                                              |
| cancel  | Boolean | 为 true 时，表示用户点击了取消（用于 Android 系统区分点击蒙层关闭还是点击取消按钮关闭） |                                                              |
| content | String  | `editable` 为 true 时，用户输入的文本                        | H5 (3.2.10+)、App (3.2.10+)、微信小程序 (2.17.1+)、字节小程序（2.62.0+） |

```javascript
uni.showModal({
	title: '提示',
	content: '这是一个模态弹窗',
	success: function (res) {
		if (res.confirm) {
			console.log('用户点击确定');
		} else if (res.cancel) {
			console.log('用户点击取消');
		}
	}
});
```

- 弹框同时使用确定取消时，需注意不同平台的确认取消按钮位置不同。在微信、H5中，确认按钮默认在右边。在App中，iOS的确认按钮默认在右边，而Android默认在左边。产生这种差异的原因是uni.showModal在App和小程序上调用的是原生提供的弹出框，原生平台的策略本身就不同。如果需要调整，可以通过自行控制按钮的文字，即“确定”按钮的文字其实可以设置为“取消”；
- showModal不满足需求时，可以自行开发组件弹框。插件市场有很多自定义弹框的组件，需注意在非H5平台，前端组件无法覆盖原生组件（如地图、video），遮罩也无法盖住tabbar和navigationbar。如需覆盖原生组件或遮罩tabbar等，App端推荐使用[subNvue](https://uniapp.dcloud.net.cn/api/window/subNVues)；
- 小程序平台，`cancelText`和`confirmText`有长度限制，最多允许 4 个字符；
- 钉钉小程序真机与模拟器表现有差异，真机title，content均为必填项
- 各家小程序平台对于 `confirm`、`cancel` 字段返回规则可能不尽相同，包含两种情况：`{ confirm: true, cancel: false }` 或 `{ confirm: true }`，但并不影响使用 if 去做判断



##### [10.1.6 uni.showActionSheet(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/prompt.html#showactionsheet)

从底部向上弹出操作菜单

**OBJECT参数说明**

| 参数      | 类型          | 必填 | 说明                                               | 平台差异说明                                                 |
| :-------- | :------------ | :--- | :------------------------------------------------- | :----------------------------------------------------------- |
| title     | String        | 否   | 菜单标题                                           | App、H5、支付宝小程序、钉钉小程序、微信小程序 3.4.5+（仅真机有效） |
| alertText | String        | 否   | 警示文案（同菜单标题）                             | 微信小程序（仅真机有效）                                     |
| itemList  | Array<String> | 是   | 按钮的文字数组                                     | 微信、百度、字节跳动小程序数组长度最大为6个                  |
| itemColor | HexColor      | 否   | 按钮的文字颜色，字符串格式，默认为"#000000"        | App-iOS、字节跳动小程序、飞书小程序不支持                    |
| popover   | Object        | 否   | 大屏设备弹出原生选择按钮框的指示区域，默认居中显示 | App-iPad（2.6.6+）、H5（2.9.2）                              |
| success   | Function      | 否   | 接口调用成功的回调函数，详见返回参数说明           |                                                              |
| fail      | Function      | 否   | 接口调用失败的回调函数                             |                                                              |
| complete  | Function      | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）   |                                                              |

**popover 值说明（仅App生效）**

| 值     | 类型   | 说明                                                         |
| :----- | :----- | :----------------------------------------------------------- |
| top    | Number | 指示区域坐标，使用原生 navigationBar 时一般需要加上 navigationBar 的高度 |
| left   | Number | 指示区域坐标                                                 |
| width  | Number | 指示区域宽度                                                 |
| height | Number | 指示区域高度                                                 |

**success返回参数说明**

| 参数     | 类型   | 说明                                    |
| :------- | :----- | :-------------------------------------- |
| tapIndex | Number | 用户点击的按钮，从上到下的顺序，从0开始 |

```javascript
uni.showActionSheet({
	itemList: ['A', 'B', 'C'],
	success: function (res) {
		console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
	},
	fail: function (res) {
		console.log(res.errMsg);
	}
});
```

- App平台，iPad设备支持设置弹出框的位置，详见 [plus.nativeUI的文档](https://www.html5plus.org/doc/zh_cn/nativeui.html#plus.nativeUI.ActionSheetStyles)
- App平台，实现原生的、复杂的底部图文菜单，例如分享菜单，可参考https://ext.dcloud.net.cn/plugin?id=69
- 在非H5端，本章的所有弹出控件都是原生控件，层级最高，可覆盖video、map、tabbar等原生控件。
- [uni-app插件市场](https://ext.dcloud.net.cn/)有很多封装好的前端组件，但注意前端组件层级不是最高，无法覆盖原生组件，除非使用cover-view或nvue。



#### `10.2 设置导航条`

##### [10.2.1 uni.setNavigationBarTitle(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/navigationbar.html#setnavigationbartitle)

动态设置当前页面的标题。

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| title    | String   | 是   | 页面标题                                         |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.setNavigationBarTitle({
	title: '新的标题'
});
```

- 如果需要在页面进入时设置标题，可以在`onReady`内执行，以避免被框架内的修改所覆盖。如果必须在`onShow`内执行需要延迟一小段时间



##### [10.2.2 uni.setNavigationBarColor(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/navigationbar.html#setnavigationbarcolor)

设置页面导航条颜色。**如果需要进入页面就设置颜色，请延迟执行，防止被框架内设置颜色逻辑覆盖**

**OBJECT参数说明**

| 参数            | 类型     | 必填 | 说明                                                         | 平台差异说明                                                 |
| :-------------- | :------- | :--- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| frontColor      | String   | 是   | 前景颜色值，包括按钮、标题、状态栏的颜色，仅支持 #ffffff 和 #000000 | App、H5、微信小程序、百度小程序、字节跳动小程序、QQ小程序、快手小程序、京东小程序 |
| backgroundColor | String   | 是   | 背景颜色值，有效值为十六进制颜色                             |                                                              |
| animation       | Object   | 否   | 动画效果，{duration,timingFunc}                              | 微信小程序、百度小程序、QQ小程序、快手小程序、京东小程序     |
| success         | Function | 否   | 接口调用成功的回调函数                                       |                                                              |
| fail            | Function | 否   | 接口调用失败的回调函数                                       |                                                              |
| complete        | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                                              |

- Android 上的 backgroundColor 参数有限制，黑色大于 rgb(30,30,30), 白色小于 rgb(235,235,235)
- 如果需要在页面进入时设置标题，可以在`onReady`内执行，以避免被框架内的修改所覆盖。如果必须在`onShow`内执行需要延迟一小段时间

**animation 结构**

| 属性       | 类型   | 默认值   | 必填 | 说明                  |
| :--------- | :----- | :------- | :--- | :-------------------- |
| duration   | number | 0        | 否   | 动画变化时间，单位 ms |
| timingFunc | String | 'linear' | 否   | 动画变化方式          |

**animation.timingFunc 有效值**

| 值        | 说明                         |
| :-------- | :--------------------------- |
| linear    | 动画从头到尾的速度是相同的。 |
| easeIn    | 动画以低速开始               |
| easeOut   | 动画以低速结束。             |
| easeInOut | 动画以低速开始和结束。       |

**success返回参数说明**

| 参数名 | 类型   | 说明     |
| :----- | :----- | :------- |
| errMsg | String | 调用结果 |

```javascript
uni.setNavigationBarColor({
    frontColor: '#ffffff',
    backgroundColor: '#ff0000',
    animation: {
        duration: 400,
        timingFunc: 'easeIn'
    }
})
```



##### [10.2.3 uni.showNavigationBarLoading(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/navigationbar.html#shownavigationbarloading)

在当前页面显示导航条加载动画。

* App平台调用此API时会在屏幕中间悬浮显示loading

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                             |
| -------- | -------- | ---- | ------------------------------------------------ |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.showNavigationBarLoading()
```



##### [10.2.4 uni.hideNavigationBarLoading(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/navigationbar.html#hidenavigationbarloading)

在当前页面隐藏导航条加载动画。

* App平台调用此API时会关闭屏幕中间悬浮显示的loading

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                             |
| -------- | -------- | ---- | ------------------------------------------------ |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.hideNavigationBarLoading()
```



##### [10.2.5 uni.hideHomeButton(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/navigationbar.html#hidehomebutton)

隐藏返回首页按钮。

**平台差异说明**

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  x   |  x   |     √      |      x       |     x      |          1.48.0+           | 1.10.0+  |     x      |     √      |

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                             |
| -------- | -------- | ---- | ------------------------------------------------ |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.hideHomeButton()
```

- 微信小程序自基础库版本2.8.3开始支持
- 当用户打开的小程序最底层页面是非首页时，默认展示“返回首页”按钮，开发者可在页面`onShow`中调用`hideHomeButton`进行隐藏。



#### `10.3 设置TabBar`

##### [10.3.1 uni.setTabBarItem(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#settabbaritem)

动态设置 tabBar 某一项的内容

**OBJECT参数说明：**

| 属性             | 类型    | 默认值 | 必填 | 说明                                                         | 平台差异                      |
| :--------------- | :------ | :----- | :--- | :----------------------------------------------------------- | :---------------------------- |
| index            | number  |        | 是   | tabBar 的哪一项，从左边算起                                  |                               |
| text             | String  |        | 否   | tab 上的按钮文字                                             |                               |
| iconPath         | String  |        | 否   | 图片路径，icon 大小限制为 40kb，建议尺寸为 81px * 81px，当 position 为 top 时，此参数无效。微信小程序 2.7.0+、支付宝小程序支持网络图片，其他平台暂不支持网络图片 |                               |
| selectedIconPath | String  |        | 否   | 选中时的图片路径，icon 大小限制为 40kb，建议尺寸为 81px * 81px ，当 position 为 top 时，此参数无效 |                               |
| pagePath         | String  |        | 否   | 页面绝对路径，必须在 [pages](https://uniapp.dcloud.net.cn/collocation/pages#pages) 中先定义，被替换掉的 pagePath 不会变成普通页面（仍然需要使用 uni.switchTab 跳转） | App（2.8.4+）、H5（2.8.4+）   |
| visible          | Boolean | true   | 否   | 该项是否显示                                                 | App（3.2.10+）、H5（3.2.10+） |
| iconfont         | Object  |        | 否   | 字体图标，优先级高于 iconPath                                | App（3.4.4+）                 |
| success          | Funtion |        | 否   | 接口调用成功的回调函数                                       |                               |
| fail             | Funtion |        | 否   | 接口调用失败的回调函数                                       |                               |
| complete         | Funtion |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                               |

**iconfont参数说明：**

| 属性          | 类型   | 说明                  |
| :------------ | :----- | :-------------------- |
| text          | String | 字库 Unicode 码       |
| selectedText  | String | 选中后字库 Unicode 码 |
| fontSize      | String | 字体图标字号(px)      |
| color         | String | 字体图标颜色          |
| selectedColor | String | 字体图标选中颜色      |

```javascript
uni.setTabBarItem({
  index: 0,
  text: 'text',
  iconPath: '/path/to/iconPath',
  selectedIconPath: '/path/to/selectedIconPath'
})
```

注意: 设置 `iconfont` 属性时，pages.json `iconfontSrc` 需要指定字体文件，参考下面的配置

```json
// pages.json
{
  "tabBar": {
    "iconfontSrc":"static/iconfont.ttf",
    "list": [
      {
        "pagePath": "pages/index/index",
        "text": "Tab1",
        "iconfont": {
          "text": "\ue102",
          "selectedText": "\ue103",
          "fontSize": "17px",
          "color": "#000000",
          "selectedColor": "#0000ff"
        }
      }
    ]
  }
}
```



##### [10.3.2 uni.setTabBarStyle(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#settabbarstyle)

动态设置 tabBar 的整体样式

**OBJECT参数说明：**

| 属性             | 类型    | 默认值 | 必填 | 说明                                                         |
| :--------------- | :------ | :----- | :--- | :----------------------------------------------------------- |
| color            | String  |        | 否   | tab 上的文字默认颜色，HexColor                               |
| selectedColor    | String  |        | 否   | tab 上的文字选中时的颜色，HexColor                           |
| backgroundColor  | String  |        | 否   | tab 的背景色，HexColor                                       |
| backgroundImage  | String  |        | 否   | 图片背景。支持设置本地图片或创建线性渐变如，优先级高于 backgroundColor，仅 App 2.7.1+ 支持 |
| backgroundRepeat | String  |        | 否   | 背景图平铺方式。repeat：背景图片在垂直方向和水平方向平铺；repeat-x：背景图片在水平方向平铺，垂直方向拉伸；repeat-y：背景图片在垂直方向平铺，水平方向拉伸；no-repeat：背景图片在垂直方向和水平方向都拉伸。 默认使用 no-repeat。仅 App 2.7.1+ 支持 |
| borderStyle      | String  |        | 否   | tabBar上边框的颜色， 仅支持 black/white                      |
| midButton        | Object  |        | 否   | 中间按钮 仅在 list 项为偶数时有效 [详情](https://uniapp.dcloud.net.cn/collocation/pages.html#tabbar)。HBuilderX 3.6.9+ |
| success          | Funtion |        | 否   | 接口调用成功的回调函数                                       |
| fail             | Funtion |        | 否   | 接口调用失败的回调函数                                       |
| complete         | Funtion |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

* **backgroundImage创建线性渐变说明**

```stylus
backgroundImage: linear-gradient(to top, #a80077, #66ff00);
```

* 目前暂不支持 radial-gradient（径向渐变）。
* 目前只支持两种颜色的渐变，渐变方向如下：
  - to right：从左向右渐变
  - to left：从右向左渐变
  - to bottom：从上到下渐变
  - to top：从下到上渐变
  - to bottom right：从左上角到右下角
  - to top left：从右下角到左上角

```javascript
uni.setTabBarStyle({
  color: '#FF0000',
  selectedColor: '#00FF00',
  backgroundColor: '#0000FF',
  borderStyle: 'white'
})
```



##### [10.3.3 uni.hideTabBar(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#hidetabbar)

隐藏 tabBar

**OBJECT参数说明：**

| 属性      | 类型    | 默认值 | 必填 | 说明                                                         |
| :-------- | :------ | :----- | :--- | :----------------------------------------------------------- |
| animation | boolean | false  | 否   | 是否需要动画效果，仅微信小程序、支付宝小程序、百度小程序、字节跳动小程序、飞书小程序、QQ小程序、快手小程序、京东小程序支持 |
| success   | Funtion |        | 否   | 接口调用成功的回调函数                                       |
| fail      | Funtion |        | 否   | 接口调用失败的回调函数                                       |
| complete  | Funtion |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |



##### [10.3.4 uni.showTabBar(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#showtabbar)

显示 tabBar

**OBJECT参数说明：**

| 属性      | 类型    | 默认值 | 必填 | 说明                                                         |
| :-------- | :------ | :----- | :--- | :----------------------------------------------------------- |
| animation | boolean | false  | 否   | 是否需要动画效果，仅微信小程序、支付宝小程序、百度小程序、字节跳动小程序、飞书小程序、QQ小程序、快手小程序、京东小程序支持 |
| success   | Funtion |        | 否   | 接口调用成功的回调函数                                       |
| fail      | Funtion |        | 否   | 接口调用失败的回调函数                                       |
| complete  | Funtion |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |



##### [10.3.5 uni.setTabBarBadge(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#settabbarbadge)

为 tabBar 某一项的右上角添加文本。

**OBJECT参数说明：**

| 参数     | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| index    | Number   | 是   | tabBar的哪一项，从左边算起                       |
| text     | String   | 是   | 显示的文本，不超过 3 个半角字符                  |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.setTabBarBadge({
  index: 0,
  text: '1'
})
```



##### [10.3.6 uni.removeTabBarBadge(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#removetabbarbadge)

移除 tabBar 某一项右上角的文本。

**OBJECT参数说明：**

| 参数     | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| index    | Number   | 是   | tabBar的哪一项，从左边算起                       |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |



[10.3.7 uni.showTabBarRedDot(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#showtabbarreddot)

显示 tabBar 某一项的右上角的红点。

**OBJECT参数说明：**

| 参数     | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| index    | Number   | 是   | tabBar的哪一项，从左边算起                       |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |



[10.3.8 uni.hideTabBarRedDot(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#hidetabbarreddot)

隐藏 tabBar 某一项的右上角的红点。

**OBJECT参数说明：**

| 参数     | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| index    | Number   | 是   | tabBar的哪一项，从左边算起                       |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |



[10.3.9 uni.onTabBarMidButtonTap(CALLBACK)](https://uniapp.dcloud.net.cn/api/ui/tabbar.html#ontabbarmidbuttontap)

监听中间按钮的点击事件

|          App          |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :-------------------: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
| √（HBuilderX 2.3.4+） |  √   |     x      |      x       |     x      |             x              |    x     |     x      |     x      |

- tabbar是原生的，层级高于前端元素
- [uni-app插件市场](https://ext.dcloud.net.cn/search?q=底部图标菜单)有封装的前端tabbar，但性能不如原生tabbar
- 如果想要一个中间带+号的tabbar，在HBuilderX中新建uni-app项目、选择 底部选项卡 模板
- 以上大部分操作 tabbar 的 API 需要在 tabbar 渲染后才能使用，避免在 tabbar 未初始化前使用



#### `10.4 页面背景`

##### [10.4.1 uni.setBackgroundColor(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/bgcolor.html#setbackgroundcolor)

动态设置窗口的背景色。

**平台差异说明**

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  x   |  x   |     √      |      x       |     √      |             x              |    √     |     √      |     √      |

**参数说明**

| 属性                  | 类型     | 默认值 | 必填 | 说明                                                |
| :-------------------- | :------- | :----- | :--- | :-------------------------------------------------- |
| backgroundColor       | String   |        | 否   | 窗口的背景色，必须为十六进制颜色值                  |
| backgroundColorTop    | String   |        | 否   | 顶部窗口的背景色，必须为十六进制颜色值，仅 iOS 支持 |
| backgroundColorBottom | String   |        | 否   | 底部窗口的背景色，必须为十六进制颜色值，仅 iOS 支持 |
| success               | Function |        | 否   | 接口调用成功的回调函数                              |
| fail                  | Function |        | 否   | 接口调用失败的回调函数                              |
| complete              | Function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）    |

```javascript
uni.setBackgroundColor({
    backgroundColor: '#ffffff',
    backgroundColorTop: '#222222',
    backgroundColorBottom: '#333333'
});
```



##### [10.4.2 uni.setBackgroundTextStyle(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/bgcolor.html#setbackgroundtextstyle)

动态设置下拉背景字体、loading 图的样式。

**平台差异说明**

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  x   |  x   |     √      |      x       |     √      |             x              |    √     |     √      |     √      |

**参数说明**

| 属性      | 类型     | 必填 | 说明                                              |
| :-------- | :------- | :--- | :------------------------------------------------ |
| textStyle | String   | 是   | 下拉背景字体、loading 图的样式，值为：dark、light |
| success   | Function | 否   | 接口调用成功的回调函数                            |
| fail      | Function | 否   | 接口调用失败的回调函数                            |
| complete  | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）  |

```javascript
uni.setBackgroundTextStyle({
  textStyle: 'dark' // 下拉背景字体、loading 图的样式为dark
})
```



#### `10.5 动画`

##### [10.5.1 uni.createAnimation(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/animation.html#createanimation)

用到再看。



10.6 页面滚动

##### [10.5.2 uni.pageScrollTo(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/scroll.html#pagescrollto)

将页面滚动到目标位置。

|      App      |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 华为快应用 | 360小程序 |
| :-----------: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :-------: |
| √(nvue不支持) |  √   |     √      |      √       |     √      |             √              |    √     |     √      |     √     |

**OBJECT参数说明**

| 参数名    | 类型     | 必填 | 说明                                                        |
| :-------- | :------- | :--- | :---------------------------------------------------------- |
| scrollTop | Number   | 否   | 滚动到页面的目标位置（单位px）                              |
| selector  | String   | 否   | 选择器，App、H5、微信小程序2.7.3+ 、支付宝小程序1.20.0+支持 |
| duration  | Number   | 否   | 滚动动画的时长，默认300ms，单位 ms                          |
| success   | function | 否   | 接口调用成功的回调函数                                      |
| fail      | function | 否   | 接口调用失败的回调函数                                      |
| complete  | function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）            |

**selector 语法** selector类似于 CSS 的选择器，但仅支持下列语法。

- ID选择器：#the-id
- class选择器（可以连续指定多个）：`.a-class.another-class`
- 子元素选择器：`.the-parent > .the-child`
- 后代选择器：`.the-ancestor .the-descendant`
- 跨自定义组件的后代选择器：`.the-ancestor >>> .the-descendant`
- 多选择器的并集：`#a-node, .some-other-nodes`

```javascript
uni.pageScrollTo({
	scrollTop: 0,
	duration: 300
});
```

​	

#### `10.6 窗口尺寸变化`

##### [10.6.1 uni.onWindowResize(CALLBACK)](https://uniapp.dcloud.net.cn/api/ui/window.html#onwindowresize)

监听窗口尺寸变化事件

**平台差异说明**

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序 | 飞书小程序 | QQ小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------: | :--------: | :------: |
|  √   |  √   |     √      |      x       |     x      |       x        |     √      |    √     |

**CALLBACK 参数说明**

| 属性 | 类型   | 说明                                                       |
| ---- | ------ | ---------------------------------------------------------- |
| size | Object | 变化后的窗口的大小，单位为 px ，{windowWidth,windowHeight} |

```javascript
const windowResizeCallback = (res) => {
  console.log('变化后的窗口宽度=' + res.size.windowWidth)
  console.log('变化后的窗口高度=' + res.size.windowHeight)
}
uni.onWindowResize(windowResizeCallback)
```

- 如App端设置软键盘弹出方式为adjustResize ，则在键盘弹出时，会触发此事件。
- 横竖屏切换时，会触发此事件。



##### [10.6.2 uni.offWindowResize(CALLBACK)](https://uniapp.dcloud.net.cn/api/ui/window.html#offwindowresize)

取消监听窗口尺寸变化事件

* `CALLBACK`为调用`uni.onWindowResize`时传入的`CALLBACK`

```javascript
uni.offWindowResize(windowResizeCallback)
```



#### [10.7 窗口样式相关的 API](https://uniapp.dcloud.net.cn/api/ui/adapt.html)



#### `10.8 字体`

动态加载网络字体，文件地址需为下载类型。微信小程序 `'2.10.0'`起支持全局生效，需在 `app.vue` 中调用。

1. 引入中文字体，体积过大时会发生错误，建议抽离出部分中文，减少体积，或者用图片替代
2. 微信小程序端只支持网络字体，字体链接必须是https。App支持网络或本地的字体（本地字体需使用[平台绝对路径](http://www.html5plus.org/doc/zh_cn/io.html#plus.io.convertLocalFileSystemURL)）。
3. 微信小程序端字体链接必须是同源下的，或开启了cors支持，微信小程序的域名是servicewechat.com
4. 工具里提示 Faild to load font可以忽略
5. nvue不支持。nvue使用 Weex 提供的 DOM.addRule 加载自定义字体，[详见](https://uniapp.dcloud.io/tutorial/nvue-api.html#dom)
6. 插件市场有加载字体的例子：https://ext.dcloud.net.cn/plugin?id=954

| 5+App  |   H5   |  微信小程序   | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 |
| :----: | :----: | :-----------: | :----------: | :--------: | :------------------------: | :------: |
| 1.9.0+ | 2.3.4+ | 基础库 2.1.0+ |   1.11.0+    |     x      |             x              |    x     |

**参数说明**

| 属性     | 类型     | 默认值 | 必填 | 说明                                                         |
| :------- | :------- | :----- | :--- | :----------------------------------------------------------- |
| global   | Boolean  | false  | 否   | 是否全局生效                                                 |
| family   | String   |        | 是   | 定义的字体名称                                               |
| source   | String   |        | 是   | 字体资源的地址。建议格式为 TTF 和 WOFF，WOFF2 在低版本的iOS上会不兼容。 |
| desc     | Object   |        | 否   | 可选的字体描述符                                             |
| success  | Function |        | 否   | 接口调用成功的回调函数                                       |
| fail     | Function |        | 否   | 接口调用失败的回调函数                                       |
| complete | Function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

**Object.desc 的结构**

| 属性    | 类型   | 默认值 | 必填 | 说明                                                         |
| :------ | :----- | :----- | :--- | :----------------------------------------------------------- |
| style   | String | normal | 否   | 字体样式，可选值为 normal / italic / oblique                 |
| weight  | String | normal | 否   | 字体粗细，可选值为 normal / bold / 100 / 200../ 900          |
| variant | String | normal | 否   | 设置小型大写字母的字体显示文本，可选值为 normal / small-caps / inherit |

```javascript
uni.loadFontFace({
  family: 'Bitstream Vera Serif Bold',
  source: 'url("https://sungd.github.io/Pacifico.ttf")',
  success() {
	  console.log('success')
  }
})
```



#### `10.9 下拉刷新`

##### [10.9.1 onPullDownRefresh](https://uniapp.dcloud.net.cn/api/ui/pulldown.html#onpulldownrefresh)

在 js 中定义 onPullDownRefresh 处理函数（和onLoad等生命周期函数同级），监听该页面用户下拉刷新事件。

- 需要在 `pages.json` 里，找到的当前页面的pages节点，并在 `style` 选项中开启 `enablePullDownRefresh`。
- 当处理完数据刷新后，`uni.stopPullDownRefresh` 可以停止当前页面的下拉刷新。



##### [10.9.2 uni.startPullDownRefresh(OBJECT)](https://uniapp.dcloud.net.cn/api/ui/pulldown.html#startpulldownrefresh)

开始下拉刷新，调用后触发下拉刷新动画，效果与用户手动下拉刷新一致。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| success  | Function | 否   | 接口调用成功的回调                               |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**success 返回参数说明**

| 参数   | 类型   | 说明         |
| :----- | :----- | :----------- |
| errMsg | String | 接口调用结果 |



##### [10.9.3 uni.stopPullDownRefresh()](https://uniapp.dcloud.net.cn/api/ui/pulldown.html#stoppulldownrefresh)

停止当前页面下拉刷新。

```json
// pages.json
{
    "pages": [
        {
        	"path": "pages/index/index",
        	"style": {
        		"navigationBarTitleText": "uni-app",
        		"enablePullDownRefresh": true
        	}
        }
    ],
    "globalStyle": {
    	"navigationBarTextStyle": "white",
    	"navigationBarBackgroundColor": "#0faeff",
    	"backgroundColor": "#fbf9fe"
    }
}
```

```javascript
// 仅做示例，实际开发中延时根据需求来使用。
export default {
	data() {
		return {
			text: 'uni-app'
		}
	},
	onLoad: function (options) {
		setTimeout(function () {
			console.log('start pulldown');
		}, 1000);
		uni.startPullDownRefresh();
	},
	onPullDownRefresh() {
		console.log('refresh');
		setTimeout(function () {
			uni.stopPullDownRefresh();
		}, 1000);
	}
}
```

- 支付宝小程序`startPullDownRefresh`在开发者工具里会提示`暂未开放，请勿使用`
- 支付宝小程序`startPullDownRefresh`请使用真机调试（非真机预览）
- 后续支付宝小程序开发工具更新可能会有所修改



FAQ

Q：如何暂时禁用掉下拉刷新，待需要的时候再重新开启？ A：`App` 平台下可以处理此类场景，详细参考：[uni-app 中实现动态禁用/开启下拉刷新](https://ask.dcloud.net.cn/article/35134)

Q：自定义title如何让下拉刷新在title之下 A：App和H5端使用circle方式的下拉刷新，设offset在title高度之下。hello uni-app的模板-导航栏中有示例。小程序端无法实现，除非放弃原生下拉刷新，自己模拟下拉刷新，插件市场有类似插件，但性能不如原生下拉刷新。

Q：如何自定义下拉刷新样式 A：小程序端的原生下拉刷新样式是固定的；App端原生的下拉刷新有2种样式可选择，下拉漏出雪花和下拉circle圈。如果使用nvue，可以使用[refresh组件](https://uniapp.dcloud.io/component/refresh)自定义下拉刷新，都是原生渲染。如果想使用scroll-view在前端实现自定义下拉刷新，需要注意列表不可太长和太复杂，否则会有性能问题。[插件市场](https://ext.dcloud.net.cn/)搜索下拉刷新有示例。



#### `10.10 节点信息`

##### [10.10.1 uni.createSelectorQuery()](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#createselectorquery)

返回一个 `SelectorQuery` 对象实例。可以在这个实例上使用 `select` 等方法选择节点，并使用 `boundingClientRect` 等方法选择需要查询的信息。

- 使用 `uni.createSelectorQuery()` 需要在生命周期 `mounted` 后进行调用。
- 默认需要使用到 `selectorQuery.in` 方法。

```javascript
const query = uni.createSelectorQuery().in(this);
query.select('#id').boundingClientRect(data => {
  console.log("得到布局位置信息" + JSON.stringify(data));
  console.log("节点离页面顶部的距离为" + data.top);
}).exec();
```



##### [10.10.2 selectorQuery.select(selector)](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#selectorquery-select)

在当前页面下选择第一个匹配选择器 `selector` 的节点，返回一个 `NodesRef` 对象实例，可以用于获取节点信息。

`selector` 类似于 CSS 的选择器，但仅支持下列语法。

- ID选择器：`#the-id`
- class选择器（可以连续指定多个）：`.a-class.another-class`
- 子元素选择器：`.the-parent > .the-child`
- 后代选择器：`.the-ancestor .the-descendant`
- 跨自定义组件的后代选择器：`.the-ancestor >>> .the-descendant`
- 多选择器的并集：`#a-node, .some-other-nodes`



##### [10.10.3 selectorQuery.selectAll(selector)](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#selectorquery-selectall)

在当前页面下选择匹配选择器 `selector` 的所有节点，返回一个 `NodesRef` 对象实例，可以用于获取节点信息。



##### [10.10.4 selectorQuery.selectViewport()](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#selectorquery-selectviewport)

选择显示区域，可用于获取显示区域的尺寸、滚动位置等信息，返回一个 `NodesRef` 对象实例。



##### [10.10.5 selectorQuery.exec(callback)](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#selectorquery-exec)

执行所有的请求。请求结果按请求次序构成数组，在callback的第一个参数中返回。



##### [10.10.6 nodesRef.fields(object,callback)](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#nodesref-fields)

获取节点的相关信息。第一个参数是节点相关信息配置（必选）；第二参数是方法的回调函数，参数是指定的相关节点信息。

**object 参数说明**

| 字段名        | 类型            | 默认值 | 必填 | 说明                                                         | 平台差异说明            |
| :------------ | :-------------- | :----- | :--- | :----------------------------------------------------------- | :---------------------- |
| id            | Boolean         | false  | 否   | 是否返回节点 `id`                                            |                         |
| dataset       | Boolean         | false  | 否   | 是否返回节点 `dataset`                                       | App、微信小程序、H5     |
| rect          | Boolean         | false  | 否   | 是否返回节点布局位置（`left` `right` `top` `bottom`）        |                         |
| size          | Boolean         | false  | 否   | 是否返回节点尺寸（`width` `height`）                         |                         |
| scrollOffset  | Boolean         | false  | 否   | 是否返回节点的 `scrollLeft` `scrollTop`，节点必须是 `scroll-view` 或者 `viewport` |                         |
| properties    | Array＜string＞ | []     | 否   | 指定属性名列表，返回节点对应属性名的当前属性值（只能获得组件文档中标注的常规属性值，id class style 和事件绑定的属性值不可获取） | 仅 App 和微信小程序支持 |
| computedStyle | Array＜string＞ | []     | 否   | 指定样式名列表，返回节点对应样式名的当前值                   | 仅 App 和微信小程序支持 |
| context       | Boolean         | false  | 否   | 是否返回节点对应的 Context 对象                              | 仅 App 和微信小程序支持 |



##### [10.10.7 nodesRef.boundingClientRect(callback)](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#nodesref-boundingclientrect)

添加节点的布局位置的查询请求。相对于显示区域，以像素为单位。其功能类似于 DOM 的 `getBoundingClientRect`。返回 `NodesRef` 对应的 `SelectorQuery`。

**callback 返回参数**

| 属性    | 类型   | 说明             |
| ------- | ------ | ---------------- |
| id      | String | 节点的 ID        |
| dataset | Object | 节点的 dataset   |
| left    | Number | 节点的左边界坐标 |
| right   | Number | 节点的右边界坐标 |
| top     | Number | 节点的上边界坐标 |
| bottom  | Number | 节点的下边界坐标 |
| width   | Number | 节点的宽度       |
| height  | Number | 节点的高度       |



##### [10.10.8 nodesRef.scrollOffset(callback)](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#nodesref-scrolloffset)

添加节点的滚动位置查询请求。以像素为单位。节点必须是 `scroll-view` 或者 `viewport`。返回 `NodesRef` 对应的 `SelectorQuery`。

**callback 返回参数**

| 属性       | 类型   | 说明               |
| ---------- | ------ | ------------------ |
| id         | String | 节点的 ID          |
| dataset    | Object | 节点的 dataset     |
| scrollLeft | Number | 节点的水平滚动位置 |
| scrollTop  | Number | 节点的竖直滚动位置 |



##### [10.10.9 nodesRef.context(callback)](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#nodesref-context)

添加节点的 Context 对象查询请求。支持 [`VideoContext`](https://uniapp.dcloud.net.cn/api/media/video-context)、[`CanvasContext`](https://uniapp.dcloud.net.cn/api/canvas/CanvasContext)、和 [`MapContext`](https://uniapp.dcloud.net.cn/api/location/map) 等的获取。

**callback 返回参数**

| 属性    | 类型   | 说明                    |
| ------- | ------ | ----------------------- |
| context | Object | 节点对应的 Context 对象 |



##### [10.10.10 nodesRef.node(callback)](https://uniapp.dcloud.net.cn/api/ui/nodes-info.html#nodesref-node)

获取 `Node` 节点实例。目前支持 `Canvas` 的获取。

**callback 返回参数**

| 属性 | 类型   | 说明                 |
| ---- | ------ | -------------------- |
| node | Object | 节点对应的 Node 实例 |

**注意**

- 目前仅能用于`canvas`
- `canvas`需设置`type="webgl"`才能正常使用



```javascript
uni.createSelectorQuery().selectViewport().scrollOffset(res => {
  console.log("竖直滚动位置" + res.scrollTop);
}).exec();

let view = uni.createSelectorQuery().in(this).select(".test");

view.fields({
  size: true,
  scrollOffset: true
}, data => {
  console.log("得到节点信息" + JSON.stringify(data));
  console.log("节点的宽为" + data.width);
}).exec();

view.boundingClientRect(data => {
  console.log("得到布局位置信息" + JSON.stringify(data));
  console.log("节点离页面顶部的距离为" + data.top);
}).exec();
```

- nvue 暂不支持 uni.createSelectorQuery，暂时使用下面的方案

```javascript
<template>
  <view class="wrapper">
    <view ref="box" class="box">
      <text class="info">Width: {{size.width}}</text>
      <text class="info">Height: {{size.height}}</text>
      <text class="info">Top: {{size.top}}</text>
      <text class="info">Bottom: {{size.bottom}}</text>
      <text class="info">Left: {{size.left}}</text>
      <text class="info">Right: {{size.right}}</text>
    </view>
  </view>
</template>

<script>
  // 注意平台差异
  // #ifdef APP-NVUE
  const dom = weex.requireModule('dom')
  // #endif

  export default {
    data () {
      return {
        size: {
          width: 0,
          height: 0,
          top: 0,
          bottom: 0,
          left: 0,
          right: 0
        }
      }
    },
    onReady() {
    	 setTimeout(()=> {
	        const result = dom.getComponentRect(this.$refs.box, option => {
		    console.log('getComponentRect:', option)
		    this.size = option.size
		})
		console.log('return value:', result)
		console.log('viewport:', dom.getComponentRect('viewport'))
	 }, 100);
     }
  }
</script>
```



#### [10.11 监听节点布局相关](https://uniapp.dcloud.net.cn/api/ui/intersection-observer.html)

可以解决一些性能问题, 用到再看。



#### [10.12 媒体查询](https://uniapp.dcloud.net.cn/api/ui/media-query-observer.html)



#### [10.13 菜单](https://uniapp.dcloud.net.cn/api/ui/menuButton.html)



#### `10.14 语言`

##### [10.14.1 uni.getLocale()](https://uniapp.dcloud.net.cn/api/ui/locale.html#getlocale) 

获取当前设置的语

如果当前应用设置过语言，会获取到之前设置的语言，未设置时会返回根据系统语言类型自动选择的语言。



##### [10.14.2 uni.setLocale(locale)](https://uniapp.dcloud.net.cn/api/ui/locale.html#setlocale) 

设置当前语言

仅可设置为框架内置语言与[自定义扩展的语言](https://uniapp.dcloud.net.cn/tutorial/i18n.html#uni-framework)，遵循 BCP47 规范。



##### [10.14.3 uni.onLocaleChange(callback)](https://uniapp.dcloud.net.cn/api/ui/locale.html#onlocalechange)

用于监听应用语言切换

**callback返回参数说明**

| 参数名 | 类型   | 说明     |
| :----- | :----- | :------- |
| locale | String | 当前语言 |

- 组件和接口显示会根据设置的语言环境自动切换，未支持的系统语言环境会显示为英文。
- App-Android、App-iOS 平台修改系统语言后会重启应用。
- App-Android 平台设置新的语言后会自动重启应用。
- 框架内置如下语言，如需自定义内容或增加其他语言参考：[自定义国际化内容](https://uniapp.dcloud.io/collocation/i18n?id=uni-framework)
  - 英语 en
  - 中文简体 zh-Hans
  - 繁体 zh-Hant
  - 法语 fr
  - 西班牙语 es
- 在 [manifest.json](https://uniapp.dcloud.net.cn/collocation/manifest) -> locale 可以配置应用的默认语言。
- 仅 3.1.5 - 3.2.4 版本会自动使用 vue-i18n 内配置的语言。
- 在小程序平台仅影响用户业务层（vue-i18n）的语言配置，不能影响小程序原生组件和接口的语言。



### `11. 文件`

#### [11.1 uni.saveFile(OBJECT)](https://uniapp.dcloud.net.cn/api/file/file.html#savefile)

保存文件到本地。

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  x   |     √      |      √       |     √      |             √              |    √     |     x      |     √      |

**注意：saveFile 会把临时文件移动，因此调用成功后传入的 tempFilePath 将不可用**

**OBJECT 参数说明：**

| 参数名       | 类型     | 必填 | 说明                                                        |
| :----------- | :------- | :--- | :---------------------------------------------------------- |
| tempFilePath | String   | 是   | 需要保存的文件的临时路径                                    |
| success      | Function | 否   | 返回文件的保存路径，res = {savedFilePath: '文件的保存路径'} |
| fail         | Function | 否   | 接口调用失败的回调函数                                      |
| complete     | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）            |

**success 返回参数说明：**

| 参数          | 说明           |
| :------------ | :------------- |
| savedFilePath | 文件的保存路径 |

```javascript
uni.chooseImage({
  success: function (res) {
    var tempFilePaths = res.tempFilePaths;
    uni.saveFile({
      tempFilePath: tempFilePaths[0],
      success: function (res) {
        var savedFilePath = res.savedFilePath;
      }
    });
  }
});
```



#### [11.2 uni.getSavedFileList(OBJECT)](https://uniapp.dcloud.net.cn/api/file/file.html#getsavedfilelist)

获取本地已保存的文件列表。

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  x   |     √      |      √       |     √      |             √              |    √     |     x      |     √      |

**OBJECT 参数说明：**

| 参数名   | 类型     | 必填 | 说明                                                    |
| :------- | :------- | :--- | :------------------------------------------------------ |
| success  | Function | 否   | 接口调用成功的回调函数，返回结果见 success 返回参数说明 |
| fail     | Function | 否   | 接口调用失败的回调函数                                  |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）        |

**success 返回参数说明：**

| 参数     | 类型          | 说明         |
| :------- | :------------ | :----------- |
| errMsg   | String        | 接口调用结果 |
| fileList | Array<Object> | 文件列表     |

**fileList 中的项目说明：**

| 键         | 类型   | 说明                                                         |
| :--------- | :----- | :----------------------------------------------------------- |
| filePath   | String | 文件的本地路径                                               |
| createTime | Number | 文件的保存时的时间戳，从 `1970/01/01 08:00:00` 到该时刻的秒数。 |
| size       | Number | 文件大小，以字节为单位。                                     |

```javascript
uni.getSavedFileList({
  success: function (res) {
    console.log(res.fileList);
  }
});
```



#### [11.3 uni.getSavedFileInfo(OBJECT)](https://uniapp.dcloud.net.cn/api/file/file.html#getsavedfileinfo)

获取本地文件的文件信息。此接口只能用于获取已保存到本地的文件。

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  x   |     √      |      √       |     √      |             x              |    √     |     x      |     √      |

**OBJECT 参数说明：**

| 参数名   | 类型     | 必填 | 说明                                                    |
| :------- | :------- | :--- | :------------------------------------------------------ |
| filePath | String   | 是   | 文件路径                                                |
| success  | Function | 否   | 接口调用成功的回调函数，返回结果见 success 返回参数说明 |
| fail     | Function | 否   | 接口调用失败的回调函数                                  |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）        |

**success 返回参数说明：**

| 参数       | 类型   | 说明                                                         |
| :--------- | :----- | :----------------------------------------------------------- |
| errMsg     | String | 接口调用结果                                                 |
| size       | Number | 文件大小，以字节为单位。                                     |
| createTime | Number | 文件保存时的时间戳，从 `1970/01/01 08:00:00` 到该时刻的秒数。 |

```javascript
uni.getSavedFileInfo({
  filePath: 'unifile://somefile', //仅做示例用，非真正的文件路径
  success: function (res) {
    console.log(res.size);
    console.log(res.createTime);
  }
});
```



#### [11.4 uni.removeSavedFile(OBJECT)](https://uniapp.dcloud.net.cn/api/file/file.html#removesavedfile)

删除本地存储的文件。

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  x   |     √      |      √       |     √      |             √              |    √     |     x      |     √      |

**OBJECT 参数说明：**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| filePath | String   | 是   | 需要删除的文件路径                               |
| success  | Function | 否   | 接口调用成功的回调函数                           |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

```javascript
uni.getSavedFileList({
  success: function (res) {
    if (res.fileList.length > 0) {
      uni.removeSavedFile({
        filePath: res.fileList[0].filePath,
        complete: function (res) {
          console.log(res);
        }
      });
    }
  }
});
```



#### [11.5 uni.getFileInfo(OBJECT)](https://uniapp.dcloud.net.cn/api/file/file.html#getfileinfo)

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  √   |     √      |      √       |     √      |             √              |    √     |     x      |     √      |

**OBJECT 参数说明：**

| 参数名          | 类型     | 默认值 | 必填 | 说明                                             | 平台差异说明                       |
| :-------------- | :------- | :----- | :--- | :----------------------------------------------- | :--------------------------------- |
| filePath        | String   |        | 是   | 本地文件路径                                     |                                    |
| digestAlgorithm | String   | md5    | 否   | 计算文件摘要的算法，可取值 md5、sha1。           | 微信小程序、京东小程序、App 2.9.0+ |
| success         | Function |        | 否   | 接口调用成功的回调函数                           |                                    |
| fail            | Function |        | 否   | 接口调用失败的回调函数                           |                                    |
| complete        | Function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |                                    |

**success 返回参数说明：**

| 参数   | 类型   | 说明                                            | 平台差异说明                       |
| :----- | :----- | :---------------------------------------------- | :--------------------------------- |
| errMsg | String | 接口调用结果                                    |                                    |
| size   | Number | 文件大小，以字节为单位。                        |                                    |
| digest | String | 按照传入的 digestAlgorithm 计算得出的的文件摘要 | 微信小程序、京东小程序、App 2.9.0+ |



#### [11.6 uni.openDocument(OBJECT)](https://uniapp.dcloud.net.cn/api/file/file.html#opendocument)

新开页面打开文档，支持格式：doc, xls, ppt, pdf, docx, xlsx, pptx。

| App  |  H5  | 微信小程序 | 支付宝小程序 | 百度小程序 | 字节跳动小程序、飞书小程序 | QQ小程序 | 快手小程序 | 京东小程序 |
| :--: | :--: | :--------: | :----------: | :--------: | :------------------------: | :------: | :--------: | :--------: |
|  √   |  x   |     √      |      √       |     √      |             √              |    √     |     x      |     √      |

**OBJECT 参数说明：**



| 参数名   | 类型    | 必填                             | 说明                                                         | 平台差异说明                         |
| :------- | :------ | :------------------------------- | :----------------------------------------------------------- | :----------------------------------- |
| filePath | String  | 是                               | 文件路径，可通过 downFile 获得                               |                                      |
| fileType | String  | 支付宝小程序必填，其他平台非必填 | 文件类型，指定文件类型打开文件，有效值 doc, xls, ppt, pdf, docx, xlsx, pptx，支付宝小程序仅支持pdf | 微信小程序、支付宝小程序、京东小程序 |
| showMenu | Boolean | 否                               | 右上角是否有可以转发分享的功能                               | 微信小程序                           |
| success  | String  | 否                               | 接口调用成功的回调函数                                       |                                      |
| fail     | String  | 否                               | 接口调用失败的回调函数                                       | 微信小程序、京东小程序               |
| complete | String  | 否                               | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                      |

```javascript
uni.downloadFile({
  url: 'https://example.com/somefile.pdf',
  success: function (res) {
    var filePath = res.tempFilePath;
    uni.openDocument({
      filePath: filePath,
      showMenu: true,
      success: function (res) {
        console.log('打开文档成功');
      }
    });
  }
});
```

| 平台        | 打开方式                                   |
| :---------- | :----------------------------------------- |
| 小程序      | 在小程序的入口应用内打开                   |
| App iOS     | 在当前应用内打开                           |
| App Android | 调用系统相关应用打开，无相关应用则不能打开 |
| H5          | 使用浏览器打开，当前浏览器不支持则不能打开 |

- App端，io操作还可以用更强大的plus.io API。https://www.html5plus.org/doc/zh_cn/io.html
- App端，打开各种格式的文件，如office、pdf等，还可以用更强大的三方插件，详见[插件市场](https://ext.dcloud.net.cn/search?q=pdf)
- 选择文件上传，uni-app有自带的api：[uni.chooseImage](https://uniapp.dcloud.io/api/media/image?id=chooseimage)和[uni.chooseVideo](https://uniapp.dcloud.io/api/media/video?id=choosevideo)。App端如需选择非媒体文件，可在插件市场搜索[文件选择](https://ext.dcloud.net.cn/search?q=文件选择)，其中Android端可以使用Native.js，无需原生插件，而iOS端需要原生插件。



### [12. 绘画](https://uniapp.dcloud.net.cn/api/canvas/createOffscreenCanvas.html)



### [13. 广告](https://uniapp.dcloud.net.cn/api/a-d/rewarded-video.html)



### 14. 第三方服务

#### [14.1 获取服务提供商](https://uniapp.dcloud.net.cn/api/plugins/provider.html)

`uni.getProvider(OBJECT)`

获取服务供应商。

在App平台，可用的服务商，是打包环境中配置的服务商，与手机端是否安装了该服务商的App没有关系。

云打包在manifest中配置相关模块和SDK信息，离线打包在原生工程中配置。某个服务商配置被打包进去，运行时就能得到相应的服务供应商。



#### [14.2 登录](https://uniapp.dcloud.net.cn/api/plugins/login.html)



#### [14.3 分享](https://uniapp.dcloud.net.cn/api/plugins/share.html)



#### [14.4 支付](https://uniapp.dcloud.net.cn/api/plugins/payment.html)



#### [14.5 消息推送](https://uniapp.dcloud.net.cn/api/plugins/payment.html) 



#### [14.6 语音](https://uniapp.dcloud.net.cn/api/plugins/voice.html)



#### [14.7 实人认证](https://uniapp.dcloud.net.cn/api/plugins/facialRecognitionVerify.html)



#### [14.8 一键生成iOS通用链接](https://uniapp.dcloud.net.cn/api/plugins/universal-links.html)







































