几乎每一个 web 应用都会带用到用户认证功能，那么实现这个功能，若用到的工具不同，开发效率则大相径庭。

那用 meteor 框架的开发这套用户认证系统，效率如何呢？ 效率很高，很少的代码就能把功能实现出来，真是很神奇。

新建一个 meteor 项目，名为 meteor-accounts, 运行命令：

```bash
meteor new meteor-accounts
cd meteor-accounts
```

进入到 meteor-accounts 目录下，删除自动生成的三个文件。

### 安装项目需要的软件包

首先，需要安装一个软件包，在命令行中运行命令：

```bash
meteor add accounts-password
```

accounts-password 提供了一套完整的基于密码的登录系统，还包括找回密码功能，具体查看文档 [Meteor Accounts]((https://www.meteor.com/accounts))。

另外，meteor 默认不提供路由功能，所以还需要安装一个包：

```bash
meteor add iron:router
```

[iron-router](https://atmospherejs.com/iron/router) 是目前 meteor 社区内最普遍使用的具备路由功能的软件包。
顺便说一下，这个软件包名由两部分组成，冒号是分隔符，iron 是开发者的名字，router 则是包名本身。这是由第三方开发者所开发软件的命名规范。

### 组织项目文件结构

接下来就是编写页面了。这里要简单介绍一下 meteor 所建应用的文件组织形式，实际上是非常灵活的，你可以按照任意方式组织，
但是要是项目比较大的话，还是遵照一定的规则，代码会更容易维护。meteor 保留了几个特殊目录，分别是：

* client 目录中的所有文件只会在客户端加载
* server 目录中的文件只在服务器端运行
* public 目录中存放一些图片，字库，favicon.ico 等资源，专为客户端服务
* private 目录中文件只能由服务器端代码访问，可以通过 Assets API 加载
* client/compatibility 与 JS 库的兼容性相关
* texts 存在与本地测试相关的代码

还有一些规范，具体查看文档 [Structuring your application](http://docs.meteor.com/#/full/structuringyourapp)

在项目的根目录下，创建一个新目录，执行下面的命令：

```bash
mkdir client
cd client
mkdir templates
cd templates
```

命名执行完毕之后，进入到 templates 目录下，这里将存放项目所需的模板文件以及与之配合的 JS 和 CSS 文件。

### 用户注册模块

首先写一个用户注册页面吧，在 templates 目录下，创建一个名为 signup.html 的新文件，添加一些代码进去：

```html
<template name="signup">
  <h2>Signup</h2>
  <form class="signup">
    <p>Email: <input type="email" name="email"></p>
    <p>Password: <input type="password" name="password"></p>
    <p><input type="submit" value="signup"></p>
  </form>
</template>
```
添加了一个名为 signup 的模板。用户注册页面有一张表单，包含两个输入框，邮箱和密码，还有一个注册按钮。页面写好了，那接下来添加路由文件，访问页面。

在项目根目录下新建一个 lib 目录，运行：

```bash
mkdir lib
cd lib
touch router.js
```

打开 router.js 文件，添加一个代码：

```js
Router.route('/signup');
```

然后在命令行中执行 `meteor` 命令，启动项目。在浏览器地址栏中输入 `http://localhost:3000/signup`, 就可以访问用户注册页面了。
这时你点击注册按钮没有任何反映，按照一般的操作流程，点击按钮之后，用户注册成功，后台会在数据库中添加一条新的用户信息，然后用户会跳转到另一个页面。

下面我们就一步步实现这些功能，首先把用户提交的信息存入数据库，meteor 默认使用 mongodb 数据库。回到 templates 目录下，新建一个名为 signup.js 的文件。
添加下面一些代码：

```js
// signup.js
Template.signup.events({
  'submit form': function(event){
    event.preventDefault();
    var email = $('[name=email]').val();
    var password = $('[name=password]').val();
    Accounts.createUser({
      email: email,
      password: password
    });
  }
});
```

通过模板对象的 events 接口，来定义模板对象 Template.signup 的事件处理程序，如上，表单的 submit 事件。解释一下代码，
当用户点击注册按钮之后，就会触发 submit 事件处理程序，首先阻止事件默认行为，得到用户的邮箱和密码信息，然后调用 accounts-password 提供的
Accounts.createUser 接口把用户信息保存到 mogodb 数据库中。

下一步就是实现页面跳转，比如说用户注册成功之后，跳转到网站首页。再到 templates 目录下新建一个 home.html 的文件，

```html
<template name="home">
  <div class="home">
    Welcome to here!
  </div>
</template>
```

然后添加首页路由, 打开 router.js 文件，添加代码：

```js
Router.route('/', {
  template: 'home'
});
```

一个斜杠字符 / 就能代表首页路由，但还要具体指明首页要加载的模板文件，为 Router.route() 接口传递一个对象参数，配置模板名称。
现在访问网站首页，就可以看到 `Welcom to here` 几个字了。那如何从用户注册页面调到首页呢？ 很简单，只需要一行代码就解决了。

打开 signup.js 文件，给 submit 事件处理程序的末尾添加一行代码：

```js
// signup.js
Template.signup.events({
  'submit form': function(event){
    event.preventDefault();
    var email = $('[name=email]').val();
    var password = $('[name=password]').val();
    Accounts.createUser({
      email: email,
      password: password
    });
    Router.go('home');
  }
});
```
到目前为止，用户就可以在网站中注册账户了。当用户注册之后，你可以打开浏览器中的 console 控制台，查看用户信息是否存入了数据库：

```js
Meteor.users.find().fetch()
```

比如说，邮箱为 aa@aa.com 的用户注册之后，其注册信息在 console 中显示如下：
这里添加一张图片

### 用户退出模块

为了操作方便，在 templates 目录下，新建一个布局模板 layout.html，代码如下：

```html
<template name="layout">
  {{> navigation}}
  {{> yield}}
</template>
```

还要定义一个 navigation.html 模板文件，添加如下代码：

```html
<template name="navigation">
  <ul>
    <li><a href="/">Home</a></li>
    {{#if currentUser}}
      <a href="#" class="logout">Log Out</a>
    {{else}}
      <a href="/login">Log In</a>
      <a href="/signup">Sign Up</a>
    {{/if}}
  </ul>
</template>
```

用户的退出操作包含在 navigation 模板中，其中的 currentUser 是由 meteor 自带的 accounts-base 软件包提供的接口，用来判断用户是否登录。

接下来就定义 navigation 模板中的事件处理程序，创建一个新文件 navigation.js，代码如下：

```js
Template.navigation.events({
  'click .logout': function(event){
      event.preventDefault();
      Meteor.logout();
      Router.go('login');
  }
});
```

这里只有一个事件处理程序，调用 meteor 自带的 Meteor.logout() 接口退出登录。

最后，还要修改一下路由，配置项目所用的布局模板，在 router.js 文件开头添加几行代码：

```js
Router.configure({
  layoutTemplate: 'layout'
});
```

### 用户登录模块

通过上述内容，为 meteor 应用添加新功能的基本流程，我们也大概弄明白了。首先创建一个登录模板，在 templates 目录下，
新建一个 login.html 文件，代码如下：

```html
<template name="login">
  <h2>Login</h2>
  <form class="login">
    <p>Email: <input type="email" name="email"></p>
    <p>Password: <input type="password" name="password"></p>
    <p><input type="submit" value="Login"></p>
  </form>
</template>
```

看起来和 signup 模板差不多，但功能是不一样的，看一下 login.js 文件中的代码就知道了。

```js
Template.login.events({
  'submit form': function(event){
    event.preventDefault();
    var email = $('[name=email]').val();
    var password = $('[name=password]').val();
    Meteor.loginWithPassword(email, password);
    Router.go('home');
  }
});
```

在 submit 事件处理程序中，调用了由 accounts-password 包提供的 Meteor.loginWithPassword 接口，让用户登录网站。

然后再添加登录路由，修改 router.js 文件：

```js
Router.route('/login');
```

这样就实现了基本的用户认证系统，是不是很方便？
