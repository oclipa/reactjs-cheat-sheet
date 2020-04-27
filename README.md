<div style="display: inline-block;">
<a class="link" href="http://oclipa.github.io/">&lt; home</a>
<a class="link" href="http://oclipa.github.io/toolbox.html">&lt; toolbox</a>
</div> 

## ReactJS

**Recommended Course: [React - The Complete Guide (incl Hooks, React Router, Redux)](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)**

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
   * Each componenets should only have a render() method (since it is static).
   * Generally, build bottom-up (i.e. low level of heirarchy first) and write tests as you build.
   * Data will be input as a `prop` into the top of the hierarchy.
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

https://github.com/reactjs/react-future/tree/master/07%20-%20Returning%20State

</div>
</div>
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

### Class Component

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
* As a general of thumb, class components are preferred if you need fine-grained control of state, or of actions performed outside of render().

</div>
</div>
<div>
<button type="button" class="collapsible">+ Arrow Functions</button>   
<div class="content" style="display: none;" markdown="1">

* See: https://medium.com/@jacobworrel/es6-arrow-functions-what-not-to-do-c28c96b4f396
* See lecture 14

</div>
</div>
<div>
<button type="button" class="collapsible">+ let, const and var</button>   
<div class="content" style="display: none;" markdown="1">

* See lecture 13
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
