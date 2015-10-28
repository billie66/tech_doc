* npm install --savee react react-dom

* npm install --save-dev babel-loader

* npm install --save history react-router@latest

* npm i --save-dev webpack-dev-server

modify package.json file

```
"scripts": {
    "build": "webpack",
    "dev": "webpack-dev-server --devtool eval --progress --colors --hot --content-base build"
  }
```

modify webpack.config.js file

```
var path = require('path');
entry: [
  'webpack-dev-server/client?http://localhost:8080',
  'webpack/hot/dev-server',
  path.resolve(__dirname, 'app/index.js')
],
output: {
  path: path.resolve(__dirname, 'build'),
  filename: 'bundle.js',
},
```

* npm i --save-dev react-hot-loader

modify webpack.config.js file

```
module: {
  loaders: [
    { test: /\.js$/,
      exclude: /node_modules/,
      loaders: ['react-hot', 'babel-loader']
    }
  ]
}
```

modify app/index.js file
```
let rootInstance = render((<Router>...</Router>), document.getElementById('app'));

// Then just copy and paste this part at the bottom of the file
if (module.hot) {
  require('react-hot-loader/Injection').RootInstanceProvider.injectProvider({
    getRootInstances: function () {
      // Help React Hot Loader figure out the root component instances on the page:
      return [rootInstance];
    }
  });
}
```

* react-router and history with webpack-dev-server

history module can make url pretty, for example, http://localhost:8080/main,

```
import { createHistory } from 'history'
let history = createHistory()

<Router history={history}>...</Router>
```

but refresh the page, then you can not get the content again, the problem is caused by webpack-dev-server, so you should add the code above to webpack.config.js

```
  devServer: {
    historyApiFallback: true
  }
```

GitHub Issue：https://github.com/rackt/react-router/issues/676
