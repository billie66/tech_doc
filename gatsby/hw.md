### Node.js 版本

```
node -v
```

输出结果是 v8.9.4

### 全局安装 Gatsby

```
npm install -g gatsby-cli
```

### 创建一个 hello world 项目

```
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

### 启动项目

```
yarn start
```

### 页面间导航

#### Gatsby Link

通过 Gatsby 提供的 Link 组件实现页面之间的导航，Gatsby 的 Link 组件对 @reach/router 的 Link 组件进行了封装，并专门针对 Gatsby 进行了优化

```
import { Link } from 'gatsby'
```

可以给 Gatsby 的 Link 组件添加 activeStyle 或者 activeClassName 属性控制它与当前页面的 URL 相匹配的时候的样式

```
<Link to="/about" activeStyle={{color: "purple"}}>about page</Link>
```

Gatsby 基于路由进行代码分离, 这意味着当打开新页面的时候，页面需要的代码片段还没有加载，预加载可以解决这个问题

当链接进入到页面可视区（viewport），就会触发预加载

#### 可编程式的导航

这里是说，在事件处理函数中可以使用的导航方法

```
import { navigate } from 'gatsby'
```
