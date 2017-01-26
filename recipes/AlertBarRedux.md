# Alert Bars using redux

Show a piece of an alert bar right below your navigation bar. You can specify text as second argument,
styles and duration (in ms) through options object.
E.g (using redux):

```javascript
const navigatorUID = store.getState().navigation.currentNavigatorUID
store.dispatch(NavigationActions.showLocalAlert(
  navigatorUID, message, {
    text: { color: '#000' },
    container: { backgroundColor: 'grey' },
    duration: 3000,
  })
)
```

by @jsdario
