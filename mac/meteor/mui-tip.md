### MUI v0.13.2

>Warning: Failed propType: Required prop `index` was not specified in `MenuItem`. Check the render method of `AppBody`.

https://github.com/callemall/material-ui/issues/1346

解决方法，在 app.browserify.js 文件中，导出 MenuItem 组件

```
MenuItem = require('material-ui/lib/menus/menu-item')
```

>v0.13.2 不包含 react-tap-event-plugin NPM 模块，需要单独安装，安装 v0.2.1 版本，但是这个组合会导致 MUI 的 leftnav 组件出现故障
