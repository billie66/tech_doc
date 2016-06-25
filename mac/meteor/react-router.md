### How to get previous path

```
<Route component={App}>
  {/* ... other routes */
</Route>

var App = React.createClass({
  getInitialState () {
    return { showBackButton: false }
  },

  componentWillReceiveProps(nextProps) {
    var routeChanged = nextProps.location !== this.props.location
    this.setState({ showBackButton: routeChanged })
  }
})
```

<https://github.com/reactjs/react-router/issues/1066>