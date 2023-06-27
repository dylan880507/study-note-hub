## I>相关文章

[chrome plugin 官网](https://developer.chrome.com/docs/extensions/mv3/intro/mv3-overview/)

[chrome manifest 官网说明](https://developer.chrome.com/docs/extensions/mv3/manifest/#overview)

[chrome API 文档](https://developer.chrome.com/docs/extensions/reference/)

[PlasmoHQ/plasmo](https://github.com/PlasmoHQ/plasmo)

[PlasmoHQ docs](https://docs.plasmo.com/)

[PlasmoHQ examples](https://github.com/PlasmoHQ/examples)

[vite-chromeV3插件](https://gitee.com/dyalnxu/vite-plugin-chrome-extension-main)

[vite+vue3+ts+chromeV3插件 封装的框架](https://gitee.com/dyalnxu/chrome-plugin-vte-vue)



[chrome V3插件入门到放弃，Plasmo不完全使用指南](https://juejin.cn/post/7138820996840030215)

[chrome扩展程序开发入门 V3](https://juejin.cn/post/7130444603991261214)





## II> 核心介绍

### 1. [manifest.json](https://developer.chrome.com/docs/extensions/mv3/overview/)

```json
{
  // Required
  "manifest_version": 3,
  "name": "My Extension",
  "version": "versionString",

  // Recommended
  "action": {...},
  "default_locale": "en",
  "description": "A plain text description",
  "icons": {...},

  // Optional
  "author": ...,
  "automation": ...,
  "background": {
    // Required
    "service_worker": "background.js",
    // Optional
    "type": ...
  },
  "chrome_settings_overrides": {...},
  "chrome_url_overrides": {...},
  "commands": {...},
  "content_capabilities": ...,
  "content_scripts": [{...}],
  "content_security_policy": {...},
  "converted_from_user_script": ...,
  "cross_origin_embedder_policy": {"value": "require-corp"},
  "cross_origin_opener_policy": {"value": "same-origin"},
  "current_locale": ...,
  "declarative_net_request": ...,
  "devtools_page": "devtools.html",
  "differential_fingerprint": ...,
  "event_rules": [{...}],
  "externally_connectable": {
    "matches": ["*://*.example.com/*"]
  },
  "file_browser_handlers": [...],
  "file_system_provider_capabilities": {
    "configurable": true,
    "multiple_mounts": true,
    "source": "network"
  },
  "homepage_url": "https://path/to/homepage",
  "host_permissions": [...],
  "import": [{"id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"}],
  "incognito": "spanning, split, or not_allowed",
  "input_components": ...,
  "key": "publicKey",
  "minimum_chrome_version": "versionString",
  "nacl_modules": [...],
  "natively_connectable": ...,
  "oauth2": ...,
  "offline_enabled": true,
  "omnibox": {
    "keyword": "aString"
  },
  "optional_host_permissions": ["..."],
  "optional_permissions": ["tabs"],
  "options_page": "options.html",
  "options_ui": {
    "page": "options.html"
  },
  "permissions": ["tabs"],
  "platforms": ...,
  "replacement_web_app": ...,
  "requirements": {...},
  "sandbox": [...],
  "short_name": "Short Name",
  "storage": {
    "managed_schema": "schema.json"
  },
  "system_indicator": ...,
  "tts_engine": {...},
  "update_url": "https://path/to/updateInfo.xml",
  "version_name": "aString",
  "web_accessible_resources": [...]
}
```

------

### 2. background.js

```json
// 『重点』下面将出现的background.js 配置service work
"background": {
    // Required
    "service_worker": "service-worker.js",
},
```

- 不使用时终止，需要时重新启动（类似于事件页面）。
- 无权访问 DOM。（service worker独立于页面）

------

### 3. content_script

```json
// manifest.json
{
 "name": "My extension",
 ...
 "content_scripts": [
   {
     // 满足matches匹配的域名
     "matches": ["https://*.nytimes.com/*"],
     // 注入css
     "css": ["my-styles.css"],
     // 注入js
     "js": ["content-script.js"],
     "run_at": "document_idle" | "document_start" | "document_end"
   }
 ],
  "permissions": [
    "activeTab"
  ],
}
```

读取或写入网页的扩展程序使用 **content_script**。内容脚本包含在已加载到浏览器的页面上下文中执行的 JavaScript。内容脚本读取和修改浏览器访问的网页的 DOM。

`content_script`可以通过使用storage/message API来与扩展其他部分进行通信。

------

### 4. popup

```json
// manifest.json 中引入popup.html
"action": {
     "default_title": "Click to view a popup",
   	 "default_popup": "popup.html"
 }
```

```html
// popup.html 引入相关js css等
<html>
  <head>
    <meta charset="UTF-8">
    <title>京东揽才</title>
    <link rel="stylesheet" href="./css/popup.css">
    <script src="popup.js"></script>
    <script src="js/axios.min.js"></script>
  </head>
  <body>
  </body>
</html>
```

## III> 相互间的通信方式

| **JS种类**      | **可访问的API**                                | **DOM访问情况**  | **JS访问情况**   | **直接跨域** |
| --------------- | ---------------------------------------------- | ---------------- | ---------------- | ------------ |
| injected script | 和普通JS无任何差别，不能访问任何扩展API        | 可以访问         | 可以访问         | 不可以       |
| content script  | 只能访问 extension、runtime等部分API           | 可以访问         | 不可以           | 不可以       |
| popup js        | 可访问绝大部分API，除了devtools系列            | 不可直接访问     | 不可以           | 可以         |
| background js   | 可访问绝大部分API，除了devtools系列            | 不可直接访问     | 不可以           | 可以         |
| devtools js     | 只能访问 devtools、extension、runtime等部分API | 可以访问devtools | 可以访问devtools | 不可以       |

### 1. content script与background

- 使用 `chrome.runtime.sendMessage` 发送信息
- 使用 `chrome.tabs.sendMessage`接收监听信息

```js
// content_script
// 监听接收信息
chrome.runtime.onMessage.addListener((request, sender, sendResponse) => {
	// 可写成switch形式 监听所有
	if (sender === "") {
		// do something
	}
	if (request.from === "cc") {
		// from 不是固定词，可使用其他自定义词汇
		// do something
	}
	// 发送回传
	sendResponse({number: request.number});

	// 修改dom
	document.querySelector("#s-usersetting-top").innerText = request.number;

	// 重发信息
	chrome.runtime.sendMessage({number: request.number + 1}, (response) => {
		console.log(
			`content script -> background infos have been received. number: ${response.number}`
		);
	});
});

// background
// 监听消息接收
chrome.runtime.onMessage.addListener((request, sender, sendResponse)=> {
	chrome.tabs.query({active: true, currentWindow: true}, (tabs)=> {
		chrome.tabs.sendMessage(tabs[0].id,{number: request.number + 1},(response) => {
				console.log(
					`background -> content script infos have been received. number: ${response.number}`
				);
		});
	});
  // 消息回传
	sendResponse({number: request.number});
});
```

------

### 2. popup与background

```js
// popup
document.querySelector("#button").addEventListener("click", () => {
	const val1 = document.querySelector("#input1").value || "0";
	const val2 = document.querySelector("#input2").value || "0";
	chrome.runtime.sendMessage({val1, val2}, (response) => {
		document.querySelector("#ans").innerHTML = response.res;
	});
});d

// background
const dealwithBigNumber = (val1, val2) => BigInt(val1) * BigInt(val2) + "";
chrome.runtime.onMessage.addListener((request, sender, sendResponse) => {
	const {val1, val2} = request;
	sendResponse({res: dealwithBigNumber(val1, val2)});
});
```

------

### 3. popup与content

```js
// content_script
// 接收popup数据并修改dom
chrome.runtime.onMessage.addListener((request, sender, sendResponse) => {
	$("body").css("background", request.color);
	sendResponse({name: 1});
});

chrome.tabs.query(
  {
    active: true
  },(tabs)=>{
    if (tabs.length > 0) {
      var current = tabs[0];
      chrome.tabs.sendMessage(current.id, { action: "getData"}, function (response) {
        isCanrecruit = response?response.sourceCanrecruit:null;
        showContent()
      })
    }
  });
```
