
AppRegistry is used to let React Native know which is the main view.
```javascript
import { AppRegistry } from 'react-native';
AppRegistry.registerComponent('ColorList', () => App);
```

For stateless component, use Functional components. Even though you pass props to it, if it doesn't use it's own state, it doesn't have it.


This way, if onSelect function is not passed, an anonymous function is asigned to it that doesn't do anything, so it doesn't break the code trying to execute the onSelect function.
```javascript...
```


```html
<StatusBar hidden={true} />
```

borderWidth: StyleSheet.hairlineWidth;


## Add multiple styles to one component

```html
<Text style={[styles.style1, styles.style2]} />
```

# Flex

## Flex is the React Native default

justifyContent: 'center'.


You don't have to specify the flex property, but if you do, like flex: 1, then all elements are going to be affected and in this case will fill all the space.

When adding multiple styles to an element, you can set a different flex to that specific element, like flex: 2, so it grows differently than it's siblings.


### Important

* alignItems is vertical or cross axis.
* justifyContent is horizontal axis.

```javascript
{
    justifyContent: 'flex-end',
    alignItems: 'flex-end'
}
```

For a single child, you can set the alignSelf: 'center', etc., property.

# Images

You need to import images to use them:

```javascript
import pic from './assets/myPicture.png';
```

borderRadius: 50


## Dimensions

With the dimensions object, you can get the height and width of the screen and make an image take the whole screen.

```javascript
{
width: Dimensions.get('window').width,
resizeMode: 'contain'
}

```

The Image component can contain child components. <Image><Text></Text></Image>
You can treat an image component as a flex container.


# Text

You can design a Text component to look and act as a button, with the onPress, background color, etc.

For the background, you can use: backgroundColor: 'rgba(255, 255, 255, .5);


# TouchableHighlight

To create a better looking button, use this component. Put views, texts, components inside it and style it. Put it a onPress event. Put an underlayColor="yourcolor" to it so it changes when is pressed.


# ScrollView

You can replace View with ScrollView


# ListView

ListView automatically scrolls.

ListView needs DataSource to work, and uses it to make smart updates:

```javascript
this.ds = new ListView.DataSource({
    rowHasChanges: (r1, r2) => r1 !== r2
});

this.state = {
    dataSource: this.ds.cloneWithRows(data)
}


<ListView dataSource={this.state.dataSource} renderRow={(color) => (<ColorButton prop={color} 
renderHeader={() => (<Text>etc</Text>)} // The title of the ListView
/>)}>

```

When adding more elements dynamically ot the data, on setState, add both the data and the dataSource again:

this.setState({
    data,
    dataSource: this.ds.cloneWithRows(data)
})

# React.PropTypes.func.isRequired

This way, you make that onNewColor property required and of type function.

```javascript
ColorForm.propTypes = {
    onNewColor: React.PropTypes.func.isRequired
}
```

# AsyncStore

Saves data on the device.

```javascript
AsyncStorage.setItem(
    '@ColorListStore:Colors',
    JSON.stringify(colors)
);


AsyncStorage.getItem(
    '@ColorListStore:Colors',
    (err, data) => {
        if(err) {
            console.error('Error loading colors', err);

        } else {
            const data = JSON.parse(data);
            this.setState({
                data,
                dataSource...
            })
        }
    }
)


```

# Navigator

This would go in App

With the Navigator, you can go pushing component's or scenes and also pop them to go back 1.

```javascript
<Navigator
    initialRoute={{name: 'Color List'}}
    renderScene={(route, navigator) => {

        switch(route.name) {
            case 'Color Info':
                return <ColorInfo backgroundColor={route.color} onSelect={() => navigator.pop() />
            default:
                return <ColorList onColorSelected={
                    color => navigator.push({
                        name: 'Color Info',
                        color
                    })
                } />
        }


    }}
/>
```

```javascript
const App = StackNavigator({
    Home: {screen: ColorList },
    Details: { screen: ColorInfo },
    Web: { screen: WebPage }
});
```

# WebView


<WebView source={{ uri: 'https://www.google.com' }} contentInset={{ top: -650 />