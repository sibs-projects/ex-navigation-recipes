# How to communicate between navigationBar and your component?

You can use `EventEmitter`

``` jsx
class MyComp extends Component {
  static route = {
    navigationBar: {
      title: 'title',
      renderLeft: (state: ExNavigationState) => {
        const { config: { eventEmitter }  } = state;

        return (
          <TextMenuButton
            tintColor={state.getBarTintColor()}
            onPress={() => eventEmitter.emit('cancel')}
          >
            Cancel
          </TextMenuButton>
        )
      },
      renderRight: (state: ExNavigationState) => {
        const { config: { eventEmitter }  } = state;

        return (
          <TextMenuButton
            tintColor={state.getBarTintColor()}
            onPress={() => eventEmitter.emit('done')}
          >
            Done
          </TextMenuButton>
        );
      },
    },
    styles: {
      ...NavigationStyles.SlideVertical,
      gestures: null,
    },
  };

  _subscriptionDone: EventSubscription;
  _subscriptionCancel: EventSubscription;

  componentWillMount() {
    this._subscriptionDone = this.props.route.getEventEmitter().addListener('done', this._handleDone);
    this._subscriptionCancel = this.props.route.getEventEmitter().addListener('cancel', this._handleCancel);
  }

  componentWillUnmount() {
    this._subscriptionDone.remove();
    this._subscriptionCancel.remove();
  }

  _handleDone = () => {
    this.props.navigator.pop();
  }

  _handleCancel = () => {
    this.props.navigator.pop();
  }
}
```
