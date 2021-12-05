[![codecov](https://img.shields.io/codecov/c/github/GSingh01/ad-b2c-react-native)](https://codecov.io/gh/GSingh01/ad-b2c-react-native)

React Native Azure AD B2C solution using Pure JS. If you are using expo you dont need to eject.

Thanks to https://github.com/sonyarouje/react-native-ad-b2c and https://github.com/wkh237/react-native-azure-ad packages for the inspiration.

Feel free to contribute or sponsor. :)

## Installation

> Don't forget to **install peer dependencies** "react": "^16.8.3", "react-native-webview": "^7.0.1"

```
yarn add vindicce-b2c-react-native
```

## Usage

> The **code** below is just **a sample implementation** to just demonstrate the API of the components. As-Is **copy paste** of below **will not work**.

### Login screen

```
import React from 'react';
import { Alert } from 'react-native';
import { LoginView } from 'ad-b2c-react-native';
import * as SecureStore from 'expo-secure-store';

export default class Login extends React.PureComponent {
  static navigationOptions = { header: null };

  constructor(props) {
    super(props);
    this.onLogin = this.onLogin.bind(this);
    this.onFail = this.onFail.bind(this);
    this.spinner = this.spinner.bind(this);
  }

  onLogin() {
    const { navigation } = this.props;
    navigation.navigate('App');
  }

  onFail(reason) {
    Alert.alert(reason);
  }

  spinner() {
  //this is just a sample implementation, so copy pasting will not work as the components used below are custom
  //and are not in imports above. Please replace it with your implementation.
  return (
        <CView> //custom wrapper around View
            <Spinner /> //component wrapping loading status symbol(e.g spinner)
        </CView>
    );
  }

  render() {
      //apart from these props you can use any webview props

      //for *secureStore*, you can pass expo's secure store or create your own wrapper,
      //which implements deleteItemAsync(key), getItemAsync(key), setItemAsync(key, data)

      //*scope is optional*,if provided will overwrite the default scope {appId offline_access}
      //*Suggestion*: with custom scope, id and refresh tokens will not be returned,
      //so consider using format 'openid offline_access {your scope} '

    return (
      <LoginView
        appId="myAppId"
        redirectURI="myRedirectURI"
        tenant="myTenant"
        loginPolicy="B2C_1_SignUpSignIn"
        passwordResetPolicy="B2C_1_PasswordReset"
        profileEditPolicy="B2C_1_ProfileEdit"
        onSuccess={this.onLogin}
        onFail={this.onFail}
        secureStore={MySecureStore}
        renderLoading={this.spinner}
        scope="openid offline_access myScope1 myScope2 ...." //optional, but see the notes above
      />
    );
  }
}

```
