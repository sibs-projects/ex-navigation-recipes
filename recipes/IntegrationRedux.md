# Integrate with your existing Redux store

Behind the scenes ExNavigation manages your navigation state using
Redux in its own store. If you'd like to store the navigation state
on your app's store, you can use the `createStoreWithNavigation`
function when creating the store and then manually provide the
`NavigationContext`, initialized with your app's store.

```javascript
/* Your store definition, let's say state/Store.js */

import { createNavigationEnabledStore, NavigationReducer } from '@exponent/ex-navigation';
import { combineReducers, createStore } from 'redux';

const createStoreWithNavigation = createNavigationEnabledStore({
  createStore,
  navigationStateKey: 'navigation',
});

const store = createStoreWithNavigation(
  /* combineReducers and your normal create store things here! */
  combineReducers({
    navigation: NavigationReducer,
    // other reducers
  })
);

export default store;
```

```javascript
/* Your routes, Router.js */

import { createRouter } from '@exponent/ex-navigation';
import HomeScreen from './HomeScreen';

export const Router = createRouter(() => ({
  home: () => HomeScreen,
}));
```

```diff
 /* The top level of your app, often in main.js or index.[ios/android].js */

 import {
   NavigationContext,
   NavigationProvider,
   StackNavigation,
 } from '@exponent/ex-navigation';

 import Store from './state/Store';
 import Router from './Router';

+const navigationContext = new NavigationContext({
+  router: Router,
+  store: Store,
+})

 return (
   <Provider store={Store}>
+    <NavigationProvider context={navigationContext}>
       <StackNavigation yourUsualPropsHere />
     </NavigationProvider>
   </Provider>
 )
```

by @exponent
