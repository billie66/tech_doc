### react context

http://codetheory.in/passing-data-across-components-with-contexts-in-reactjs/

### references

http://jamesknelson.com/learn-raw-react-no-jsx-flux-es6-webpack/?utm_source=javascriptweekly&utm_medium=email

https://github.com/facebook/react/issues/3610

### componentDidMount

https://facebook.github.io/react/docs/component-specs.html#mounting-componentdidmount

当组件首次渲染（render）之后，会立即触发 componentDidMount 方法，在这个阶段可以获得其子组件的 DOM 结点，也可以用 Jquery 提供的接口操作组件，如控制组件的显示和隐藏

  componentDidMount() {
    $( ".loading-icon" ).delay( 1000 ).fadeOut( 'slow', function() {
      $( ".loading-data" ).fadeIn( 'slow' );
    });
  },
让 loading-icon 显示一秒隐藏之后，再显示要加载数据 loading-data

http://busypeoples.github.io/post/react-component-lifecycle/

Any DOM interactions should always happen in this phase not inside the render method.
in this phase 指的是 componentDidMount
