# How Toggle Drawer from NavigatonBar

You can have a custom component to handle this

```jsx
import React, { Component } from 'react';
import {
  TouchableOpacity,
  Image,
  StyleSheet,
  Platform,
} from 'react-native';
import {
  withNavigation,
} from '@exponent/ex-navigation';

@withNavigation
export default class NavigationBarMenuButton extends Component {
  render() {
    const { tintColor, navigation } = this.props;

    // change **drawer** to DrawerNavigation id
    const navigator = navigation.getNavigator('drawer');

    return (
      <TouchableOpacity style={buttonStyles.buttonContainer} onPress={() => navigator.toggleDrawer()}>
        <Image
          style={[buttonStyles.menuButton, tintColor ? { tintColor } : null]}
          source={require('./ExNavigationAssets').menuIcon}
        />
      </TouchableOpacity>
    );
  }
}

const buttonStyles = StyleSheet.create({
  buttonContainer: {
    flex: 1,
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'center',
  },
  menuButton: {
    resizeMode: 'contain',
    ...Platform.select({
      ios: {
        height: 26,
        width: 26,
        marginLeft: 8,
        marginRight: 6,
      },
      android: {
        height: 24,
        width: 24,
        margin: 16,
      },
    }),
  },
});
```

by @sibelius
