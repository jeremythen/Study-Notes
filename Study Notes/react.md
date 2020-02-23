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




