### update to meteor v1.3

```
meteor update --release 1.3
```

### create a new app

```
meteor create myapp
cd myapp
meteor npm install
meteor
```

### install react

```
meteor npm install --save react react-dom
```

output:

```
react-dom@0.14.8 node_modules/react-dom

react@0.14.8 node_modules/react
├── envify@3.4.0 (through@2.3.8, jstransform@10.1.0)
└── fbjs@0.6.1 (whatwg-fetch@0.9.0, ua-parser-js@0.7.10, promise@7.1.1, loose-envify@1.1.0, core-js@1.2.6)
```

### use meteor data inside react components

```
meteor npm install --save react-addons-pure-render-mixin
meteor add react-meteor-data
```

### file structure

* http://guide.meteor.com/structure.html

### create an project with the specific meteor version

只要在创建项目的时候，指定所需要的 meteor 版本号，则对应的 meteor 版本会被自动安装。

```
meteor create myapp --release 1.2.1
```

### meteor npm install vs npm install (meteor v1.3)

<https://forums.meteor.com/t/meteor-npm-install-vs-npm-install/20495>
