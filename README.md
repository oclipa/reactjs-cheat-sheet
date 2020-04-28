<div style="display: inline-block;">
<a class="link" href="http://oclipa.github.io/">&lt; home</a>
<a class="link" href="http://oclipa.github.io/toolbox.html">&lt; toolbox</a>
</div> 

## ReactJS

**Recommended Course:**
   * **[React - The Complete Guide (incl Hooks, React Router, Redux)](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)**

-------

<div>
<button type="button" class="collapsible">+ How To Approach Building An App In React</button>
<div class="content" style="display: none;" markdown="1">

**Based on: [https://reactjs.org/docs/thinking-in-react.html](https://reactjs.org/docs/thinking-in-react.html)**

1. Break data model into components that (ideally) only do one thing.
   * [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle)
1. Break down UI into components, where each component matches one piece of the data model.
1. Arranage UI components into a hierarchy.
1. Build a static version of the hierarchy in React.
   * At this stage, use `props` rather than `state` (see "[What is the difference between state and props](https://reactjs.org/docs/faq-state.html#what-is-the-difference-between-state-and-props)").
   * Each component should only have a render() method (since it is static).
   * Generally, build bottom-up (i.e. low level of heirarchy first) and write tests as you build.
   * Data will be input as a `prop` into the top of the hierarchy, e.g. in index.js:
      * `ReactDOM.render(<App data="dataSource" />, document.getElementById('root'));`
1. Identify the minimum set of mutable (i.e. changeable) state required by the app.
   * [Don't Repeat Yourself Principle](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
   * e.g. it is good for state to reference an array, but not the number of items in the array.
   * Three questions:
      * Is it passed in from a parent via props? If so, it probably isn’t state.
      * Does it remain unchanged over time? If so, it probably isn’t state.
      * Can you compute it based on any other state or props in your component? If so, it isn’t state.
1. Identify which component mutates, or owns, the state.
   * For each piece of state in your application:
      * Identify every component that renders something based on that state.
      * Find a common owner component (a single component above all the components that need the state in the hierarchy).
      * Either the common owner or another component higher up in the hierarchy should own the state.
      * If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common owner component.
   * The owner of the `state` will pass it to components that need it via `props`. 
   * Components that mutate state should avoid UI rendering.
1. Add inverse data flow (i.e. from lower hierarchy to higher).
   * Components should only update their own state.
   * Pass callbacks (e.g. `onChange` event) from higher components to lower components, which will fire when the state should be updated.  
   * The callbacks will call `setState()`.

</div>
</div>
<div>
<button type="button" class="collapsible">+ React Design Principles</button>
<div class="content" style="display: none;" markdown="1">

**Based on: [https://reactjs.org/docs/design-principles.html](https://reactjs.org/docs/design-principles.html)**

1. The key feature of React is composition of components.
   * Components should be able to be changed without affecting the rest of the codebase.
   * Components describe any composable behaviour, which includes rendering, lifecycle and state.
1. Resist adding features that can be implemented by clients.
   * [Minimal API Surface Area](https://www.youtube.com/watch?v=4anAwXYqLG8)
   * Only add out-of-scope features if it will avoid clients producing multiple solutions to the same problem.
1. Before deprecating a feature, always consider all use cases and communicate reasons and alternatives to clients.
1. If some pattern is hard to express in a declarative way, provide an imperative API.
1. If you can't identify a perfect API, provide a temporary subpar API (but it must be temporary).
1. Value API stability.
   * When something changes, there should be a clear (and preferably automated) migration path.
   * Deprecate APIs internally first, before deprecating them for clients (to allow validation).
   * Add deprecation warnings in the current major version and change the behaviour in the following major release.
   * Consider using [codemod](https://www.youtube.com/watch?v=d0pOgY8__JM) scripts for changes that require a lot of repetitive manual work.
1. Value interoperability.
   * Enable gradual adoption by allowing existing functionality to be wrapped by new functionality.
1. Perform the minimum amount of work before returning to React.
   * Allows React to schedule and split work.
1. Be renderer-agnostic
   * Don't assume the app will only run in a browser.
   * e.g. [https://reactnative.dev](React Native)
1. Aim for elegant APIs but prefer ugly APIs if they avoid work for the client.
   * Correct, performant and a good developer experience are more important than elegant.
1. Prefer boring code to clever code.
   * Avoid new internal abstractions.
   * Verbose code is easier to move around and change.
1. Use verbose name for APIs.
   * Make points of interaction highly visible and distinct.
   * Optimize for search (makes automated updates easier).
1. [Eat Your Own Dog Food](https://en.wikipedia.org/wiki/Eating_your_own_dog_food)
   * But be open to the idea that external clients may have other use cases.

</div>
</div>
<div>
<button type="button" class="collapsible">+ React Patterns</button>
<div class="content" style="display: none;" markdown="1">

* Stateful Functions
* Module Pattern
* Default Props and Initial State
   * Specify default values for `props` with `defaultProps`.
```
function Greeting(props) {
  return <div>Hi {props.name}!</div>;
}
Greeting.defaultProps = {
  name: "Guest"
};
```

* Data-Down, Actions-Up
* Higher-Order Component
* Container Components
* Callback Chaining
* Async Sequence
https://github.com/reactjs/react-future/tree/master/07%20-%20Returning%20State

</div>
</div>
<div>
<button type="button" class="collapsible">+ Best Practices List</button>   
<div class="content" style="display: none;" markdown="1">

**Taken from [https://medium.com/@konstankino/2019-reactjs-best-practices-design-patterns-516e1c3ca06a](https://medium.com/@konstankino/2019-reactjs-best-practices-design-patterns-516e1c3ca06a)**

* When using ReduxJS, split your Reducer code into smaller methods to avoid huge JSON within your Reducer.
* Consider using TypeScript in your apps if you do not do it already.
* Use the create-react-app generator to bootstrap your ReactJS app.
* Keep your code DRY. Don’t Repeat Yourself, but keep in mind code duplicate is NOT always a bad thing.
* Avoid having large classes, methods or components, including Reducers.
* Use more robust managers to manage application state, such as Redux.
* Use event synchronizer, such as Redux-Thunk, for interactions with your back end API.
* Avoid passing too many attributes or arguments. Limit yourself to five props that you pass into your component.
* Use ReactJS defaultProps and ReactJS propTypes.
* Use linter, break up lines that are too long.
* Keep your own jslint configuration file.
* Always use a dependency manager with a lock file, such as NPM or yarn.
* Test your commonly accessed code, code that is complex and prone to bugs.
* Write more tests that give more test coverage for your code with a little effort and test code to ensure its proper functioning.
* Every time you find a bug, make sure you write a test first.
* Use function-based components by starting to use React Hooks, a new ReactJS way to create state-full components.
* Use ES6 de-structuring for your props.
* Use conditional rendering.
* User `map()` to collect and render collections of components.
* Use partial components, such as `<>` … `</>`
* Name your event handlers with handle prefixes, such as `handleClick()` or `handleUpdate()`.
* Use `onChange` to control your inputs, such as `onChange={this.handleInputChange}`.
* Use JEST to test your ReactJS code.

</div>
</div>

-------

<div>
<button type="button" class="collapsible">+ Setup Basic Environment</button>
<div class="content" style="display: none;" markdown="1">

1. Install NodeJs: 
   * [https://nodejs.org](https://nodejs.org)
2. Install create-react-app: 
   * `sudo npm install create-react-app -g`
3. Create a new app: 
   * `create-react-app [app-name] [--scripts-version version]`
   * This will create a new sub-directory of the current directory called `app-name`.
   * `--scripts-version version` is optional; if not used, the latest version of create-react-app will be used.
4. In the new app directory, start the development server: 
   * `npm start"
   * This actually calls a bespoke command defined in package.json.

</div>
</div>
<div>  
<button type="button" class="collapsible">+ Example of a Simple App</button> 
<div class="content" style="display: none;" markdown="1">

### index.js 

**(boiler-plate code generated by create-react-app)**

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();

```

### App.js 

**(created from template generated by create-react-app)**

```jsx
// imports ////////////////////////////////////////////////////

import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import './App.css';
import Calculator from './Calculator/Calculator.js';

// App class //////////////////////////////////////////////////

class App extends Component {
  
  // application state ////////////////////////////////////////

  state = {
    algName: 'None',
    val1: 0,
    val2: 0
  };
  
  // event handlers and functions /////////////////////////////

  val1ChangedHandler = ( event ) => {
    this.setState( 
        {
          algName: "None",
          val1: event.target.value
        } 
      );
  };

  val2ChangedHandler = ( event ) => {
    this.setState( 
        {
          algName: "None",
          val2: event.target.value
        } 
      );
  };
  
  doCalculationHandler = ( event ) => {
    this.setState( 
        {
          algName: event.target.value
        } 
      );
  };

  // render ////////////////////////////////////////////////////

  render() {
    // local style /////////////////////////////////////////////
    const style = {
      backgroundColor: 'green',
      color: 'white',
      font: 'inherit',
      border: '1px solid blue',
      padding: '8px',
      cursor: 'pointer'
    };
    
    let a = this.state.algName;
    let v1 = this.state.val1;
    let v2 = this.state.val2;

    let calc = (<Calculator algName={a} val1={v1} val2={v2} />);

    return (
      <div className="App"> {/* required */} 
        <div className="inputs">
            <input type="text" 
                    onChange={(event) => 
                                this.val1ChangedHandler(event)} 
                    value={v1} />
            
            <input type="text" 
                    onChange={(event) => 
                                this.val2ChangedHandler(event)} 
                    value={v2} />
            
            <div className = "buttons">
              <button style={style} 
                      onClick={(event) => 
                                this.doCalculationHandler(event)}
                      value="add">Add</button>
              <button style={style} 
                      onClick={(event) => 
                                this.doCalculationHandler(event)}
                      value="subtract">Subtract</button>
            </div>
        </div>
        <div className="output">
          {calc}
        </div>
      </div>
    );
  }
}

export default App;
```

### Calculator/Calculator.js

**(created manually)**

```jsx
import React from 'react';
import './Calculator.css';

const calculator = (props) => {
    
    const algName = props.algName;
    const val1 = parseFloat(props.val1);
    const val2 = parseFloat(props.val2);
    
    let result = 0;
    
    if (algName === 'add') {
      result = val1 + val2;
    }
    else if (algName === 'subtract') {
      result = val1 - val2;
    }
    else if (algName === 'None') {
      return <span></span>
    }
    
    return (
        <span>Result = {result}</span>
    )
};

export default calculator;
```
</div>
</div>
<div>
<button type="button" class="collapsible">+ Functional vs Class Components</button>   
<div class="content" style="display: none;" markdown="1">

**Both Functional and Class components should start with an uppercase letter**

### Functional Component

```jsx
// ES5
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// ES6
const Welcome = (props) => {
  return <h1>Hello, {props.name}</h1>;
}
```

* Functional components do not access props via `this`(e.g. `props.XY`).

Pros:

* Functional components are generally considered easier to read and test.
* Code tends to be smaller.
* It is easier to separate container and presentational components.
* There may be a performance boost in future React versions.

Cons:

* You cannot call setState() in a functional component.
   * As of React 16.8, you can use useState() but this only allows you to overwrite the state, rather than merging updates into the existing state.
* You cannot use lifecycle hooks in a functional component.
   * As of React 16.8, you can use useEffect() however this is not as fine-grained as lifecycle hooks.
   * useEffect() allows you to perform an action after render() has been called.

**useEffect**

* `import React, {useEffect} from 'react';`
* Takes a function that will run for every render cycle.
  * `useEffect( () => { somefunction; }); )`
* Can have multiple calls to useEffect in the same function (e.g. each reacting to different object).
* Essentially, componentDidMount and componentDidUpdate combined in one effect (see below).
* Controlled by passing an object (or array of objects) into the method and the method only reacts if the object has changed:
  * `useEffect( () => { somefunction; }, [props.somedata] ); )`
  * To have the method run only the first time an object is rendered, pass an empty array.
* To perform clean-up using useEffect, return a function:
  * `useEffect( () => { somefunction; }, [props.somedata] ); return () => { cleanupfunction } )`
  * Runs BEFORE the main useEffect function runs, but AFTER the (first) render cycle.


### Class Component

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
} 
```

* Class components must access state and props using `this`(e.g. `this.state.XY`).

* As a general of thumb, class components are preferred if you need fine-grained control of state, or you need actions performed outside of render() and you do not want to use React Hooks.

**Class Component LifeCycle**

1. This is only available to Class components.
1. Lifecycle Hooks have nothing to do with React Hooks!

<img src="assets/reactjs-component-lifecycle.png" />

<br/>[Original Image](https://twitter.com/dan_abramov/status/981712092611989509/photo/1)
&copy; Dan Abramov: [https://overreacted.io/](https://overreacted.io/)
<br/>[Interactive Version](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

* Mounting
   1. `constructor()`
      * Call super(props)
      * Use to set up state
      * Don't cause Side-Effects
   1. `getDerivedStateFromProps(props, state)`
      * Sync state with props
      * Very niche case
      * Don't cause Side-Effects
   1. `render()`
      * Prepare and Structure your JSX code
      * Don't do any actions that will block the rendering process.
      * Only completes after render() has been called for all children.
   1. `componentDidMount()` &lt;-- Commonly used
      * Very common 
      * Can cause Side-Effects (e.g. send http requests)
      * Don't update state (at least, not synchronously)
   1. `componentWillMount()`
      * Available but deprecated
      * Do not use

* Updating
   1. `getDerivedStateFromProps(props, state)`
      * See above
   1. `componentWillReceiveProps(props)`
      * Available but deprecated
      * Do not use
   1. `shouldComponentUpdate(nextProps, nextState)` &lt;-- Commonly used
      * Used to cancel update process
      * Typically used for performance reasons (if used carefully)
   1. `render()`
      * See above
   1. `getSnapshotBeforeUpdate(prevProps, prevState)`
      * Another niche method
      * Last minute DOM operations (e.g. getting current scrolling position of user)
      * Don't cause Side-Effects
   1. `componentWillUpdate()`
      * Available but deprecated
      * Do not use
   1. `componentDidUpdate()` &lt;-- Commonly used
      * Can cause Side-Effects (e.g. send http requests)
      * Don't update state (at least, not synchronously)

* Unmounting (clean-up)
   * `componentWillUnmount()
   
* Other 
   * componentDidCatch()

</div>
</div>

<div>
<button type="button" class="collapsible">+ var, let and const</button>   
<div class="content" style="display: none;" markdown="1">

`var`- creates a variable; doesn't differentiate between variables and constants.

`let`- is basically the same as `var`; use this if a variable is actually variable.

`const`- use this if a variable never changes (i.e. is constant).

With the release of ES6, avoid using `var`.

</div>
</div>

<div>
<button type="button" class="collapsible">+ Arrow Functions</button>   
<div class="content" style="display: none;" markdown="1">

"Traditional" Function (ES5):

```
function myFunc() {
  console.log(arguments);
  return ...
}
```

Arrow Function (ES6):

```
const myFunc = (args) => ({
  console.log(args);
  ...
})
```

Differences:
* Arrow functions avoid problems with `this` keyword (always refers to the enclosing context).
* Arrow functions have an implict return, so the `return` keyword does not need to be used, however the the function block must be wrapped in parantheses (if nothing is being returned, the parantheses can be left out).
* Arrow functions cannot be [hoisted](https://www.w3schools.com/js/js_hoisting.asp), unlike the ES5 function.
* Arguments must be explicitly passed into arrow functions (the `arguments` object is only available to ES5 functions).
* Cannot use arrow functions as constructors or methods (see below).

Digression: **What is the difference between a method and a function?**
The difference between a method and a function (in javascript) is that: 
   * functions are called in isolation (e.g. `someFunction()`)
   * methods are only called from other objects (e.g. `someObject.someFunction()`)
e.g.
```
    var object = {
      myMethod: function() {
        console.log("Am I still a method?");
      }
    };
    object.myMethod();          // this is a method call
    var myFunc = object.myMethod; 
    myFunc();                   // this is now a function call
```
For those coming from languages such as C#, it may be better to think of functions as private and methods as public.
</div>
</div>

<div>
<button type="button" class="collapsible">+ Spread and Rest Operators</button>   
<div class="content" style="display: none;" markdown="1">

* See lecture 18
</div>
</div>
<div>
<button type="button" class="collapsible">+ Destructuring</button>   
<div class="content" style="display: none;" markdown="1">

* See lecture 19

The [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

```
let a, b, rest;
[a, b] = [10, 20];

console.log(a);
// expected output: 10

console.log(b);
// expected output: 20

[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// expected output: Array [30,40,50]
```

The following component declarations are equivalent:

```
function Greeting(props) {
  return <div>Hi {props.name}!</div>;
}

function Greeting({ name }) {
  return <div>Hi {name}!</div>;
}
```

The following is an example [Rest Parameter Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters), which collects remaining props into an object:

```
function Greeting({ name, ...restProps }) {
  return <div>Hi {name}!</div>;
}
```

</div>
</div>
<div>
<button type="button" class="collapsible">+ Array Functions</button>   
<div class="content" style="display: none;" markdown="1">

* map()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
* find()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find
* findIndex()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex
* filter()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
* reduce()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b
* concat()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b
* slice()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice
* splice()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice

</div>
</div>
<div>
<button type="button" class="collapsible">+ Iterating Over Lists</button>   
<div class="content" style="display: none;" markdown="1">

* map()
* Spread Operator

</div>
</div>
<div>
<button type="button" class="collapsible">+ Props & State</button>   
<div class="content" style="display: none;" markdown="1">

* props
   * props are read-only
* setState()
   * [Beware: React setState is asynchronous!](https://medium.com/@wereHamster/beware-react-setstate-is-asynchronous-ce87ef1a9cf3)
   * https://reactjs.org/docs/react-component.html#setstate
* useState() - see lecture 44
</div>
</div>
<div>
<button type="button" class="collapsible">+ Two-Way Binding</button>   
<div class="content" style="display: none;" markdown="1">

* See lecture 47
</div>
</div>
<div>
<button type="button" class="collapsible">+ Styling</button>   
<div class="content" style="display: none;" markdown="1">

* Inline - lecture 49
* Stylesheets - lecture 48
* Dynamic - lecture 66 and 67
* Radium - lecture 68 and 69
   * `npm install radium`
* styled-components - lecture 70, 71 and 72
   * https://styled-components.com/
   * `npm install styled-components`
   * `import styled from 'styled-components'`
   * ```const Button = styled.button`[css]` ```
      * tagged template literals: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates 
   * All styled methods return a React component
* CSS modules
   * See lecture 73, 74 and 75
   * Also: https://stackoverflow.com/questions/50234890/how-to-use-css-modules-with-create-react-app
</div>
</div>
<div>
<button type="button" class="collapsible">+ Using Conditionals</button>   
<div class="content" style="display: none;" markdown="1">
  
* See lecture 53
</div>
</div>
<div>
<button type="button" class="collapsible">+ Debugging</button>   
<div class="content" style="display: none;" markdown="1">

* Simplest: Use Chrome Developer Tools (OPTION + CMD + i)
   * Can combine with React Developer Tools Extension: [https://chrome.google.com/webstore/search/react%20developer%20tools?hl=en](https://chrome.google.com/webstore/search/react%20developer%20tools?hl=en)
* Alternatively, use the "Debugger for Chrome" extension in Visual Studio Code.
</div>
</div>
<div>
<button type="button" class="collapsible">+ Error Handling</button>   
<div class="content" style="display: none;" markdown="1">

Use the ErrorBoundary component to catch errors thrown by components.
   * Caveat: ErrorBoundary does not work in event handlers; in this case use try/catch

```jsx
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = {
      hasError: false,
      errorMessage: ''  
    }
  }

  // can be used for both client- and server-side
  // is called in "render phase" when the DOM has not yet been updated
  // should be used for rendering a fallback UI
  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }
  
  // can only be used on the client-side
  // is called during the "commit phase" when the DOM has already been updated
  // should be used for something like error reporting
  componentDidCatch = (error, errorInfo) => {
    this.setState({hasError: true, errorMessage: error});
    //logComponentStackToMyService(errorInfo.componentStack);
  }
  
  render() {
    if (this.state.hasError) {
      return <h1>{this.state.errorMessage}</h1>;
    }

    return this.props.children;
  }
}

export default ErrorBoundary;
```

Usage:

```
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

For imperative code, use try/catch:

```jsx
try {
  showButton();
} catch (error) {
  // ...
}
```
</div>
</div>

&nbsp;

&nbsp;

&nbsp;

------
**Move along; nothing to see here...**

<script type="text/javascript">

    function loadCSS(filename){ 

       var file = document.createElement("link");
       file.setAttribute("rel", "stylesheet");
       file.setAttribute("type", "text/css");
       file.setAttribute("href", filename);
       document.head.appendChild(file);
    }

    //just call a function to load your CSS
    //this path should be relative your HTML location
    loadCSS("../collapse.css");

    var coll = document.getElementsByClassName("collapsible");
    var i;

    for (i = 0; i < coll.length; i++) {
      coll[i].addEventListener("click", function() {
        this.classList.toggle("active");
        var content = this.nextElementSibling;
        if (content.style.display === "block") {
          content.style.display = "none";
        } else {
          content.style.display = "block";
        }
      });
    }

</script>
