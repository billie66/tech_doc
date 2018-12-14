### reselect

<http://blog.rangle.io/react-and-redux-performance-with-reselect/>

### 废弃的 React 生命周期方法

从 React v16.3 版本开始，废弃了三个生命周期方法：

- componentWillMount
  之前需要在这个方法中完成的功能，可以移到构造函数中去实现

- componentWillReceiveProps
  由 getDerivedStateFromProps 代替

- componentWillUpdate
  由 getSnapshotBeforeUpdate 代替

### 静态生命周期方法（static lifecycle methods）

static 生命周期方法不能使用 this 关键字

- getDerivedStateFromProps
  唯一的功能就是让组件能够根据 props 的改变更新内部 state

  componentWillReceiveProps 和 getDerivedStateFromProps 都增加了组件的复杂度，越复杂就越容易出 bug，所以官方提倡不使用这两个函数，而是使用更简单的替代方案

  只要父组件重新渲染，那么不管父组件传递给子组件的 props 是否改变，这两个生命周期函数都会在子组件中执行。因此，通过这两个函数中的任意一个无条件的重写 state 都是不安全的，这样做会导致状态更新丢失

  举个例子

  ```js
  class EmailInput extends Component {
    state = { email: this.props.email }

    render() {
      return <input onChange={this.handleChange} value={this.state.email} />
    }

    handleChange = event => {
      this.setState({ email: event.target.value })
    }

    componentWillReceiveProps(nextProps) {
      // This will erase any local state updates!
      // Do not do this.
      this.setState({ email: nextProps.email })
    }
  }
  ```

  一开始，这段代码看起来没啥问题。但实际上是有问题的，当 EmailInput 组件的父组件重新渲染的时候，你在输入框中写入的内容会被清空，显示最初的 email 值

- getSnapshotBeforeUpdate

### React 组件的生命周期

- 挂载（Mounting)
  把 React 组件加载到 DOM 上
  constructor（设置组件最初的状态） -> getDerivedStateFromProps -> render（ React 更新 DOM 和 refs） -> componentDidMount（与 DOM 交互，调用 API）

- 更新（Updating)
  导致组件更新的操作：新的 props，setState(), forceUpdate()
  若 SCU 返回值为 false
  getDerivedStateFromProps -> shouldComponentUpdate
  若 SCU 返回值为 true
  getDerivedStateFromProps -> shouldComponentUpdate -> render -> getSnapshotBeforeUpdate -> React 更新 DOM 和 refs -> componentDidUpdate

- 卸载 (Unmounting)
  componentWillUnmount

### 什么是 derived state
