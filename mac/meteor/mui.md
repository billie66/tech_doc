### meteor 中使用 material-ui（简称 mui）

首先安装 mui，之前介绍 meteor 中使用 react-router 的时候，我们已经知道了如何在 meteor 项目中使用 npm 软件包，在项目根目录下面的 package.json 文件中添加：

```js
"material-ui": "0.13.2",
"react-tap-event-plugin": "0.2.1"
```

保存之后，在命令行中运行 meteor 命令，安装 mui 及其所依赖的 react-tap-event-plugin 插件。那这两个 npm 包安装位置在哪里呢？

```bash
cd ./packages/npm-container/.npm/package/node_modules/
```

为什么要安装 react-tap-event-plugin 插件呢？因为 mui 的一些组件需要借助它监听 touch 事件。不过，这种依赖是暂时的，等到 react v1.0 发布之后，就不再需要这个插件了。
```

安装好 mui 之后，需要把它导出，才能在项目中使用。进入 client/lib 目录，打开 app.browserify.js 文件，添加两行代码：

```js
mui = require('material-ui');
var injectTapEventPlugin = require('react-tap-event-plugin');
injectTapEventPlugin();
```

这样就可以使用 mui 提供的组件了。下面自定义一个组件，实际演示如何使用 mui

### 举例说明

在使用 mui 之前，我们需要知道到底 mui 提供了哪些可用的组件。这时就要查看源码了，打开 mui 在 github 中的项目地址，进入到 src 目录中，会看到一个 index.js 文件，这个文件就列出了 mui 所提供的所有组件。顺便说一下，这个方法是我自己摸索出来。知道 mui 提供的组件列表，很重要，因为在使用这些组件的时候，你要先导出才能使用，如果你不知道组件名，怎么使用呢？

现在就要动手操作了，比方说定义一个导航栏，在 client 目录下新建一个文件，名为 Button.jsx，代码如下：

```js
const { RaisedButton } = mui;

Button = React.createClass({

  render() {
    return (
      <RaisedButton />
    );
  }
});
```

mui 项目中包含了很多 svg 图标，除了下面三个图标，

```js
Icons: {
  NavigationMenu: require('./svg-icons/navigation/menu'),
  NavigationChevronLeft: require('./svg-icons/navigation/chevron-left'),
  NavigationChevronRight: require('./svg-icons/navigation/chevron-right'),
},
```

可以通过 `mui.Icons.*` 方式使用之外，其它的图标组件可以先在 app.browserify.js 文件中导出，比如导出一个闹铃图标，如何操作呢？

```js
ActionAlarm = require('material-ui/lib/svg-icons/action/alarm');
```

然后就可以在项目中使用这个图标了，

```html
<ActionAlarm />
```

那这个图标路径 `material-ui/lib/svg-icons/action/alarm` 是怎么知道的呢？到 mui 的安装目录看一下，会找到一个 lib 目录，jsx 文件编译之后的存放位置，mui 提供的所有组件都可以在 lib 目录下找到。

mui 的文档网站是开源的，位于 mui 项目的 docs 目录下，docs/README.md 文件介绍了如何在本地把网站运行起来。

### mui 文档网站的响应式如何实现的？

不能使用 media query，通过 js 直接判断窗口大小，不同窗口使用不同的样式

