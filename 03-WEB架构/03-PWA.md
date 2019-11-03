## PWA

> GCM，Google Cloud Messaging，Google 云端通讯，它能够让第三方应用的开发者把通知消息或信息从服务器发送到所有使用这个应用的安卓系统或 Chrome 浏览器的应用或拓展上

PWA，Progressive web apps，渐进式 Web 应用，运用现代的 Web API 以及传统的渐进式增强策略来创建跨平台 Web 应用，使其具有与原生应用相同的用户体验。

PWA 是一套纯 Web App 的解决方案，相对于 Native App，Web App 的固有缺陷：

* 网络延迟，浏览器需要需要先行下载页面文件后才能渲染，Native App 缓存可以明显降低用户等待时间
* 入口问题，传统的 Web App 寄生于浏览器环境，Native App 可以直接从系统桌面安装

PWA 通过 Service Worker 操作 Cache Storage 解决网路延迟问题，通过 Web App Manifest 解决从系统桌面安装 Web App 的问题。

经过几年来的摸索，目前互联网行业的普遍共识：

* Web App：迭代快，获取用户成本低；跨平台强体验弱，开发成本低。适合拉新
* Native App：迭代慢，获取用户成本高；跨平台弱体验强，开发成本高。适合保活

PWA App 兼具了传统 Web App 与 Native App 的优点，通过其技术簇，在具有传统 Web App 优点的前提下，使性能和体验无限接近 Native App，从而实现从拉新到保活的完整闭环。

PWA 目前的问题是：

* 核心依赖技术的浏览器实现还不够
* 由于国内屏蔽谷歌，导致
  * Chrome 浏览器不可用，各手机厂商的自带浏览器差异化比较大，都自有黑科技，比如 X5 的同层播放
  * 依赖 GCM 推送的通知不可用，Web Push Protocol 还没有国内的推送服务实现

### 特点

PWA 的主要特点包括下面三点：

* 可靠 - 即使在不稳定的网络环境下，也能瞬间加载并展现
* 体验 - 快速响应，并且有平滑的动画响应用户的操作
* 粘性 - 像设备上的原生应用，具有沉浸式的用户体验，用户可以添加到桌面

### 技术簇

PWA 技术簇：

* App Shell
* Web App Manifest，浏览器检查到有 Manifest 文件时，会提示用户安装应用到桌面；最新的情况是，在 Android 系统中，PWA App 甚至可以被收纳到的应用抽屉中，一样出现在系统设置中
* Service Worker 与 Cache Storage，离线缓存 App Shell 和页面资源，即便在弱网络或离线状态下也可以 显示页面
* Push API 与 Notification API

#### App Shell

App Shell 是用户界面所需的最小的 HTML、CSS 和 JS，类似开发本机应用时需要向应用商店发布的一组代码。用户初次打开时可以快速的获得页面。之于应用中其它不变的内容，可以通过渐进的方式逐步离线缓存在用户本地

https://developers.google.cn/web/fundamentals/architecture/app-shell

#### Web App Manifest

Web App manifest 是 JSON 格式的文件，应使用 application/manifest+json MIME 类型，但是不强制这样做。

##### 部署

Web App manifest 通过 HTML head 区域的 link 元素部署：

```
<link rel="manifest" href="/manifest.json">
```

##### 成员

Web App manifest 文件范例

```
{
    "name": "HackerWeb",
    "short_name": "HackerWeb",
    "start_url": ".",
    "display": "standalone",
    "background_color": "#fff",
    "description": "A simply readable Hacker News app.",
    "icons": [
        {
            "src": "images/touch/homescreen48.png",
            "sizes": "48x48",
            "type": "image/png"
        },
        {
            "src": "images/touch/homescreen96.png",
            "sizes": "96x96",
            "type": "image/png"
        },
        {
            "src": "images/touch/homescreen192.png",
            "sizes": "192x192",
            "type": "image/png"
        }
    ],
    "related_applications": [
        {
            "platform": "web"
        },
        {
            "platform": "play",
            "url": "https://play.google.com/store/apps/details?id=cheeaun.hackerweb"
        }
    ]
}
```

其中，主要成员：

* background_color：应用的背景颜色；仅用于改善加载时体验，当应用本身的样式表可用时，不能被用作背景色

* description：应用的一般描述

* dir：指定名称、短名称和描述成员的主文本方向。与 lang 一起，帮助正确显示右到左文本。可选值：

  * ltr，由左到右
  * rtl，由右到左
  * auto，由浏览器自动判断

  ```
  "dir": "rtl",
  "lang": "ar",
  "short_name": "أنا من التطبيق!"
  ```

* display：应用的首选显示模式。可选值：

  * fullscreen，全屏显示，所有可用的显示区域都被使用，并且不显示状态栏
  * standalone，让应用看起来像一个独立的应用程序
  * minimal-ui，让应用看起来像一个独立的应用程序，但有浏览器地址栏
  * browser，默认值，该应用在传统的浏览器标签或新窗口中打开

* icons：指定各种环境中用作应用图标的图像对象数组。图像对象可能包含以下值：

  * sizes，包含空格分隔的图像尺寸的字符串
  * src，图像文件的路径，如果是一个相对 URL，则基本 URL 将是 manifest 的 URL
  * type，图像类型，此字段的目的是允许用户代理快速忽略不支持的图形类型

* lang，指定 name 和 short_name 成员中值的主要语言

* name，应用名

* orientation，指定应用的默认方向 … 后续内容参考 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/Manifest)

#### Service Worker 与 Cache Storage

参考《02-WEB性能》

#### Push API 与 Notification API

Push API 用于服务器向 Web 应用推送消息 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Push_API)

Notifications API 用于向用户配置和显示桌面通知 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/notification)



### 参考

* https://lavas.baidu.com/
* https://huangxuan.me/2017/02/09/nextgen-web-pwa/





