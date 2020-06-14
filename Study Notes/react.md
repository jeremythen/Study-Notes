npx create-react-app todo // npx is first used to create the project.

npm install bootstrap@4.1.2

npm start // starts the application

npm run build // production builds the application

npm start

---

Components are the main building
block for React applications, and they are written using JSX, which is a superset of JavaScript that allows
HTML to be included in code files without requiring any special quoting.

---

<select value={this.state.value} onChange={this.handleChange}> // use value when an option is selected for select elements

---

const OtherComponent = React.lazy(() => import('./OtherComponent'));

--

// This Suspense component will show Loading... until the OtherComponent is ready

import React, { Suspense, lazy, Component } from 'react';

const Home = lazy(() => import('./routes/Home'));

<Suspense fallback={<div>Loading...</div>}>
    <OtherComponent />
</Suspense>

---

Overriding these methods on any React component will make that component a ErrorBoundary:

static getDerivedStateFromError() {

}

componentDidCatch(errorparam1, errorparam2) {
console.log('in componentDidCatch', a, b, c);
}

---

HOC -> Higher-order components
Is a function that receives a component and returns another component, enhanced.
Whereas a component transforms props into UI, a higher-order component transforms a component into another component.

---

componentDidUpdate(prevProps) {...

---


Components can be passed as a parameter and received in a variable with different name:
Which is a pure function, it should not have any side effects.

function getIt(AnyComponent) {
    return class extends React.Component {
        ...

        render() {
            return <AnyComponent ...>
        }
    }...
}

getIt(MyComponent)..
getIt(OtherComponent)...

---

Rest operator on object distructoring creates a new object with the remaining properties of the old object.
const { extraProp, ...passThroughProps } = this.props;

---
Components can have a displayName property that is used for debuging with React Devtools

MyComponent.displayName = 'Whateter display message or name';

---

React’s diffing algorithm (called reconciliation)

---

React.forwardRef(function(props, ref) {
    return <AComponent {...props} forwaredRef={ref} />
});

---

Conversely, if you want a value like false, true, null, or undefined to appear in the output, you have to convert it to a string first:

<div>
  My JavaScript variable is {String(myVariable)}.
</div>

---

If your project is built with Create React App, run:

npm run build

---

Portals:

render() {
  // React does *not* create a new div. It renders the children into `domNode`.
  // `domNode` is any valid DOM node, regardless of its location in the DOM.
  return ReactDOM.createPortal(
    this.props.children,
    domNode
  );
}

---

Profiles to check with React Devtools the performance of the app.

<Profiler id="Navigation" onRender={callback}>
    <Navigation {...props} />
</Profiler>

---

defaultProps is used to assign default props to use like {this.props.myProp1}:

MyComponent.defaultProps = {
  myProp1: 'This is my prop 1'
}

---

Render props.
Any prop function that is used in the render method of a component to call that function and determine what will be rendered:

<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>

class DataProvided...
render() {
    return this.props.render();
}
--

Mouse.propTypes = {
  children: PropTypes.func.isRequired
};

---

React.PureComponent



---

Computed values:

{
    [name]: name
}

---

```javascript
this.input = React.createRef();

<input type="text" ref={this.input} />

this.input.current.value
```

```javascript
this.input = null;

<input type="text" ref={input => this.input = input } />

this.input.value
```
---

Use defaultValue="The value" instead of value="The value" for uncontrolled component.


# The component Lifecycle

## Mounting

```javascript
constructor()
static getDerivedStateFromProps() // old: componentWillReceiveProps. getDerivedStateFromProps(props, state)
// componentWillMount, legacy. getDerivedStateFromProps is the new thing.
render()
* render() will not be invoked if shouldComponentUpdate() returns false.
```

componentDidMount()

## Updating

```javascript
static getDerivedStateFromProps() // old: componentWillReceiveProps
shouldComponentUpdate() // shouldComponentUpdate(nextProps, nextState)
render()
getSnapshotBeforeUpdate() // getSnapshotBeforeUpdate(prevProps, prevState). Any value returned by this lifecycle will be passed as a parameter to componentDidUpdate().
componentDidUpdate() // componentDidUpdate(prevProps, prevState, snapshot). (don't forget to compare props, in a conditional do any setState, etc., or you’ll cause an infinite loop.):
```

## Unmounting

```javascript
componentWillUnmount() // You should not call setState() in componentWillUnmount() because the component will never be re-rendered.
```
## Error handling

```javascript
static getDerivedstateFromError()
componentDidCatch()
```
---

# States:

## setState()

```javascript

this.setState((state, props) => {
  return {counter: state.counter + props.step, callback};
});

```

setState() does not always immediately update the component. It may batch or defer the update until later. This makes reading this.state right after calling setState() a potential pitfall. Instead, use componentDidUpdate or a setState callback (setState(updater, callback)), either of which are guaranteed to fire after the update has been applied.

If the next state depends on the current state, we recommend using the updater function form, instead:

```javascript
this.setState((state) => {
  return {quantity: state.quantity + 1};
});
```

React may batch multiple setState() calls into a single update for performance.

## forceUpdate()

Calling forceUpdate() will cause render() to be called on the component, skipping shouldComponentUpdate(). 


---

# Class Properties

defaultProps

```javascript
CustomButton.defaultProps = {
  color: 'blue'
};
```

displayName

```javascript
CustomButton.displayName = 'Whatever name I want';
```

# Portals

Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component. 
Event though portals may render in a different DOM element than where it is being called, it will still depend on it's actual parent. Will have event bubbling the same.

```javascript
render() {
    return ReactDOM.createPortal(
      this.props.children,
      this.el
    );
  }
```



# Notes

When implementing the constructor for a React.Component subclass, you should call super(props) before any other statement. Otherwise, this.props will be undefined in the constructor, which can lead to bugs.

You should not call setState() in the constructor().

Avoid copying props into state! This is a common mistake.
Only use this pattern if you intentionally want to ignore prop updates. In that case, it makes sense to rename the prop to be called initialColor or defaultColor. You can then force a component to “reset” its internal state by changing its key when necessary.

getDerivedStateFromProps exists for only one purpose. It enables a component to update its internal state as the result of changes in props.
```javascript
componentWillReceiveProps(nextProps) {
    // This will erase any local state updates!
    // Do not do this.
    this.setState({ email: nextProps.email });
}

// static getDerivedStateFromProps(props, state) {

```

componentDidMount()
This method is a good place to set up any subscriptions. If you do that, don’t forget to unsubscribe in componentWillUnmount().


---
getSnapshotBeforeUpdate() is invoked right before the most recently rendered output is committed to e.g. the DOM. It enables your component to capture some information from the DOM (e.g. scroll position) before it is potentially changed. Any value returned by this lifecycle will be passed as a parameter to componentDidUpdate().

```javascript
getSnapshotBeforeUpdate(prevProps, prevState) {
    // Are we adding new items to the list?
    // Capture the scroll position so we can adjust scroll later.
    if (prevProps.list.length < this.props.list.length) {
      const list = this.listRef.current;
      return list.scrollHeight - list.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // If we have a snapshot value, we've just added new items.
    // Adjust scroll so these new items don't push the old ones out of view.
    // (snapshot here is the value returned from getSnapshotBeforeUpdate)
    if (snapshot !== null) {
      const list = this.listRef.current;
      list.scrollTop = list.scrollHeight - snapshot;
    }
  }

  ```

 # Recursing On Children

Bad

<ul>
  <li>first</li>
  <li>second</li>
</ul>
// Inserting new element at the beginning without keys, inefficient.
<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>

Good

<ul>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>
// Inserting new element at the beginning without keys, efficient.
<ul>
  <li key="2014">Connecticut</li>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>

---

Code-Splitting

```javascript

import("./math").then(math => {
  console.log(math.add(16, 26));
});


```

React.lazy

```javascript

const OtherComponent = React.lazy(() => import('./OtherComponent'));

```

Suspense

```javascript
import React, { Suspense, lazy } from 'react';


 <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Switch>
        <Route exact path="/" component={Home}/>
        <Route path="/about" component={About}/>
      </Switch>
    </Suspense>
  </Router>

```

Named Exports 

```javascript
import React, { lazy } from 'react';
const MyComponent = lazy(() => import("./MyComponent.js"));
```

# Context

```javascript

const ThemeContext = React.createContext('light');

  const ThemeContext = React.createContext('light');

class App extends React.Component {
  render() {
    // Use a Provider to pass the current theme to the tree below.
    // Any component can read it, no matter how deep it is.
    // In this example, we're passing "dark" as the current value.
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

// A component in the middle doesn't have to
// pass the theme down explicitly anymore.
function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  // Assign a contextType to read the current theme context.
  // React will find the closest theme Provider above and use its value.
  // In this example, the current theme is "dark".
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;
  }
}


```

# Forwarding Refs

The second ref argument only exists when you define a component with React.forwardRef call. Regular function or class components don’t receive the ref argument, and ref is not available in props either.
Ref forwarding is not limited to DOM components. You can forward refs to class component instances, too

```javascript
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// You can now get a ref directly to the DOM button:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

# Higher-Order Component

```javascript
Concretely, a higher-order component is a function that takes a component and returns a new component.

const CommentListWithSubscription = withSubscription(
  CommentList,
  (DataSource) => DataSource.getComments()
);

const BlogPostWithSubscription = withSubscription(
  BlogPost,
  (DataSource, props) => DataSource.getBlogPost(props.id)
);


function withSubscription(WrappedComponent, selectData) {
  // ...and returns another component...
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.handleChange = this.handleChange.bind(this);
      this.state = {
        data: selectData(DataSource, props)
      };
    }

    componentDidMount() {
      // ... that takes care of the subscription...
      DataSource.addChangeListener(this.handleChange);
    }

    componentWillUnmount() {
      DataSource.removeChangeListener(this.handleChange);
    }

    handleChange() {
      this.setState({
        data: selectData(DataSource, this.props)
      });
    }

    render() {
      // ... and renders the wrapped component with the fresh data!
      // Notice that we pass through any additional props
      return <WrappedComponent data={this.state.data} {...this.props} />;
    }
  };
}
```

---


# Render Props

```javascript
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>


class Cat extends React.Component {
  render() {
    const mouse = this.props.mouse;
    return (
      <img src="/cat.jpg" style={{ position: 'absolute', left: mouse.x, top: mouse.y }} />
    );
  }
}

class Mouse extends React.Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove(event) {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100vh' }} onMouseMove={this.handleMouseMove}>

        {/*
          Instead of providing a static representation of what <Mouse> renders,
          use the `render` prop to dynamically determine what to render.
        */}
        {this.props.render(this.state)}
      </div>
    );
  }
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>
        <Mouse render={mouse => (
          <Cat mouse={mouse} />
        )}/>
      </div>
    );
  }
}


```


# Typechecking With PropTypes

```javascript
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```


