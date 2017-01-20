# Navigation bar configuration

On every screen you can use the built-in navigation bar, you can add a title, left button, right button or change navigation bar’s style. All you need to do is pass appropriate params to `navigationBar` in the `route` configuration:

```jsx
import React, { Component } from 'react';

class Foo extends Component {
  static route = {
    navigationBar: {
      title: 'Assignments',
      backgroundColor: 'tomato',
      elevation: 2,
      renderLeft: () => <MenuButton />,
    },
  };

  render() { /* … */ };
}
```

by @knowbody
