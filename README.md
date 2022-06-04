# React-native-modal
The goal of react-native-modal is expanding the original React Native &lt;Modal> component by adding animations, style customization options, and new features, while still providing a simple API.

# Demo

<p align="center">
<img src="https://raw.githubusercontent.com/react-native-modal/react-native-modal/master/.github/images/example-modal.gif" height="500" />
</p>

## Installation

```bash
npm i react-native-modal
```

# Example

```javascript

import React, { Component } from 'react';
import { Text, TouchableOpacity, StyleSheet, View } from 'react-native';
import Modal from 'react-native-modal';

export default class Example extends Component {
  state = {
    visibleModal: null,
  };

  _renderButton = (text, onPress) => (
    <TouchableOpacity onPress={onPress}>
      <View style={styles.button}>
        <Text>{text}</Text>
      </View>
    </TouchableOpacity>
  );

  _renderModalContent = () => (
    <View style={styles.modalContent}>
      <Text>You Clicked On Modal !</Text>
      {this._renderButton('Close', () => this.setState({ visibleModal: null }))}
    </View>
  );

  render() {
    return (
      <View style={styles.container}>
        {this._renderButton('Default modal', () => this.setState({ visibleModal: 1 }))}
        {this._renderButton('Sliding from the sides', () => this.setState({ visibleModal: 2 }))}
        {this._renderButton('A slower modal', () => this.setState({ visibleModal: 3 }))}
        {this._renderButton('Full Screen modal!', () => this.setState({ visibleModal: 4 }))}
        {this._renderButton('Bottom half modal', () => this.setState({ visibleModal: 5 }))}
        
        <Modal isVisible={this.state.visibleModal === 1}>
          {this._renderModalContent()}
        </Modal>

        <Modal
          isVisible={this.state.visibleModal === 2}
          animationIn={'slideInLeft'}
          animationOut={'slideOutRight'}
        >
          {this._renderModalContent()}
        </Modal>

        <Modal
          isVisible={this.state.visibleModal === 3}
          animationInTiming={2000}
          animationOutTiming={2000}
        >
          {this._renderModalContent()}
        </Modal>

        <Modal
          isVisible={this.state.visibleModal === 4}
          backdropColor={'lightgreen'}
          animationIn={'zoomInDown'}
          animationOut={'zoomOutUp'}
          animationInTiming={1000}
          animationOutTiming={1000}
        >
          {this._renderModalContent()}
        </Modal>

        <Modal 
        isVisible={this.state.visibleModal === 5} 
        style={styles.bottomModal}
        >
          {this._renderModalContent()}
        </Modal>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  button: {
    backgroundColor: 'lightblue',
    padding: 12,
    margin: 16,
    justifyContent: 'center',
    alignItems: 'center',
    borderRadius: 4,
  },
  modalContent: {
    backgroundColor: 'white',
    padding: 22,
    justifyContent: 'center',
    alignItems: 'center',
    borderRadius: 4,
  },
  bottomModal: {
    justifyContent: 'flex-end',
    margin: 0,
  },
});

```


For a more complex example take a look at the `/example` directory.

## Available props

| Name                             | Type                 | Default                        | Description                                                                                                                                |
| -------------------------------- | -------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `animationIn`                    | `string` or `object` | `"slideInUp"`                    | Modal show animation                                                                                                                       |
| `animationInTiming`              | `number`             | `300`                            | Timing for the modal show animation (in ms)                                                                                                |
| `animationOut`                   | `string` or `object` | `"slideOutDown"`                 | Modal hide animation                                                                                                                       |
| `animationOutTiming`             | `number`             | `300`                            | Timing for the modal hide animation (in ms)                                                                                                |
| `avoidKeyboard`                  | `bool`               | `false`                          | Move the modal up if the keyboard is open                                                                                                  |
| `coverScreen`                    | `bool`               | `true`                           | Will use RN `Modal` component to cover the entire screen wherever the modal is mounted in the component hierarchy                          |
| `hasBackdrop`                    | `bool`               | `true`                           | Render the backdrop                                                                                                                        |
| `backdropColor`                  | `string`             | `"black"`                        | The backdrop background color                                                                                                              |
| `backdropOpacity`                | `number`             | `0.70`                           | The backdrop opacity when the modal is visible                                                                                             |
| `backdropTransitionInTiming`     | `number`             | `300`                            | The backdrop show timing (in ms)                                                                                                           |
| `backdropTransitionOutTiming`    | `number`             | `300`                            | The backdrop hide timing (in ms)                                                                                                           |
| `customBackdrop`                 | `node`               | `null`                           | The custom backdrop element                                                                                                                |
| `children`                       | `node`               | **REQUIRED**                   | The modal content                                                                                                                          |
| `deviceHeight`                   | `number`             | `null`                           | Device height (useful on devices that can hide the navigation bar)                                                                         |
| `deviceWidth`                    | `number`             | `null`                           | Device width (useful on devices that can hide the navigation bar)                                                                          |
| `isVisible`                      | `bool`               | **REQUIRED**                   | Show the modal?                                                                                                                            |
| `onBackButtonPress`              | `func`               | `() => null`                     | Called when the Android back button is pressed                                                                                             |
| `onBackdropPress`                | `func`               | `() => null`                     | Called when the backdrop is pressed                                                                                                        |
| `onModalWillHide`                | `func`               | `() => null`                     | Called before the modal hide animation begins                                                                                              |
| `onModalHide`                    | `func`               | `() => null`                     | Called when the modal is completely hidden                                                                                                 |
| `onModalWillShow`                | `func`               | `() => null`                     | Called before the modal show animation begins                                                                                              |
| `onModalShow`                    | `func`               | `() => null`                     | Called when the modal is completely visible                                                                                                |
| `onSwipeStart`                   | `func`               | `() => null`                     | Called when the swipe action started                                                                                                       |
| `onSwipeMove`                    | `func`               | `(percentageShown) => null`      | Called on each swipe event                                                                                                                 |
| `onSwipeComplete`                | `func`               | `({ swipingDirection }) => null` | Called when the `swipeThreshold` has been reached                                                                                          |
| `onSwipeCancel`                  | `func`               | `() => null`                     | Called when the `swipeThreshold` has not been reached                                                                                      |
| `panResponderThreshold`          | `number`             | `4`                              | The threshold for when the panResponder should pick up swipe events                                                                        |
| `scrollOffset`                   | `number`             | `0`                              | When > 0, disables swipe-to-close, in order to implement scrollable content                                                                |
| `scrollOffsetMax`                | `number`             | `0`                              | Used to implement overscroll feel when content is scrollable. See `/example` directory                                                     |
| `scrollTo`                       | `func`               | `null`                           | Used to implement scrollable modal. See `/example` directory for reference on how to use it                                                |
| `scrollHorizontal`               | `bool`               | `false`                          | Set to true if your scrollView is horizontal (for a correct scroll handling)                                                               |
| `swipeThreshold`                 | `number`             | `100`                            | Swiping threshold that when reached calls `onSwipeComplete`                                                                                |
| `swipeDirection`                 | `string` or `array`  | `null`                           | Defines the direction where the modal can be swiped. Can be 'up', 'down', 'left, or 'right', or a combination of them like `['up','down']` |
| `useNativeDriver`                | `bool`               | `false`                          | Defines if animations should use native driver                                                                                             |
| `useNativeDriverForBackdrop`     | `bool`               | `null`                           | Defines if animations for backdrop should use native driver (to avoid flashing on android)                                                 |
| `hideModalContentWhileAnimating` | `bool`               | `false`                          | Enhances the performance by hiding the modal content until the animations complete                                                         |
| `propagateSwipe`                 | `bool` or `func`     | `false`                          | Allows swipe events to propagate to children components (eg a ScrollView inside a modal)                                                   |
| `style`                          | `any`                | `null`                           | Style applied to the modal                                                                                                                 |
