Meteor 和 react 结合在一起使用，意味着 view 层不使用 meteor 自带的 template 模板，而是由
react 组件代替，数据管理则由 meteor 负责。

### 创建项目

首先创建一个 meteor 应用名为 meteor-react-demo，

```bash
mkdir meteor
cd meteor
meteor create meteor-react-demo
cd meteor-react-demo
```

项目生成之后，进入项目根目录，删除生成的三个默认文件。

### 安装官方的 react 软件包

```bash
meteor add react
```

react 软件包中捆绑了一些所必需的工具，让 meteor 和 react 很方便的一起使用，其中包括：

* react-runtime: React 库本身
* jsx: 编译器，把 jsx 语句转换成 js，支持 ES6 语法
* react-meteor-data: 一个 React mixin，负责管获取 meteor 数据库或其它组件中的响应式数据（reactive resources）

#### 在 React 组件中使用响应式 Meteor 数据

Meteor 中的许多数据资源都是 "响应式的" - 也就是说，当一些事情发生改变的时候，它们使用 Meteor 中的 Tracker 库通知数据消费者。这样的数据资源包括：

* Meteor.user() - 当前登录的用户
* Mongo.Collection - 一个持久化的数据表，可以从客户端访问
* ReactiveVar - 响应式地存储一个数据
* 许多 Atmosphere 中的软件包提供的其它数据，如 geolocation

react-meteor-data 软件包中包含了一个名为 ReactMeteorData 的 React mixin，一旦你把它添加到 React 组件中后，
就可以在组件中定义一个名为 getMeteorData 的方法。

在 getMeteorData 方法中，你可以访问所有的 Meteor 响应式数据资源（reactive data source）, 还有
this.props 和 this.state 数据。当访问的数据发生改变的时候，随之 getMeteorData 方法会自动重新运行。
getMeteorData 方法的返回数据必须是一个对象，并且这个对象的属性会被复制到组件的 this.data 中。
你可以从组件的 render() 方法中访问 this.data 来使用这些数据。

在每次 getMeteorData 重新运行的时候，在 getMeteorData 方法中使用 Meteor.subscribe 订阅的数据会自动保存，并且当组件卸载的时候会自动清空。
Meteor.subscribe 方法的参数可以由 this.props 和 this.state 数据决定。

以上资料主要翻译了 <http://react-in-meteor.readthedocs.org/en/latest/meteor-data/> 中的一部分文档，
官方文档中还介绍了 react-meteor-data 软件包的设计思路，非常值得读一读。

仔细阅读一下官方文档，对于理解 React 组件和 Meteor 之间的数据通信，协同工作，真是非常有帮助。

### 路由使用 React Router

项目中路由功能的实现，打算使用 React 社区非常有名的 React Router，Meteor 官方的 react-todos 实例中也用的是 React Router。

许多有用的 React 组件和与 React 相关的模块都是 NPM 软件包，通过著名的 Browserify 工具可以把这些软件包捆绑起来提供给客户端使用。

因此为了能够在客户端加载 NPM 软件包，首先我们需要安装两个来自 Meteor 社区的工具： meteorhacks:npm 和 cosmos:browserify

```bash
meteor add meteorhacks:npm cosmos:browserify
```

软件包安装完毕之后，在命令行运行 `meteor` 命令，初始化对 node 软件包的支持。这时会在项目根目录下创建一个 packages/ 的目录，这个目录下将存放 NPM 相关依赖。

第二步是添加要安装的 npm 软件包信息到 packages.json 文件

在项目根目录下面创建一个名为 packages.json 的文件，打开文件，添加下面几行代码：

```js
{
  "react-router": "0.13.3",
  "externalify": "0.1.0"
}
```

这就是我们将要安装的 NPM 软件包，react-router 和 externalify，每个软件包都有相对应的版本号。再次运行 `meteor` 命令，安装这些软件包。

第三步 meteor 应用中导入 react-router 模块

目前，Meteor 不支持使用 require 语法加载模块，所以需要用到 cosmos:browserify 软件包提供的一个特殊文件，来实现这个功能。
在项目中创建一个目录 `client/lib`，进入到新建目录，创建一个文件名为 app.browserify.js。在这个新建的文件里面，你可以
require 任意已安装的 NPM 模块，并把它导出成一个在本项目范围内使用的变量，意味着项目中的每一个 JavaScript 文件都能访问这个变量。
例如，要使用 react-router 模块，在 app.browserify.js 文件添加下面一行代码：

```js
ReactRouter = require('react-router');
```

第四步 配置 browserify 及其 transfoms

Browserify 支持大量的 transforms，可以让你更改 NPM 软件包的捆绑方式。项目中要用到 externalify transform，这样
React Router 将使用 Meteor 中安装的 React 软件包，而不是来自 NPM 中的 React。同样在 `client/lib` 目录下，新创建一个文件
app.browserify.options.json，添加下面一些代码：

```js
{
  "transforms": {
    "externalify": {
      "global": true,
      "external": {
        "react": "React.require"
      }
    }
  }
}
```

注意 app.browserify.js 和 app.browserify.options.json 这两个文件名不能改变。

完成上面四个步骤之后，你就可以在你的 Meteor 应用中使用 React Router 路由了。另外，你也可以通过这种方式，使用其他的 NPM 软件包。

顺便提以下，目前使用这种方式在 Meteor 项目中添加 NPM 软件包，从长远来看，并不是一种理想的方式，还有待提高，具体参考

<http://react-in-meteor.readthedocs.org/en/latest/client-npm/>

### 动手编写 React 组件

首先创建一个布局组件，在 client 目录下，新建一个 App.jsx 的文件，文件内容如下：

```js
const {
  RouteHandler
} = ReactRouter;

App = React.createClass({
  getInitialState: function(){
    return {};
  },
  render: function(){
    return (
      <div>
        <h1>Meteor React Demo</h1>
        <RouteHandler />
      </div>
    );
  }
});
```
接下来创建 items 组件，列出所有的条目，仍然在 client 目录下，创建一个 items.jsx 文件：

```js
Items = React.createClass({
  mixins: [ReactMeteorData],
  getMeteorData: function(){
    return {
      items: ItemsCollection.find({}).fetch()
    };
  },
  getInitialState: function(){
    return {};
  },
  addItem: function(e){
    e.preventDefault();
    var item = React.findDOMNode(this.refs.input).value;
    ItemsCollection.insert({"content": item});
    React.findDOMNode(this.refs.input).value = '';
  },
  render: function(){
    return (
      <div>
        <ul>
          {this.data.items.map(function(item){
            return <li key={item._id}>{item.content}</li>;
          })}
        </ul>
        <form onSubmit={this.addItem}>
          <input type="text" ref="input"/>
          <button type="submit">Add Item</button>
        </form>
      </div>
    );
  }
});
```
下面，我们需要在数据库中创建一张表 items，它既可以被 server 访问也可以被 client
访问，所以我们在项目根目录的 lib 目录下，创建一个 collection.js 文件：

```bash
mkdir lib
cd lib
touch collection.js
```

collection.js 文件内容如下：

```js
ItemsCollection = new Mongo.Collection("items");
```

最后定义路由，因为路由是运行在客户端的，所以把路由文件 routes.jsx 放到 client 目录下，内容如下：

```js
const {
  Route
} = ReactRouter;

const routes = (
  <Route name="root" handler={App} path="/">
    <Route name="items" path="/items" handler={Items} />
  </Route>
)

const router = ReactRouter.create({
  routes: routes,
  location: ReactRouter.HistoryLocation
});

Meteor.startup(function () {
  router.run(function (Handler, state) {
    React.render(<Handler/>, document.body);
  });
});
```

到目前为止，这个 meteor-react-demo 就搭建完了，打开浏览器，访问 `http://localhost:3000` 可以看到 `Meteor React Demo` 几个字样。

访问 `http://localhost:3000/items` 网址，则会看到一个输入框，输入一些字符，提交之后，你刚输入的字符就会在输入框上面显示出来。
