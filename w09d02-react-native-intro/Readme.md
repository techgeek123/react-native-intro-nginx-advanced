# Introduction to React-Native 

## Learning Competencies
At the end of this chapter you will be knowing about

- What is React Native
- Setting up React Native
- Styling React-Native applications
- Async in React-Native
- Creating your first React-Native application


## Overview

### Setting up React Native environment

Assuming that you have Node installed, you can use npm to install the `create-react-native-app` command line utility:

`npm install -g create-react-native-app`

Then run the following commands to create a new React Native project called "AwesomeProject":

`create-react-native-app AwesomeProject`

`cd AwesomeProject`

`npm start`

Checkout this [link](https://habiletechnologies.com/blog/getting-started-react-native-complete-setup-guide/) for complete setup guide

## What is React Native ?

React Native is like React, but it uses native components instead of web components as building blocks. It is a framework for building cross platform mobile apps with the help of Javascript and the React library. So rather than building an android app in java or an iOS app in swift/objective C one can build an app in Native which will be compatible to both platforms and bring great features of the web to mobile

For example given below is the code for an app which says "Hello world!"

```js
import React, { Component } from 'react';
import { Text } from 'react-native';

export default class HelloWorldApp extends Component {
  render() {
    return (
      <Text>Hello world!<Text>
    );
  }
}

```

JSX lets you write your markup language inside code. It looks like HTML on the web, except instead of web things like `<div>` or `<span>`, you use React components. In this case, `<Text>` is a built-in component that just displays some text.

The above code is defining `HelloWorldApp`, which is a new Component. When you're building a React Native app, you'll be making new components a lot.A component can be pretty simple - the only thing that's required is a render function which returns some JSX to render.

The data inside React Components is managed by state and props.

## States and props

Remember that state is mutable while props are immutable. This means that state can be updated in the future while props cannot be updated.

### Using state

This is our root component. We are just importing Home which will be used in most of the chapters.

**Note** : This file won't change during the course of this tutorial, so we will leave it out in the future.

```js
index.js

import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';
import Home from './src/components/home/Home.js'

class reactTutorialApp extends Component {
   render() {
      return (
         <View>
            <Home />
         <View>
      );
   }
}
export default reactTutorialApp

AppRegistry.registerComponent('reactTutorialApp', () ⇒ reactTutorialApp);
```

Initial state is defined inside the Home class by using the `state = {}` syntax.

We will bind myText in a view using the `{this.state.myText}` syntax.

```js
src/components/home/Home.js

import React, { Component } from 'react';
import { Text, View } from 'react-native';

class Home extends Component {
   state = {
      myText: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit 
               sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
               Ut enim ad   minim veniam, quis nostrud  exercitation ullamco laboris 
               nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in
               reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
               Excepteur sint occaecat cupidatat non proident, sunt in culpa qui 
               officia deserunt mollit anim id est laborum.'
   }
   render() {
      return (
         <View>
            <Text>
               {this.state.myText}
            </Text>
         </View>
      );
   }
}
export default Home;

```

Since state is mutable, we can update it by creating the `updateState` function and call it using the `onPress = {this.updateText}` event.

```js

updateState = () ⇒ this.setState({ myState: 'The state is updated' })

render() {
      return (
         <View>
            <Text onPress = {this.updateState}>
               {this.state.myState}
            </Text>
         </View>
      );
   }
```

### Container Component and Presentational Component

Presentational components should get all data by passing props. Only container components should have state.

#### Container Component

Now we will update our container component. This component will handle the state and pass the props to the presentational component.

Container component is only used for handling state. All functionality related to view(styling etc.) will be handled in the presentational component.

**Example**

If we want to use example from the last chapter we need to remove the `Text` element from the render function since this element is used for presenting text to the users. This should be inside the presentational component.

Let us review the code in the example given below. We will import the `PresentationalComponent` and pass it to the render function.

After we import the `PresentationalComponent` and pass it to the render function, we need to pass the props. We will pass the props by adding `myText = {this.state.myText}` and `updateText = {this.updateText}` to `<PresentationalComponent>`. Now, we will be able to access this inside the presentational component.

```js
src/components/home/Home.js

import React, { Component } from 'react'
import { View } from 'react-native'
import PresentationalComponent from './PresentationalComponent'

class Home extends Component {
   state = {
      myState: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit,
         sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
         Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi
         ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in
         voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur 
         sint occaecat cupidatat non proident, sunt in culpa qui officia 
         deserunt mollit anim id est laborum.'
   }
   updateState = () ⇒ {
      this.setState({ myState: 'The state is updated' })
   }
   render() {
      return (
         <View>
            <PresentationalComponent myState = {this.state.myState} updateState = {this.updateState}/>
         <View>
      )
   }
}
export default Home
```

#### Presentational Component

Presentational components should be used only for presenting view to the users. These components do not have state. They receive all data and functions as props.

The best practice is to use as much presentational components as possible.

**Example**: 

Our component will receive props, return view elements, present text using `{props.myText}` and call the `{props.updateText}` function when a user clicks on the text.

```js
src/components/home/PresentationalComponent.js

import React, { Component } from 'react'
import { Text, View } from 'react-native'

const PresentationalComponent = (props) ⇒ {
   return (
      <View>
         <Text onPress = {props.updateState}>
            {props.myState}
         </Text>
      </View>
   )
}
export default PresentationalComponent
```

Now, we have the same functionality as in our State chapter. The only difference is that we refactored our code to the container and the presentational component.

You can run the app and see the text

**Note**: In generally we will use class syntax for stateful (container) components and function syntax for stateless (presentational) components.

## Styling

There are a couple of ways to style your elements in React Native.

You can use the `style` property to add the **styles inline**. However, this is not the best practice because it can be hard to read the code.

In this chapter, we will use the **Stylesheet** for styling.

Import the `StyleSheet` and at the bottom of the file, we will create our stylesheet and assign it to the `styles` constant. Note that our `styles` are in camelCase and we do not use px or % for styling

To apply styles to our text, we need to add `style = {styles.myText}` property to the `Text` element.

```js
src/components/home/PresentationalComponent.js

import React, { Component } from 'react'
import { Text, View, StyleSheet } from 'react-native'

const PresentationalComponent = (props) ⇒ {
   return (
      <View>
         <Text style = {styles.myState}>
            {props.myState}
         </Text>
      </View>
   )
}
export default PresentationalComponent

const styles = StyleSheet.create ({
   myState: {
      marginTop: 20,
      textAlign: 'center',
      color: 'blue',
      fontWeight: 'bold',
      fontSize: 20
   }
})
```

### TextInput in React-Native

we will see how to work with TextInput elements in React Native.

The Home component will import and render inputs.

```js
src/components/home/Home.js

import React from 'react';
import Inputs from './Inputs.js'

const Home = () ⇒ {
   return (
      <Inputs />
   )
}
export default Home
```

### Inputs

We will define the initial state. After defining the initial state, we will create the handleEmail and the handlePassword functions. These functions are used for updating state.

The login() function will just alert the current value of the state.

We will also add some other properties to text inputs to disable auto capitalisation, remove the bottom border on Android devices and set a placeholder.

```js
src/components/home/Inputs.js

import React, { Component } from 'react'
import { View, Text, TouchableOpacity, TextInput, StyleSheet } from 'react-native'

class Inputs extends Component {
   state = {
      email: '',
      password: ''
   }
   handleEmail = (text) ⇒ {
      this.setState({ email: text })
   }
   handlePassword = (text) ⇒ {
      this.setState({ password: text })
   }
   login = (email, pass) ⇒ {
      alert('email: ' + email + ' password: ' + pass)
   }
   render(){
      return (
         <View style = {styles.container}>
            <TextInput style = {styles.input}
               underlineColorAndroid = "transparent"
               placeholder = "Email"
               placeholderTextColor = "#9a73ef"
               autoCapitalize = "none"
               onChangeText = {this.handleEmail}/>
            
            <TextInput style = {styles.input}
               underlineColorAndroid = "transparent"
               placeholder = "Password"
               placeholderTextColor = "#9a73ef"
               autoCapitalize = "none"
               onChangeText = {this.handlePassword}/>
               
            <TouchableOpacity
               style = {styles.submitButton}
               onPress = {
                  () ⇒ this.login(this.state.email, this.state.password)
               }>
               <Text style = {styles.submitButtonText}> Submit </Text>
            <TouchableOpacity>
         </View>
      )
   }
}
export default Inputs

const styles = StyleSheet.create({
   container: {
      paddingTop: 23
   },
   input: {
      margin: 15,
      height: 40,
      borderColor: '#7a42f4',
      borderWidth: 1
   },
   submitButton: {
      backgroundColor: '#7a42f4',
      padding: 10,
      margin: 15,
      height: 40,
   },
   submitButtonText:{
      color: 'white'
   }
})
```

Whenever we type in one of the input fields, the state will be updated. When we click on the Submit button, text from inputs will be shown inside the dialog box.

## Async in React-Native

we will see how to use `fetch` for handling network requests.

```js
src/components/home/Home.js

import React from 'react';
import HttpExample from './HttpExample.js'

const Home = () ⇒ {
   return (
      <HttpExample />
   )
}
export default Home
```

### Using Fetch

We will use the `componentDidMount` lifecycle method to load the data from server as soon as the component is mounted. This function will send `GET` request to the server, return JSON data, log output to console and update our state.

```js
src/components/home/HttpExample.js

import React, { Component } from 'react'
import { View, Text } from 'react-native'

class HttpExample extends Component {
   state = {
      data: ''
   }
   componentDidMount = () ⇒ {
      fetch('https://jsonplaceholder.typicode.com/posts/1', {
         method: 'GET'
      })
      .then((response) ⇒ response.json())
      .then((responseJson) ⇒ {
         console.log(responseJson);
         
         this.setState({
            data: responseJson
         })
      })
      .catch((error) ⇒ {
         console.error(error);
      });
   }
   render() {
      return (
         <View>
            <Text>
               {this.state.data.body}
            </Text>
         </View>
      )
   }
}
export default HttpExample
```

## Exploration
- React Native official [doc](https://facebook.github.io/react-native/docs/getting-started.html)
- Create react app using [Expo](https://expo.io/learn)
- React-Native [video tutorial](https://www.youtube.com/watch?v=3Pm5_Cf7pQI)
