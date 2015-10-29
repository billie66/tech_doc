What is reactivity?

什么是反应性？

We will define reactivity here as the ability of Meteor (or any system) to automatically update the values of variables and objects when the information they depend on changes.

在这里，我们将把反应性定义为 Meteor（或任意系统）在变量或对象所依赖的信息发生变化的时候，可以自动更新变量值或对象的能力，

The most widely-known example or a reactive system is a spreadsheet. Let’s say you have a spreadsheet with a cell A1 that contains a number and another cell B1 that runs the formula =A1+1. If A1 is set to 1, we expect B1 to change to 2. If we then change A1 to 4, how will cell B1 show the correct value of 5? Clearly, B1 needs to run its formula again. On the other hand, running when, say, C5 changes would be ineffective and wasteful. So, we need (1) a way to run B1’s formula over and over again, and (2) a way to tell B1 when to rerun. Meteor has a very clever way of achieving this with the minimum amount of reruns. This is most visible when Meteor updates templates in real-time, but you can run any code reactively.

最广为人知的例子或反应系统就是电子表格。比方说，你有一张电子表格，里面有一个存放数字的单元格 A1，还有另一个执行公式 =A1+1 单元格 B1。
如果把 A1 设置为1，则期望 B1 的值变为2。如果把 A1 的值改为4，那单元格 B1 是如何显示正确的数值5呢？ 显然，B1 需要再次运行它的公式。

所以，我们需要（1）一种反复运行 B1 公式的方法。（2）一种通知 B1 运行的方法。 通过最小量的重复运行，Meteor 有一个非常聪明的办法实现需求。
当 Meteor 实时更新模板的时候，这是最显而易见的，但是你也可以反应式地运行任意的代码


### references

http://robertdickert.com/blog/2013/11/14/why-is-my-meteor-app-not-updating-reactively/

https://www.discovermeteor.com/blog/reactivity-basics-meteors-magic-demystified/
