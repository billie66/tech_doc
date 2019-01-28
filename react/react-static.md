### dev env

```
nvm install v10.15.0
npm install -g yarn
yarn global add react-static
```

### version

```
react-static --version
```

output: 6.3.0

### check npm package version used in project

```
yarn list react-static
```

### haoqi demo

use the basic template to create a haoqi demo

```
react-static create
```

还没有 material-ui 的样例

### 启动项目

开发环境启动项目

```
yarn start
```

运行起来之后，react-hot-loader 生效

### 安装 redux

```
yarn add redux react-redux redux-thunk
```

### 使用 redux

没有特别的地方，按照平常项目中使用 redux 方式可以让 redux 在 `react_static`
中正常工作。需要注意的地方就是，只属于浏览器端的专属名词，需要用下面代码包裹一下,要不然不能编译成功。

```
if (typeof window !== 'undefine') {
  localstorage.setItem({})
}
```

### 安装 material-ui

接下来，要做的工作就是项目中集成 material-ui，不知道这一步会不会出问题。



