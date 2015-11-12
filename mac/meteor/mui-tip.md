### MUI v0.13.2

>Warning: Failed propType: Required prop `index` was not specified in `MenuItem`. Check the render method of `AppBody`.

https://github.com/callemall/material-ui/issues/1346

解决方法，在 app.browserify.js 文件中，导出 MenuItem 组件

```
MenuItem = require('material-ui/lib/menus/menu-item')
```

>v0.13.2 不包含 react-tap-event-plugin NPM 模块，需要单独安装
