### 使用 MUI tabs 组件

* 选用默认主题 LightRawTheme

http://material-ui.com/#/customization/themes

```
const { AppBar, AppCanvas, Styles, Tab, Tabs, Paper } = mui;
const { Colors, Typography, Spacing } = Styles;
const ThemeManager = Styles.ThemeManager;
const DefaultRawTheme = Styles.LightRawTheme;

App = React.createClass({
  getInitialState () {
    return {
      muiTheme: ThemeManager.getMuiTheme(DefaultRawTheme)
    };
  },

  childContextTypes: {
    muiTheme: React.PropTypes.object
  },

  getChildContext() {
    return {
      muiTheme: this.state.muiTheme,
    };
  },

  render() {
    return (
      <AppCanvas>
        { this._getTabs() }
        { this.props.children }
      </AppCanvas>
    );
  },
```

### 使用 Tabs 组件

对于 MUI 组件，虽然也能添加 calssName，但是优先级要低于 inline styles，若修改 MUI 组件的样式，使用 inline styles

https://facebook.github.io/react/tips/inline-styles.html

MUI Tabs 的文档 http://material-ui.com/#/components/tabs

```
_getTabs() {
  let styles = {
    root: {
      position: 'fixed',
      height: 64,
      top: 0,
      right: 0,
      zIndex: 4,
      width: '100%'
    },
    container: {
      position: 'absolute',
      right: (Spacing.desktopGutter/2) + 48,
      textTransform: 'uppercase'
    },
    tabs: {
      width: '300px'
    },
    tab: {
      height: 64,
      color: '#727272'
    }
  };

  return (
    <Paper
      style={styles.root}
      zDepth={1}
      rounded={false}>
      <div style={styles.container}>
        <Tabs
          style={styles.tabs}
          tabItemContainerStyle={{backgroundColor: '#fff'}}
          inkBarStyle={{height: '4px', marginTop: '-4px'}}
          value={this.state.tabIndex}
          onChange={this._handleTabsChange}>
          <Tab
            value='1'
            label='Home'
            route='/home'
            style={styles.tab} />
          <Tab
            value='2'
            label='Blogs'
            route='/blogs'
            style={styles.tab} />
          <Tab
            value='3'
            label='About'
            route='/about'
            style={styles.tab} />
        </Tabs>
      </div>
    </Paper>
  );
},

_getSelectedIndex() {
  return this.props.history.isActive('/home') ? '1' :
    this.props.history.isActive('/blogs') ? '2' :
    this.props.history.isActive('/about') ? '3' : '0';
},

_handleTabsChange(value, e, tab) {
  this.props.history.pushState(null, tab.props.route);
  this.setState({tabIndex: this._getSelectedIndex()});
},
```

这里使用了 react-router 的 History mixin 接口

https://github.com/rackt/react-router/blob/master/docs/API.md#history-mixin

### 刷新页面，标签选中

```
componentWillMount() {
  let newMuiTheme = this.state.muiTheme;
  newMuiTheme.inkBar.backgroundColor = "#00bcd4";
  this.setState({
    muiTheme: newMuiTheme,
    tabIndex: this._getSelectedIndex()
  });
},

componentWillReceiveProps(nextProps, nextContext) {
  let newMuiTheme = nextContext.muiTheme ? nextContext.muiTheme : this.state.muiTheme;
  this.setState({
    tabIndex: this._getSelectedIndex(),
    muiTheme: newMuiTheme
  });
},
```

需要理解一下 react 组件的 lifecycle

https://egghead.io/lessons/react-component-lifecycle-mounting-usage
https://egghead.io/lessons/react-component-lifecycle-updating?series=react-fundamentals
