# How can I slide my view from bottom up (transition) from one screen to the other?

You simply need to add `styles` to your `route` configuration in the Component that you are pushing onto StackNavigation:

```jsx
import React, { Component } from 'react';
import { NavigationStyles } from '@exponent/ex-navigation';

class Foo extends Component {
  static route = {
    styles: {
      ...NavigationStyles.SlideVertical,
    },
  };

  render() { /* … */ };
}
```

by @knowbody
