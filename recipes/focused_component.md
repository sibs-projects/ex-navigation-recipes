# Focused component

You can check if your component is `focused` to do logic, like changing `StatusBar` style.

You can also render `null` if your component is not `focused`, so you can improve app performance


```jsx
export class ScrollTabs extends React.Component {
  static route = {
    navigationBar: {
      title: function ({title = i18n.home}) {
        return title
      },
      renderLeft: function () {
        return <UserMenu />
      },
      renderRight: function (params) {
        if (params.getTitle() !== i18n.routines) {
          return <Reload />
        } else {
          return <History />
        }
      }
    }
  }

  componentDidMount () {
      if (Platform.OS === 'android' && Platform.Version >= 23) StatusBar.setBackgroundColor('white', true)
      StatusBar.setBarStyle('dark-content', true)
  }

  componentWillReceiveProps(nextProps) {
    if (nextProps.isFocused && !this.props.isFocused) {
      if (Platform.OS === 'android' && Platform.Version >= 23) StatusBar.setBackgroundColor('white', true)
      StatusBar.setBarStyle('dark-content', true)
    }
  }


  render () {
    if (this.props.navigator.getCurrentRoute().routeName !== 'Home') return null

    // render goes on...

```

by @jsdario
