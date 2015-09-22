http://www.smashingthingstogether.com/how-to-make-a-custom-sign-up-form-meteor-js/

ttp://blog.benmcmahen.com/post/41741539120/building-a-customized-accounts-ui-for-meteor

Accounts.createUser(options, callback)

On the client, this function logs in as the newly created user on successful
completion. On the server, it returns the newly created user id.

网站用户不需要注册，就可以对每个视频发表评论，不保存任何用户信息

但仍然需要一位管理员，创建视频，更新视频，那管理员功能如何实现？

有管理员，就要保存管理员的信息，那还得借助 accounts-password 包，用邮箱和密码登录

不开放注册界面，只有登录界面，如何实现？

可以在 Meteor 启动的时候，手动把管理员信息添加进去（seed data），这样就不需要注册界面了。

```
Meteor.startup(function() {
  if (Meteor.users.find().count() === 0) {
    Accounts.createUser({
      username: 'test',
      email: 'test@example.com',
      password: 'password'
    });
  }
});
```

但是另一个问题又出现了，这些重要信息保存在哪里呢？ 若开源的话，那每个人都可能成为管理员

Meteor 如何保存重要数据呢？ 使用 Settings.json 文件

相关文章 [Making Use of Settings.json](http://themeteorchef.com/snippets/making-use-of-settings-json/)

即使是这样，只要使用了 accounts-password 模块，用户还是可以在浏览器 console 中，使用 Accounts.createUser 接口注册，怎么解决？

可以禁止这个操作，通过 Accounts.config 接口，设置 forbidClientAccountCreation 选项

```
Accounts.config({
  forbidClientAccountCreation : true
});
```

那问题又出现了，上面的代码写在哪里？ 应该放在 client 和 server 端都能执行的地方

参考 issue <https://github.com/meteor/meteor/issues/828>

那这样 server 端还能使用 Accounts.createUser 接口吗? 可以

经过上面的分析，网站管理员就诞生了。

另外，可以添加下面的模块，控制用户的角色，只能用在 server 端，要不然会有警告信息

```
meteor add alanning:roles
```

但是，如何在 client 端创建用户后，就添加 role 呢？ 有的在 server 端写一个 method, 调用这个方法实现。
测试之后，发现用户注册后，不能自动登录

### 第二部分

即使普通用户看不到新建视频的表单，但代码是开源的，能看懂代码的 cracker，仍然可以在 console 中创建、编辑视频，
所以需要在与视频相关的 methods 中，判断管理员是否登录，若没有登录，则抛出异常

```
if (! this.userId) {
  throw new Meteor.Error('not-admin', "can not manage episodes");
}
```

调用 Meteor.Error 才能把异常从 server 端传到 client 端

另外，就是发表评论的问题了，测试一下，用户不指定 episodeId，是否能在 console 中发表评论? 可以

### 第三部分

meteor 和 react 的结合，再看一遍 getMeteorData 的用途

react 组件中可以直接使用 meteor 模块的接口，比方说 Meteor.user()，那还用使用 getMeteorData() 获取当前登录用户的信息吗？

### Methods location

Methods 所在的位置，既可以在 client 端执行也可以在 server
端执行，可以参考[Optimistic UI](http://info.meteor.com/blog/optimistic-ui-with-meteor-latency-compensation)

### 第四部分 部署到服务器

http://meteortips.com/deployment-tutorial/
