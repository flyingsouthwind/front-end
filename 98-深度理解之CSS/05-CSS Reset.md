## CSS Reset

HTML 标签在不同浏览器中不同的默认样式会带来兼容性问题，影响开发效率，目前，较为流行的解决方式是页面刚打开时就全部重置浏览器默认样式，这就是 css reset。

常见的 css reset 部分代码：

```
/* 是否重置盒模型有待斟酌 */
* {
    -webkit-box-sizing: border-box;
       -moz-box-sizing: border-box;
    				box-sizing: border-box;
}

*:before,
*:after {
    -webkit-box-sizing: border-box;
       -moz-box-sizing: border-box;
    				box-sizing: border-box;
}

body, div, dl, dt, dd, ul, ol, li, h1, h2, h3, h4, h5, h6, pre, code, form, fieldset, legend, input, button, textarea, p, blockquote, th, td {
    margin: 0;
    padding: 0;
}

body {
    background: #fff;
    color: #555;
    font-size: 14px;
    font-family: "Arial", "Microsoft YaHei", "黑体", "宋体", sans-serif;
}

td, th, caption {
    font-size: 14px;
}

h1, h2, h3, h4, h5, h6 {
    font-weight: normal;
    font-size: 100%;
}

address, caption, cite, code, dfn, em, strong, th, var {
    font-style: normal;
    font-weight: normal;
}

a {
    color: #555;
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
}

img {
    border: none;
    vertical-align: middle;
}

ol, ul, li {
    list-style: none;
}

input, textarea, select, button {
    font: 14px "Arial", "Microsoft YaHei", "黑体", "宋体", sans-serif;
}

table {
    border-collapse: collapse;
}

html {
    overflow-y: scroll;
}

.clearfix:before,
.clearfix:after {
    content: " ";
    display: inline-block;
    height: 0;
    clear: both;
    visibility: hidden;
}

.clearfix {
    *zoom: 1;
}

...
```

css reset 的优点：

* 使 HTML 标签在不同浏览器中的样式趋于一致化

css reset 的缺点：

* 浪费性能，不论标签是否使用，几乎统一重置所有标签，文件笨重
* 缺乏弹性，使用到的 HTML 标签样式往往需要重新设定
* 由于样式继承，开发调试时出现大量的 css reset 样式，影响调试

### CSS Normalize

相对于 CSS reset，CSS Normalize 是为 HTML5 准备的优质替代方案，其最大特点就是保留 HTML 标签预设样式，仅针对不同浏览器与各版本间不相容的标签进行些微调整。

CSS Normalize 的优点：

* 保留有用的浏览器默认设置，而不是将其删除
* 为广泛的 HTML 元素提供了一般化的样式，且不会因为样式继承导致调试时样式杂乱
* 模块化，项目被拆分为多个相关却又独立的部分，可根据自己需要选择，文件很小
* 修正浏览器 Bug 与不一致，例如，IE９中 SVG 的溢出
* 有详细的文档来解释代码

CSS Normalize 的 [Github 地址](https://github.com/necolas/normalize.css) ，v8.0.1 中文注释版本：

```
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. 更正所有浏览器中的行高
 * 2. 防止 iOS 横屏时字号放大
 */
html {
    line-height: 1.15; /* 1 */
    -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections/章节
   ========================================================================== */

/* 删除 body 默认 margin */
body {
    margin: 0;
}

/**
 * 在 IE 中一致地渲染`main`元素。
 */
main {
    display: block;
}

/* 更正 Chrome/Firefox/Safari 中 `section`/`article` 上下文中 `h1` 字体大小和边距 */
h1 {
    font-size: 2em;
    margin: 0.67em 0;
}

/* Grouping content/分组内容
   ========================================================================== */

/**
 * 1. 在 Firefox 中添加正确的盒尺寸
 * 2. 在 Edge 和 IE 中 overflow 时显示
 */
hr {
    box-sizing: content-box;    /* 1 */
    height: 0;                  /* 1 */
    overflow: visible;          /* 2 */
}

/**
 * 1. 更正所有浏览器中字体大小的继承和缩放
 * 2. 纠正所有浏览器中奇怪的`em`字体大小
 */
pre {
    font-family: monospace, monospace;  /* 1 */
    font-size: 1em;                     /* 2 */
}

/* Text-level semantics/文本级语义
   ========================================================================== */

/**
 * 删除 IE 10 中链接激活时的灰色背景
 */
a {
    background-color: transparent;
}

/**
 * 1. 移除Chrome 57-中的底部边框
 * 2. 在 Chrome，Edge，IE，Opera 和 Safari 中添加正确的文本修饰
 */
abbr[title] {
    border-bottom: none;                /* 1 */
    text-decoration: underline;         /* 2 */
    text-decoration: underline dotted;  /* 2 */
}

/* 在Chrome，Edge和Safari中添加正确的字体粗细 */
b,
strong {
    font-weight: bolder;
}

/**
 * 1. 更正所有浏览器中字体大小的继承和缩放
 * 2. 纠正所有浏览器中奇怪的`em`字体大小
 */
code,
kbd,
samp {
    font-family: monospace, monospace;  /* 1 */
    font-size: 1em;                     /* 2 */
}

/**
 * 在所有浏览器中添加正确的 font-size
 */
small {
    font-size: 80%;
}

/* 在所有浏览器中，阻止`sub`和`sup`元素影响行高 */
sub,
sup {
    font-size: 75%;
    line-height: 0;
    position: relative;
    vertical-align: baseline;
}

sub {
    bottom: -0.25em;
}

sup {
    top: -0.5em;
}

/* Embedded content/可替换内容
   ========================================================================== */

/* 删除 IE 10 中链接内图像的 border */
img {
    border-style: none;
}

/* Forms/表单
   ========================================================================== */

/**
 * 1. 更改所有浏览器中的字体样式
 * 2. 删除 Firefox 和 Safari 中的 margin
 */
button,
input,
optgroup,
select,
textarea {
    font-family: inherit;   /* 1 */
    font-size: 100%;        /* 1 */
    line-height: 1.15;      /* 1 */
    margin: 0;              /* 2 */
}

/* 在 IE 和 Edge 中显示 overflow */
button,
input { /* 1 */
    overflow: visible;
}

/* 删除 Edge，Firefox 和 IE 中的 text-transform 继承 */
button,
select { /* 1 */
    text-transform: none;
}

/* 纠正无法在 iOS 和 Safari 中设置可点击类型的样式 */
button,
[type="button"],
[type="reset"],
[type="submit"] {
    -webkit-appearance: button;
}

/* 在 Firefox 中删除 border 和 padding */
button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
    border-style: none;
    padding: 0;
}

/* 恢复上一个规则未设置的焦点样式 */
button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
    outline: 1px dotted ButtonText;
}

/* 纠正 Firefox 中的 padding */
fieldset {
    padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. 更正 Edg e和 IE 中的文本换行
 * 2. 更正 IE 中 fieldset 元素的 color 值为 inherit
 * 3. 删除填充，以便开发人员在所有浏览器中清除`fieldset`元素时不会被捕获。
 */
legend {
    box-sizing: border-box; /* 1 */
    color: inherit; /* 2 */
    display: table; /* 1 */
    max-width: 100%; /* 1 */
    padding: 0; /* 3 */
    white-space: normal; /* 1 */
}

/* 在 Chrome，Firefox 和 Opera 中添加正确的 vertical-align 方式 */
progress {
    vertical-align: baseline;
}

/* 删除 IE 10+ 中默认垂直滚动条 */
textarea {
    overflow: auto;
}

/**
 * 1. 在 IE 10 中使用正确的盒尺寸
 * 2. 移除 IE 10 中的 padding
 */
[type="checkbox"],
[type="radio"] {
    box-sizing: border-box; /* 1 */
    padding: 0; /* 2 */
}

/* 更正 Chrome 中增量和减量按钮的光标样式 */
[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
    height: auto;
}

/**
 * 1. 纠正 Chrome 和 Safari 中的奇怪外观
 * 2. 纠正 Safari 中的 outline 样式
 */
[type="search"] {
    -webkit-appearance: textfield; /* 1 */
    outline-offset: -2px; /* 2 */
}

/* 在 macOS 上删除 Chrome 和 Safari 中的内部 padding */

[type="search"]::-webkit-search-decoration {
    -webkit-appearance: none;
}

/**
 * 1. 纠正无法在 iOS 和 Safari 中设置可点击类型的样式
 * 2. 在 Safari 中将字体属性更改为“inherit”
 */
::-webkit-file-upload-button {
    -webkit-appearance: button; /* 1 */
    font: inherit; /* 2 */
}

/* Interactive/互动
   ========================================================================== */

/* 确保在 Edge, IE 10+, Firefox 中正确显示 */

details {
    display: block;
}

/* 确保所有浏览器中元素正确显示 */
summary {
    display: list-item;
}

/* Misc/杂项
   ========================================================================== */

/* 确保 IE 10+ 中元素正确显示 */
template {
    display: none;
}

/* 确保 IE 10+ 中元素正确显示 */
[hidden] {
    display: none;
}
```





