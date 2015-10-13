### meteor 中使用 material-ui（简称 mui）

首先安装 mui，之前介绍 meteor 中使用 react-router 的时候，我们已经知道了如何在 meteor 项目中使用 npm 软件包，在项目根目录下面的 package.json 文件中添加：

```js
"material-ui": "0.10.4",
"react-tap-event-plugin": "0.1.7"
```

保存之后，在命令行中运行 meteor 命令，安装 mui 及其所依赖的 react-tap-event-plugin 插件。那这两个 npm 包安装位置在哪里呢？

```bash
cd ./packages/npm-container/.npm/package/node_modules/
```

为什么要安装 react-tap-event-plugin 插件呢？因为 mui 的一些组件需要借助它监听 touch 事件。不过，这种依赖是暂时的，等到 react v1.0 发布之后，就不再需要这个插件了。 那怎么使用它呢？在 meteor 启动的时候，添加这么一行代码：

```js
Meteor.startup(function () {
  injectTapEventPlugin();
});
```

安装好 mui 之后，需要把它导出，才能在项目中使用。进入 client/lib 目录，打开 app.browserify.js 文件，添加两行代码：

```js
mui = require('material-ui');
injectTapEventPlugin = require('react-tap-event-plugin');
```

这样就可以使用 mui 提供的组件了。下面自定义一个组件，实际演示如何使用 mui

### 举例说明

在使用 mui 之前，我们需要知道到底 mui 提供了哪些可用的组件。这时就要查看源码了，打开 mui 在 github 中的项目地址，进入到 src 目录中，会看到一个 index.js 文件，这个文件就列出了 mui 所提供的所有组件。顺便说一下，这个方法是我自己摸索出来。知道 mui 提供的组件列表，很重要，因为在使用这些组件的时候，你要先导出才能使用，如果你不知道组件名，怎么使用呢？

现在就要动手操作了，比方说定义一个导航栏，在 client 目录下新建一个文件，名为 NavBar.jsx，代码如下：

```js
const { IconButton } = mui;
const { NavigationMenu } = mui.Icons.NavigationMenu;
const ThemeManager = new mui.Styles.ThemeManager(); // required by material UI

NavBar = React.createClass({
  /* required by material UI */
  childContextTypes: {
    muiTheme: React.PropTypes.object
  },
  getChildContext: function() {
    return {
      muiTheme: ThemeManager.getCurrentTheme()
    };
  },
  /* end */

  render() {
    return (
      <div><IconButton><NavigationMenu /></IconButton></div>
    );
  }
});
```

自定义了一个 NavBar 组件，使用了 mui 的 IconButton 和 NavigationMenu 组件 ，代码中注释部分是 mui 要求必须包含的。注意一下，NavigationMenu 组件的导出方式。

查看 mui 的源码可知，NavigationMenu 就是一个 svg 图标组件。mui 项目中包含了很多 svg 图标，除了下面三个图标，

```js
Icons: {
  NavigationMenu: require('./svg-icons/navigation/menu'),
  NavigationChevronLeft: require('./svg-icons/navigation/chevron-left'),
  NavigationChevronRight: require('./svg-icons/navigation/chevron-right'),
},
```

可以通过 `mui.Icons.*` 方式使用之外，其它的图标组件需要先在 app.browserify.js 文件中导出，比如导出一个闹铃图标，如何操作呢？

```js
ActionAlarm = require('material-ui/lib/svg-icons/action/alarm');
```

然后就可以在项目中使用这个图标了，

```html
<ActionAlarm />
```

那这个图标路径 `material-ui/lib/svg-icons/action/alarm` 是怎么知道的呢？到 mui 的安装目录看一下，会找到一个 lib 目录，jsx 文件编译之后的存放位置，mui 提供的所有组件都可以在 lib 目录下找到。

mui 的文档网站是开源的，位于 mui 项目的 docs 目录下，docs/README.md 文件介绍了如何在本地把网站运行起来。

mui 组件遵照 ES6 的编码方式，目前在 meteor 所使用的 react 组件中还不能直接使用。

mui 文档网站的响应式如何实现的？

不能使用 media query，通过 js 直接判断窗口大小，不同窗口使用不同的样式

### 升级 MUI v0.12.3

Meteor 版本为 v1.2.0.1

MUI 更新很快，变动也比较大，一直想着升级到 v0.12.x，但没有成功，所以一些新特性，如 controlled tabs 就不能使用，很不方便。

MUI 不能升级，网上也找不到答案，心里总是惦记着这个事，今天又查看了一下 MUI 的 CHANGLOG，发现 MUI 已经更新到 v0.12.3 了，并且降低了 react 的版本（~0.13）

于是，我又试着升级了一下，成功了。packages.json 文件的内容如下：

```js
{
  "material-ui": "0.12.3",
  "react-tap-event-plugin": "0.1.7"
}
```

虽然 MUI 升级成功了，但是不起作用，因为使用的 MUI v0.10.4 的代码规则，没有报告错误，试了一下 controlled tabs 组件仍然不生效。

参考这个 [issue](https://github.com/mrphu3074/react-material-ui/issues/15)，就可以解决问题，

话说十几天前还没有答案呢，看来越来越多的开发者加入了 MUI，Meteor，React 阵营。

揭晓答案！删除 NPM 模块 react-tap-event-plugin， 因为 MUI v0.12.3 版本会自动安装 react-tap-event-plugin 插件，不需要重复安装。
现在的 packages.json 文件的内容如下：

```js
{
  "material-ui": "0.12.3"
}
```

操作完成之后，浏览器 console 中就出现报错信息了，因为 MUI v0.12.x 之后的主题管理方式改变了，所以修改代码：

```js
const ThemeManager = Styles.ThemeManager;
const DefaultRawTheme = Styles.LightRawTheme;

childContextTypes: {
  muiTheme: React.PropTypes.object
},

getChildContext() {
  return {
    muiTheme: ThemeManager.getMuiTheme(DefaultRawTheme),
  };
},
```

做了这些修改之后，就可以在 Meteor 项目中使用新版的 MUI 了。

另外，根据这个实例，https://github.com/rkstar/meteor-material-ui-example，app.browserify.js 文件内容可以这样写：

```js
// NOTE:
// "let" keyword will not work here!  it throws errors.
// this must either be declared without a keyword (global) or with "var"
var injectTapEventPlugin = require("react-tap-event-plugin")

//Needed for onTouchTap
//Can go away when react 1.0 release
//Check this repo:
//https://github.com/zilverline/react-tap-event-plugin
injectTapEventPlugin()
React.initializeTouchEvents(true)

// init material ui
mui = require('material-ui')
```

还有一点值得注意，MUI v0.12.3，使用的 React 版本为 v0.14.0。

安装 React-router 的时候，也会安装 React
