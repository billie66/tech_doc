### 安装 react-router

更改 packages.json 文件，添加一行代码：

```
"react-router": "1.0.0-rc4"
```

回到命令行，运行 meteor 命令，安装 react-router

```
npm-container: updating npm dependencies -- externalify, material-ui, react-router...
```

注意 react-router 包含了 history 模块，所以不需要单独安装 history

### 使用 react-router

更改 client/lib/app.browserify.js 文件

```
ReactRouter = require("react-router");
```

创建一个 client/Home.jsx 文件：

```
const { RaisedButton } = mui;
const { Link } = ReactRouter;

Home = React.createClass({
  render() {
    return (
      <div>
        <p>Welcome to my corner</p>
        <Link to="/about">
          <RaisedButton label="ABOUT ME" />
        </Link>
        {this.props.children}
      </div>
    );
  }
});
```

创建一个新文件 client/About.jsx 文件：

```
const { Link } = ReactRouter;
const { RaisedButton } = mui;

About = React.createClass({
  render() {
    return (
      <div>
        <p>Hi, I am Peter</p>
        <Link to="/">
          <RaisedButton label="HOME" />
        </Link>
      </div>
    );
  }
});
```

更新 startup.jsx 文件：

```
const {
  Router,
  Route
} = ReactRouter;

const Routes = (
  <Route path="/" component={Home}>
    <Route path="about" component={About}/>
  </Route>
);

Meteor.startup(function() {
  injectTapEventPlugin();
  ReactDOM.render((
    <Router>
      {Routes}
    </Router>
  ), document.getElementById("container"));
});
```

这时，点击页面内的按钮，就可以在两个页面之间进行切换了。

### 美化 URL
此时查看页面的 url，会发现很不美观，如何解决这个问题，就需要用到 history NPM 模块提供的功能了。

首先，需要导入 history 模块，修改 client/lib/app.browserify.js 文件

```
History = require("history");
```

修改 startup.jsx 文件，添加一行代码

```
const { createHistory } = History;

```

再修改 startup.jsx 文件中与 Router 相关的代码：

```
<Router history={createHistory()}>
  {Routes}
</Router>
```

这里的 createHistory 方法就是 createBrowserHistory 方法

http://rackt.org/history/stable/GettingStarted.html

https://github.com/rackt/react-router/blob/master/docs/guides/basics/Histories.md

### 判断当前页面 url

现在，如果访问 localhost:300/about 页面，也会出现 `ABOUT ME` 按钮，如何让它只出现在首页

修改 cliet/Home.jsx 文件，如下：

```
const { RaisedButton } = mui;
const { Link } = ReactRouter;

Home = React.createClass({
  render() {
    let isActive = this.props.history.isActive('/about');
    let aboutButton = '';
    if (!isActive) {
      aboutButton = (
        <Link to="/about">
          <RaisedButton label="ABOUT ME" />
        </Link>
      );
    }
    return (
      <div>
        <p>Welcome to my corner</p>
        {this.props.children}
        { aboutButton }
      </div>
    );
  }
});
```
