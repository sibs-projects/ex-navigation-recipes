### Screen Tracking / Analytics

You might want to do some screen tracking in your apps. Since the entire navigation state is in redux, screen tracking is as simple as writing a redux middleware. Below is a simple middleware that uses `routeName` as the screen name for tracking screens.

```javascript
import SegmentIO from 'react-native-segment-io-analytics';

const navigationStateKey = 'navigation';

// gets the current screen from navigation state
function getCurrentScreen(getStateFn) {
  const navigationState = getStateFn()[navigationStateKey];
  // navigationState can be null when exnav is initializing
  if (!navigationState) return null;

  const { currentNavigatorUID, navigators } = navigationState;
  if (!currentNavigatorUID) return null;

  const { index, routes } = navigators[currentNavigatorUID];
  const { routeName } = routes[index];
  return routeName;
}

const screenTracking = ({ getState }) => next => action => {
  if (!action.type.startsWith('EX_NAVIGATION')) return next(action);
  const currentScreen = getCurrentScreen(getState);
  const result = next(action);
  const nextScreen = getCurrentScreen(getState);
  if (nextScreen !== currentScreen) {
    SegmentIO.screen(nextScreen);
  }
  return result;
}

export default screenTracking;

```

by @chirag04
