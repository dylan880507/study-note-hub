## 相关网站

### [Vue3官网](https://cn.vuejs.org/)

### [Vue3官网手册](https://cn.vuejs.org/guide/introduction.html)

### [Vue3 API](https://cn.vuejs.org/api/)

### [Vue3 在线编辑](https://cn.vuejs.org/examples/#hello-world)

[Vue2到Vue3迁移文档](https://v3-migration.vuejs.org/)

### [Vue Router](https://router.vuejs.org/zh/)

### [官方状态管理库 - Pinia](https://pinia.vuejs.org/)

### [官网推荐打包工具 - Vite](https://cn.vitejs.dev/)

### [Vue CLI](https://cli.vuejs.org/zh/)

## createApp

- 每个 Vue 应用都是通过 [`createApp`](https://cn.vuejs.org/api/application.html#createapp) 函数创建一个新的**应用实例**


```js
//定义
function createApp(rootComponent: Component, rootProps?: object): App


//创建新的应用实例
import { createApp } from 'vue';
const app = createApp({
  /* 根组件选项 */
});


//或者import根组件, 传入createApp
import { createApp } from 'vue';
import App from './App.vue';
const app = createApp(App);
```

## app.mount()

- 参数可以是一个实际的 DOM 元素或一个 CSS 选择器 (使用第一个匹配到的元素)。返回**根组件的实例**。
- 如果该组件有模板或定义了渲染函数，它将替换容器内所有现存的 DOM 节点。否则在运行时编译器可用的情况下，容器元素的 `innerHTML` 将被用作模板。
- 对于每个应用实例，`mount()` 仅能调用一次。

```js
//定义
interface App {
  mount(rootContainer: Element | string): ComponentPublicInstance
}


import { createApp } from 'vue';
const app = createApp(/* ... */);
//使用css选择器
app.mount('#app');

//也可以挂载到一个实际的 DOM 元素。
app.mount(document.body.firstChild);


//例如下述demo, createApp没有定义template和渲染函数, 所以app挂在后, 会使用#app内的innerHTML作为模板
<div id="app">
  <button @click="count++">{{ count }}</button>
</div>

import { createApp } from 'vue';
const app = createApp({
  data() {
    return {
      count: 0
    }
  }
});
app.mount('#app');
```

## app.unmount()

- 卸载一个已挂载的应用实例。卸载一个应用会触发该应用组件树内所有组件的卸载生命周期钩子。

```js
//定义
interface App {
  unmount(): void
}
```

## app.version

- 提供当前应用所使用的 Vue 版本号。这在[插件](https://cn.vuejs.org/guide/reusability/plugins.html)中很有用，因为可能需要根据不同的 Vue 版本执行不同的逻辑。

```js
//定义
interface App {
  version: string
}


export default {
  install(app) {
    const version = Number(app.version.split('.')[0]);
    if (version < 3) {
      console.warn('This plugin requires Vue 3');
      return false;
    }
  }
}
```

## app.config

- 每个应用实例都会暴露一个 `config` 对象，其中包含了对这个应用的配置设定。你可以在挂载应用前更改这些属性 (下面列举了每个属性的对应文档)。

```js
import { createApp } from 'vue';
const app = createApp(/* ... */);
console.log(app.config);
```

## app.config.errorHandler

- 用于为应用内抛出的未捕获错误指定一个全局处理函数。

```js
//定义
interface AppConfig {
  errorHandler?: (
    err: unknown, //错误对象
    instance: ComponentPublicInstance | null, //触发该错误的组件实例
    info: string //一个指出错误来源类型信息的字符串
  ) => void
}


app.config.errorHandler = (err, instance, info) => {
  // 处理错误，例如：报告给一个服务
};
```

## app.config.warnHandler

- 用于为 Vue 的运行时警告指定一个自定义处理函数。

```js
//定义
interface AppConfig {
  warnHandler?: (
    msg: string, //警告信息
    instance: ComponentPublicInstance | null, //来源组件实例
    trace: string //组件追踪字符串
  ) => void
}
 
  
app.config.warnHandler = (msg, instance, trace) => {
  // `trace` is the component hierarchy trace
};
```

## app.config.performance

- 设置此项为 `true` 可以在浏览器开发工具的“性能/时间线”页中启用对组件初始化、编译、渲染和修补的性能表现追踪。仅在开发模式和支持 [performance.mark](https://developer.mozilla.org/en-US/docs/Web/API/Performance/mark) API 的浏览器中工作。

## app.config.compilerOptions

- 配置运行时编译器的选项。设置在此对象上的值将会在浏览器内进行模板编译时使用，并会影响到所配置应用的所有组件。另外你也可以通过 [`compilerOptions` 选项](https://cn.vuejs.org/api/options-rendering.html#compileroptions)在每个组件的基础上覆盖这些选项。
- 脚手架的项目需要在脚手架中配置

### app.config.compilerOptions.isCustomElement

如果该标签需要当作原生自定义元素则应返回 `true`。对匹配到的标签，Vue 会将其渲染为原生元素而非将其视为一个 Vue 组件来解析。

```js
//将所有标签前缀为 `ion-` 的标签视为自定义元素
app.config.compilerOptions.isCustomElement = (tag) => {
  return tag.startsWith('ion-')
}
```

### app.config.compilerOptions.whitespace

- 用于调整模板中空格的处理行为

- condense | preserve, 默认condense

```js
app.config.compilerOptions.whitespace = 'preserve';
```

### app.config.compilerOptions.delimiters

- **类型** `[string, string]`
- **默认** `['{{', '}}']`

- 此项通常是为了避免与同样使用 mustache 语法的服务器端框架发生冲突。

```js
// 分隔符改为ES6模板字符串样式
app.config.compilerOptions.delimiters = ['${', '}'];
```

### app.config.compilerOptions.comments

- **类型** `boolean`
- **默认** `false`

- 默认情况下，Vue 会在生产环境移除所有注释，设置该项为 `true` 会强制 Vue 在生产环境也保留注释。

```js
app.config.compilerOptions.comments = true;
```

## app.config.globalProperties

- 一个用于注册能够被应用内所有组件实例访问到的全局属性的对象。
- 这是对 Vue 2 中 `Vue.prototype` 使用方式的一种替代，此写法在 Vue 3 已经不存在了。
- 如果全局属性与组件自己的属性冲突，组件自己的属性将具有更高的优先级。

```js
//定义
interface AppConfig {
  globalProperties: Record<string, any>
}
  
app.config.globalProperties.msg = 'hello';
export default {
  mounted() {
    const _self = this;
    console.log(_self.msg); // 'hello'
  }
}
```

## [app.config.optionMergeStrategies](https://cn.vuejs.org/api/application.html#app-config-optionmergestrategies)


## app.provide()

- 提供一个值，可以在应用中的所有后代组件中注入使用。
- 第一个参数是注入的 key，第二个参数则是提供的值。返回应用实例本身。

```js
//定义
interface App {
  provide<T>(key: InjectionKey<T> | symbol | string, value: T): this
}


import { createApp } from 'vue';
const app = createApp(/* ... */);
app.provide('message', 'hello');

//在应用的某个组件中
export default {
  inject: ['message'],
  created() {
    console.log(this.message) // 'hello'
  }
}
```

## app.component()
