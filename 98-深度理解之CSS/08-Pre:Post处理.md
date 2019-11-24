## Pre/Post处理

预处理，定义了一种新的语言，为 CSS 增加一些编程特性，将 CSS 作为目标生成文件，例如，Sass（SCSS）、LESS、Stylus ...

后处理，直接对 CSS 进行处理，并最终生成 CSS 的处理器，属于广义上的 CSS 预处理器。 最典型的例子是 CSS 压缩工具 clean-css、Autoprefixer ...

### PostCss

PostCSS 本身是一个功能单一的工具，只是提供了一种用 JS 处理 CSS 的方式。PostCSS 真正的强大之处在于其不断发展的插件体系。

PostCSS 不能简单的被归类为 CSS 预处理器或者后处理器，其本身能执行的任务非常多，通过强大的插件体系，它可以同时覆盖传统意义上的预处理和后处理功能，只不过，主流的使用方式是将其作为 Css 的 Babel 使用，即用更贴近未来 Css 标准的方式来写 Css。

PostCSS 的工作流程是：

* 把 CSS 代码解析成 JS 可操作的抽象语法树（AST）结构
* 把 AST 交由插件来进行处理，插件能进行的操作是多种多样的，比如：
  * 可以支持变量和混入（mixin）
  * 增加浏览器相关的声明前缀
  * 将使用将来 CSS 规范的样式规则转译成当前的 CSS 规范支持的格式，从这个角度出发，PostCSS 至于 Css，类似于 Babel 至于 JS
* 由 AST 生成最终供各种浏览器使用的 Css

#### 使用

PostCSS 一般不能单独使用，需要与构建工具（例如Webpack、Grunt、Gulp等）集成以完成任务，其基本使用流程为（以Webpack为例）：

1. 安装插件

   ```
   npm install --save-dev postcss-loader postcss-preset-env
   ```

2. 配置 postcss.config.js

   ```
   const postcssPresetEnv = require('postcss-preset-env');
   
   module.exports = {
       plugins: [
           postcssPresetEnv({
               stage: 3,
               features: {
                   'nesting-rules': true
               },
               autoprefixer: {
                   browsers: [
                       'IE >= 8',
                       'Android >= 4.0'
                   ]
               }
           })
       ]
   };
   ```

3. webpack.config.js 中配置 postcss-loader

   ```
   module.exports = {
       ...
       module: {
           rules: [
               ...
               {
                   test: /\.css$|\.pcss$/,
                   use: ExtractTextPlugin.extract({
                       use: ['css-loader?minimize', 'postcss-loader'],
                       fallback: "vue-style-loader"
                   })
               }
           ]
       },
       ...
   };
   ```

#### 参考

* [PostCss配置指南](https://github.com/ecmadao/Coding-Guide/blob/master/Notes/CSS/PostCSS%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8C%97.md)
* https://github.com/anjia/blog/issues/1
* https://www.ibm.com/developerworks/cn/web/1604-postcss-css/index.html
* https://www.w3cplus.com/blog/tags/516.html
* https://blog.csdn.net/yushuangyushuang/article/details/79209752


