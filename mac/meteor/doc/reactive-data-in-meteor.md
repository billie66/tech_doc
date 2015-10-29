我们在 Meteor 中看到的很多魔法，其实是由 Meteor 奇妙的响应式数据模型（reactive data model）制造的，
若在应用中能够合理的实现响应式数据模型，在数据或状态改变的时候，不需要程序员进行任何 DOM 操作，应用就能够自动更新，。
然而，对于 meteor 初学者来说，可能并没有完全弄明白什么是响应式（reactive），响应式怎么样？ 什么时候使用响应式？

> 反应性数据源可以触发下面一些数据的改动：
>
>Session variables
Database queries on Collections
Meteor.status
The ready() method on a subscription handle
Meteor.user
Meteor.userId
Meteor.loggingIn

上面列表中的后五项，显然只适合于非常具体的运行环境，而前两项可用于更广义的反应性。

We’ll have a look at the benefits of both, as well as observing that there are actually other ways of achieving reactivity, both using MDG packages and by building reactive sources oneself.

我们将看一看这两项的好处，同时也看一下其他实现反应性的方式，使用 MDG 包和创建响应式数据源

Session 提供了方便的接口来存储和获取任意的 key-value 数据对，且默认是响应式的。意思是说，如果模板的
helpers 或者 Tracker.autorun 调用了 Session.get 方法获取某个键值，而这个键值通过 Session.set 方法设置在了其他地方。例如：

```js
Session.setDefault('myName', 'Richard');

Template.greeting.helpers({
  myName: function() {
    return Session.get('myName');
  }
});
```

```html
<template name="greeting">
  <p>Hello there, {{myName}}</p>
</template>
```

在这种情况下，如果我们在浏览器的 console 中执行 `Session.set('myName', 'Claire')`，此时
greeting 模板中的 <p> 标签的内容会更新为 `Hello there, Claire`，正如我们对 Meteor 反应性魔法所期望的结果一样。


如果你想使用 Session 变量，需要牢记以下几点：

Session values persist across hot reloads. This is potentially useful during development, but it’s something you need to be aware of to avoid unexpected behaviour.

Session 数值会在各热加载期间持久存储。在项目开发期间这是有潜在帮助的，但也是你需要注意的事情，以免发生意外行为。

The API isn’t particularly extensive. In addition to get and set, you’re provided with equals and setDefault, but this is as far as Session methods extend, which can seem quite clunky if you’re storing large, nested objects this way. Of course, you could write your own helper methods, but there may be easier alternatives (see below).

会话 API 不是特别广泛。除了 get 和 set 方法之外，只有 equals 和 setDefault 两个方法，
如果用这种方式存储庞大的，嵌套式的对象，可能看起来相当笨拙。当然，你可以编写自己的 helper 方法，但是有更简便的替代方式。

The values you store will always sit in the global namespace. Whilst this shouldn’t be a problem from the perspective of namespace conflicts (as they’re all wrapped inside the Session object), you need to be aware that a Meteor-savvy user can always get and set any Session value in the browser console, whether you’d rather it be private or not.

会话值总是存储在全局命名空间内。虽然这不是一个问题，从命名空间冲突的观点来看（它们都被包裹在
Session 对象中），你需要注意，一个 Meteor 高手可以借助浏览器 console 读取和设置任意的会话值，不管数据是私有的还是公开的。

Session variables will not cause their dependencies to rerun when Session.set is supplied with a value which is equal to the existing value. This may be an advantage as it potentially reduces DOM thrashing, but bear in mind that you cannot assume dependencies will rerun simply because you’ve called Session.set.

会话变量将不会引起它们的依赖代码重新运行，当 Session.set 设置的新值与原来的值相同时。这可能是一个优势，因为它减少了
DOM 的渲染，但是应该记住，你不能假定依赖代码将会重新运行，只是因为你已经调用了 Session.set 方法。

Database queries on Collections

The topic of Collections and their use in Meteor applications is a very large one indeed, so I’ll keep this section brief. However, these are the main points regarding reactive data:

关于响应式数据，collections 占据着重要地位：

It’s perfectly possible (and often very useful) to define client-only collections, which will be sessional, and won’t be synchronised with the server. These give you the full power of the minimongo API without any pub/sub overhead, and have reactivity baked in.

完全有可能（而且经常非常有用）只定义客户端 collections, 可能是会话数据，不会同步到服务器端。提供给你全面的 minimongo 的接口，没有任何 pub/sub 耗损，并且数据是响应式的

For collections to drive reactivity, you actually need to be querying the database from within the Template helper or autorun block; i.e. there needs to be a Collection.find or findOne or count within the helper or autorun - you can’t fetch() results somewhere else, store them in a variable and expect references to that variable to be reactive (unless of course it’s a reactive variable…).

为了 collections 能够驱动反应性，实际上，你需要从模板 helper 或者 autorun 代码块中查询数据库；例如，在模板
helper 或 autorun 代码块中使用 Collection.find 或 findone 或 count 方法，你不可以把在其他地方
fetch() 到的数据结果存储到变量中，并期望对那个变量的引用是响应式的（除非它是一个响应式变量）

You can also define a private, client-only collection with the var keyword (i.e. var MyCollection = new Mongo.Collection(null)). This will provide a private, reactive structure, which can be used as a key/value store alternative to Session variables. The only difficulty is that you will only be able to update values by using the _id field (which you’ll either have to repeatedly query or else store somewhere) due to the way Meteor treats client-side code. Like Session variables, you can also only store EJSON-able values.

你也可以定义一个私有的，只有客户端使用的 collection，通过 var 关键字（例如，var MyCollection = new Mongo.Collection(null)）。
这将生成一个私有的响应式数据结构，这可以用做一个会话变量的存储方式。唯一的困难是，你只能通过 _id 字段来更新数值，归结于
Meteor 对待客户端代码的方式。正如会话变量，你也只能存储 [EJSON](http://docs.meteor.com/#/full/ejson) 数据。

ReactiveVar and ReactiveDict Packages

In fact, Meteor also ships with two other reactive data sources out of the box, ReactiveVar and ReactiveDict. Both need to be added as packages (even though they’re present in the standard distribution), and only ReactiveVar appears in the official documentation, but both can be extremely useful for developers.

事实上，Meteor 还附带了其他两个响应式数据源，ReactiveVar 和 ReactiveDict。它们两个都需要单独安装，官方文档只支持 ReactiveVar，但这两个包对开发者非常有帮助。

ReactiveVar

安装 ReactiveVar 软件包：

```bash
$ meteor add reactive-var
```

ReactiveVar is in some respects an atomic reactive unit, like a single Session variable, with the disadvantage that its values will not persist across hot code pushes. However, there are lots of advantages:

在某些方面 ReactiveVar 是一个原子反应单位，就像一个单独的 Session 变量，其数值在各个热代码推送之间不会保留。然而，这有很多好处：

ReactiveVar instances can be scoped as any normal Javascript variable, and can contain any value - not just EJSON.

ReactiveVar 实例的作用域和任何普通的 Javascript 变量一样，也可以包含任何数值，不仅仅是 EJSON 数据。

They also allow you (although they don’t compel you) to define a proprietary equals function, which will determine the exact circumstances under which resetting the value of the variable will invalidate dependent computations. This allows you to very easily overwrite the default, Session-like behaviour if required, and ensure that the setting of a ReactiveVar value will always invalidate dependent computations. You could also supply even more subtle logic.

它们也允许你（虽然不强迫）定义一个专属的 equals 函数，用来确定什么情况下重置变量值会导致依赖计算失效。
如果需要的话，这可以让你非常容易的覆盖默认的，类似会话变量行为，并且确保设置一个 ReactiveVar 数值总能让依赖计算失效。你也可以提供更多细微的逻辑。

However, by default, updating the value of a ReactiveVar will not invalidate computations which depend on it if the new value is the same as the existing one, exactly like Session variables (provided no equals function is supplied).

然而，默认情况下，更新一个 ReactiveVar 数值将不会让依赖计算失效，要看具体情况，如果新设置的数值与原来的值相同的情况下，正如会话变量（假定没有定义 equals 函数）

To reiterate, unlike Session variables, the value of a ReactiveVar will not be retained across hot code pushes.

对于迭代，不同于会话变量，一个 ReactiveVar 变量值在各个热代码推送之间不会保留。

ReactiveDict

安装 ReactiveDict 软件包

```bash
meteor add reactive-dict
```

ReactiveDict is the prototype which is used to construct the global Session object. What this means is that all the familiar Session methods and properties are available for any other ReactiveDict you might construct, except you wouldn’t necessarily have to leave the parent object in the global namespace. Some other things to bear in mind:

ReactiveDict 是一个用来构建全局 Session 对象的原型。意思是说，你所熟悉的 Session 方法和属性都能用于其它的 ReactiveDict 实例，
除非你不一定要离开位于全局命名空间中的父对象。一些事情需要牢记：

You can pass an object containing migration data into the constructor - i.e. you can seed the ReactiveDict when it’s created:

构建 ReactiveDict 实例的时候，可以给初始化

```bash
myDict = new ReactiveDict({foo: 'bar'});
```

Given that, like a Session object, each key has its own associated dependency, the only reason for creating multiple ReactiveDicts is to keep the information in each private. Beyond this, segregating your keys into different ReactiveDicts will have no impact on your app’s reactivity.


### reference

* http://richsilv.github.io/meteor/meteor-reactive-data-types/
