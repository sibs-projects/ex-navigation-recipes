# Perform navigation actions from outside of a component

You might be using some Redux middleware like saga, thunk, promise, or
effex (we recommend [effex](https://github.com/exponent/redux-effex)
because we love `async/await`). Whatever you're using, you no longer
have access to `this.props.navigator` and the like. What to do?
Well as long as you include your navigation state inside of your Redux
store, you can dispatch a NavigationAction to it -- after all, this is
what `this.props.navigator.push` etc. do behind the scenes.

In the following example we call `getState` and `dispatch` directly on
your store -- feel free to change this to whatever the equivalent is
for your context (eg: if this was effex, `dispatch` and `getState` would
be passed in to the `goHome` function).

```javascript
import { NavigationActions } from '@exponent/ex-navigation'
import Store from '../state/Store';
import Router from './Router'

export default function goHome() {
  let navigatorUID = Store.getState().navigation.currentNavigatorUID;
  Store.dispatch(NavigationActions.push(navigatorUID, Router.getRoute('home')))
}
```

by @exponent
