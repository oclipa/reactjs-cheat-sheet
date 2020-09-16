<div style="display: inline-block;" >
<a class="link" href="http://oclipa.github.io/">&lt; home</a>
<a class="link" href="http://oclipa.github.io/toolbox.html">&lt; toolbox</a>
</div> 

## React

**Recommended Course:**
   * **[React - The Complete Guide (incl Hooks, React Router, Redux)](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)**

-------------------------------------------------------------------------------------------------------

<button type="button" id="toggle-all" value="none">Expand All Sections</button>

-------------------------------------------------------------------------------------------------------

<div id="howto">
<button type="button" class="collapsible">+ Theory</button>
<div class="content" style="display: none;" markdown="1">
  
<div id="howto">
<button type="button" class="collapsible">+ How To Approach Building An App In React</button>
<div class="content" style="display: none;" markdown="1">

**Based on: [https://reactjs.org/docs/thinking-in-react.html](https://reactjs.org/docs/thinking-in-react.html)**

1. Break data model into components that (ideally) only do one thing.
   * [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle)
1. Break down UI into components, where each component matches one piece of the data model.
1. Arrange UI components into a hierarchy.
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

<div id="design">
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
1. If some pattern is hard to express in a declarative way ("I want a table for two"), provide an imperative API ("Go to restaurant, speak to waiter, etc.)").
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

<div id="patterns">
<button type="button" class="collapsible">+ React Patterns</button>
<div class="content" style="display: none;" markdown="1">

There are many patterns that are considered important for React; certainly too many to list here.  

A good sources of information about React Patterns is:
   * [https://vasanthk.gitbooks.io/react-bits/](https://vasanthk.gitbooks.io/react-bits/)

Additional information can be found here:
   * [https://reactpatterns.com/](https://reactpatterns.com/)

Some examples of common patterns can be found here:
   * [https://github.com/reactjs/react-future/tree/master/07%20-%20Returning%20State](https://github.com/reactjs/react-future/tree/master/07%20-%20Returning%20State)

</div>
</div>

<div id="practices">
<button type="button" class="collapsible">+ Best Practices List (WIP)</button>   
<div class="content" style="display: none;" markdown="1">

**Taken from [https://medium.com/@konstankino/2019-reactjs-best-practices-design-patterns-516e1c3ca06a](https://medium.com/@konstankino/2019-reactjs-best-practices-design-patterns-516e1c3ca06a)**

* When using ReduxJS, split your Reducer code into smaller methods to avoid huge JSON within your Reducer.
* Consider using TypeScript in your apps if you do not do it already.
* Use the create-react-app generator to bootstrap your React app.
* Keep your code DRY. Don’t Repeat Yourself, but keep in mind code duplicate is NOT always a bad thing.
* Avoid having large classes, methods or components, including Reducers.
* Use more robust managers to manage application state, such as Redux.
* Use event synchronizer, such as Redux-Thunk, for interactions with your back end API.
* Avoid passing too many attributes or arguments. Limit yourself to five props that you pass into your component.
* Use React defaultProps and React propTypes.
* Use linter, break up lines that are too long.
* Keep your own jslint configuration file.
* Always use a dependency manager with a lock file, such as NPM or yarn.
* Test your commonly accessed code, code that is complex and prone to bugs.
* Write more tests that give more test coverage for your code with a little effort and test code to ensure its proper functioning.
* Every time you find a bug, make sure you write a test first.
* Use function-based components by starting to use React Hooks, a new React way to create state-full components.
* Use ES6 de-structuring for your props.
* Use conditional rendering.
* User `map()` to collect and render collections of components.
* Use partial components, such as `<>` … `</>`
* Name your event handlers with handle prefixes, such as `handleClick()` or `handleUpdate()`.
* Use `onChange` to control your inputs, such as `onChange={this.handleInputChange}`.
* Use JEST to test your React code.

</div>
</div>

</div>
</div>

------------------------------------------------------------------------------------------------------

<div id="in-practice">
<button type="button" class="collapsible">+ Basics</button>
<div class="content" style="display: none;" markdown="1">
  
<div id="nodejs">
<button type="button" class="collapsible">+ Using NodeJS and create-react-app</button>
<div class="content" style="display: none;" markdown="1">

1. To install NodeJS:
   * Either, download the installer from the NodeJS website: [https://nodejs.org](https://nodejs.org)
   * Or, if using MacOS, install using HomeBrew: `brew install node`
   * Or, if using Zsh on Unbuntu (if using Bash, just replace `zsh` with `bash` and `.zshrc` with `.bash_profile`):
      1. `sudo apt-get update`
      1. `sudo apt-get upgrade`
      1. `sudo apt-get install build-essential`
      1. `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | zsh`
      1. Restart prompt (if there problems are reported with .bashrc, check the permissions on .bashrc)
      1. `nvm install --lts`
      1. `nvm use --lts`
      1. `echo "nvm use --silent --lts" >> .zshrc`
      
1. Install create-react-app (might not need `sudo`): 
   * `[sudo] npm install create-react-app -g`
1. Create a new app: 
   * `create-react-app [app-name] [--scripts-version version]`
   * This will create a new sub-directory of the current directory called `app-name`.
   * `--scripts-version version` is optional; if not used, the latest version of create-react-app will be used.
1. Install an existing app (which has an existing package.json file): 
   * In the app root folder run: `npm install`
1. In the new app directory, start the development server: 
   * `npm start`
   * This actually calls a bespoke command defined in package.json.

</div>
</div>

<div id="npm">
<button type="button" class="collapsible">+ Popular NPM Packages</button>   
<div class="content" style="display: none;" markdown="1">

**Globally Installed**

* `[sudo] npm install create-react-app -g`
  * Command-line tool that creates the basic framework for a React app.
* `[sudo] npm install yarn -g`
  * Yarn is an alternative to npm.
* `npm install firebase-tools -g`
   * If using Google Firebase

**Locally Installed Production (i.e. per project; required for production)**

* `npm install prop-types`
   * Enables use of PropTypes for validation of properties
* `npm install radium`
   * Uses an HOC that can be used to style components.
   * Requires pseudo-CSS for inline CSS (the same as standard React).
* `npm install styled-components`
   * Uses tagged template literals to style components.
   * Allows inline CSS to be specified as normal (rather than in the pseudo-CSS required by standard React or Radium).
   * Doesn't really allow a clear separation between style and logic.
* `npm install axios`
   * This is a promise-based HTTP client.
* `npm install react-router-dom`
   * Enables routing
* `npm install redux`
   * Enables enhanced state management
* `npm install react-redux`
   * Allows Redux store to be hooked up to React application
* `npm install redux-thunk`
   * Enables both complex synchronous logic and simple asynchronous logic when accessing a Redux store.
* `npm install firebase`
   * Enables access to Google's Firebase database.
* `npm install gh-pages`
   * If deploying to GitHub Pages

**Locally Installed Development (i.e. per project; only required for development)**
* `npm install eslint --save-dev`
   * Linting tool for javascript
   * NOTE: this is included as a dependency of `create-react-app` and so can be skipped if CRA is installed.
* `npm install prettier --save-dev`
   * Code formatter
* `npm install eslint-config-prettier --save-dev`
   * Allows ESLine and Prettier to work together
* `npm install jest --save-dev `
   * Enables unit tests to be run.
   * NOTE: this is included as a dependency of `create-react-app` and so can be skipped if CRA is installed.
* `npm install enzyme react-test-renderer enzyme-adapter-react-16 --save-dev`
   * Enables unit testing of React components

</div>
</div>

<div id="simple-app">  
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

<div id="dom">
<button type="button" class="collapsible">+ Virtual DOM</button>   
<div class="content" style="display: none;" markdown="1">

It is important to note that, when render() is called for an app (or a functional component returns), React creates a Virtual DOM ([Domain Object Model](https://www.w3schools.com/whatis/whatis_htmldom.asp)); it does not automatically update the real DOM (i.e. the UI).  This is for performance reasons (updating the real DOM is potentially expensive).

Once generated, the new Virtual DOM is compared to the previous Virtual DOM to see if anything has changed.  In the event something has changed, the real DOM is updated with the changes in the new Virtual DOM, and the UI redrawn.  If nothing has changed, the UI is not updated.
</div>
</div>
  
<div id="func-components">
<button type="button" class="collapsible">+ Functional Components</button>   
<div class="content" style="display: none;" markdown="1">

* Functional component names should start with an uppercase letter.
* Functional components should be used if the component is not stateful.

**Basic Implementation**

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

**Details**

* Functional components do not access props via `this`(e.g. `props.XY`).

Pros:

* Functional components are generally considered easier to read and test.
* Code tends to be smaller.
* It is easier to separate container and presentational components.
* There may be a performance boost in future React versions.

Cons:

* You cannot call `setState()` in a functional component.
   * As of React 16.8, you can use the `useState()` hook but this only allows you to overwrite the state, rather than merging updates into the existing state.
* You cannot use lifecycle hooks in a functional component.
   * As of React 16.8, you can use the `useEffect()` hook, however this is not as fine-grained as lifecycle hooks.
   * `useEffect()` allows you to perform an action after render() has been called.

See the React Hooks section, below, for further information.

</div>
</div>
  
<div id="class-components">
<button type="button" class="collapsible">+ Class Components</button>   
<div class="content" style="display: none;" markdown="1">

* Class component names should start with an uppercase letter.
* Class components should be used if the component is stateful, or there is a need to use lifecycle methods (e.g. `componentDidMount()`).

**Basic Implementation**

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
} 
```

**Details**

* Class components must access state and props using `this`(e.g. `this.state.XY`).
* As a general rule of thumb, class components are preferred if you need fine-grained control of state, or you need actions performed outside of render() and you do not want to use React Hooks.

**Class Component LifeCycle**

1. This is only available to Class components.
1. Lifecycle Hooks have nothing to do with React Hooks!

<a href="assets/reactjs-component-lifecycle.png" target="_blank"><img src="assets/reactjs-component-lifecycle.png" style="width: 100%"/></a>

<br/>[Original Image](https://twitter.com/dan_abramov/status/981712092611989509/photo/1)
&copy; Dan Abramov: [https://overreacted.io/](https://overreacted.io/)
<br/>[Interactive Version](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

* **Mounting**
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
      * **Only called when a component is first mounted; use `componentDidUpdate()` if component is already displayed**
   1. `componentWillMount()`
      * Available but deprecated
      * Do not use

* **Updating**
   1. `getDerivedStateFromProps(props, state)`
      * See above
   1. `componentWillReceiveProps(props)`
      * Available but deprecated
      * Do not use
   1. `shouldComponentUpdate(nextProps, nextState)` &lt;-- Commonly used
      * Used to cancel update process (even if Virtual DOM changes)
      * Typically used for performance reasons, but needs to be used sparingly.
      * e.g. `return nextProps.property !== this.props.property`
      * For a functional equivalent to this, see [React.memo()](https://reactjs.org/docs/react-api.html#reactmemo).
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
      * **Only called when a component is already displayed; use `componentDidMount()` if component is not yet displayed**

* **Unmounting (clean-up)**
   * `componentWillUnmount()`
   
* **Other**
   * `componentDidCatch()`

</div>
</div>

<div id="pure">
<button type="button" class="collapsible">+ Pure Components</button>   
<div class="content" style="display: none;" markdown="1">

* A [`PureComponent`](https://reactjs.org/docs/react-api.html#reactpurecomponent) is essentially the same as a `Component` except that it checks to see if either the props or state has changed before allowing the Virtual DOM to be updated. 
   * i.e. This is a replacement for `shouldComponentUpdate()` (which will ignored for a `PureComponent`).
   * Note that all children must extend `PureComponent`.

```jsx
import React, { PureComponent } from 'react';

class App extends PureComponent {
  
  ...
  
  render() {
    ...
  };
}
```
</div>
</div>

<div id="adjacent">
<button type="button" class="collapsible">+ Adjacent Elements</button>   
<div class="content" style="display: none;" markdown="1">

The `render()` method does not allow adjacent elements (i.e. ones with the same root) to be returned, e.g.

```jsx
return (
    <p onClick={
      this.props.click
    }>
      I'm {this.props.name} and 
      I am {this.props.age} years old!
    </p>
    <p>{this.props.children}</p>
    <input 
      type="text" 
      onChange={this.props.changed} 
      value={this.props.name} 
    />
)
```
There are several ways around this:

**Use a Root Element**

```jsx
return (
    <div>
      <p onClick={
        this.props.click
      }>
        I'm {this.props.name} and 
        I am {this.props.age} years old!
      </p>
      <p>{this.props.children}</p>
      <input 
        type="text" 
        onChange={this.props.changed} 
        value={this.props.name} 
      />
    </div>
)
```

**Use Square Brackets**

* In this case, essentially you are returning an array, which means the elements need to be delimited by commas.  
* Also, a `key` needs to be specified for each element.

```jsx
return (
    [
      <p key="i1" onClick={
        this.props.click
      }>
        I'm {this.props.name} and 
        I am {this.props.age} years old!
      </p>
      <p key="i2">{this.props.children}</p>
      <input
        key="i3"
        type="text" 
        onChange={this.props.changed} 
        value={this.props.name} 
      />
    ]
)
```

**Use a Wrapper/Aux Function**

In some places this function is referred to as `Aux`, however this is a reserved word on Windows and should be avoided (unless you can guarantee that Windows will never be used for development).

*Wrapper.js*

```jsx
import React from 'react';

const wrapper = props => props.children;

export default wrapper;
```

*Person.js*

```jsx
import Wrapper from '../../../hoc/Wrapper';

...

render() {
  return (
      <Wrapper>
        <p onClick={
          this.props.click
        }>
          I'm {this.props.name} and 
          I am {this.props.age} years old!
        </p>
        <p>{this.props.children}</p>
        <input 
          type="text" 
          onChange={this.props.changed} 
          value={this.props.name} 
        />
      </Wrapper>
  );
}
```

**Use React.Fragment**

Since React 16.8, there is a built-in version of `Wrapper` called `React.Fragment`:

*Person.js*

```jsx
import React, { Component, Fragment } 
        from 'react';
...

render() {
  return (
      <Fragment>
        <p onClick={
          this.props.click
        }>
          I'm {this.props.name} and 
          I am {this.props.age} years old!
        </p>
        <p>{this.props.children}</p>
        <input 
          type="text" 
          onChange={this.props.changed} 
          value={this.props.name} 
        />
      </Fragment>
  );
}
```
</div>
</div>

<div id="hoc">
<button type="button" class="collapsible">+ Higher Order Components (HOC)</button>   
<div class="content" style="display: none;" markdown="1">

The `Wrapper`and `Fragment` components are examples of Higher Order Components.  This means that they wrap another component and add specific, limited functionality to the wrapped component.

There is a general convention to name HOCs with a `With` at the beginning, and place them in an `hoc` folder.

There are two approaches to defining HOCs:

**Return a JSX Functional Component**

* In this case, the HOC typically wraps group of elements rendered by a component.
* This approach is recommended when changing the HTML code or styling.

*hoc/WithClass.js (upper-case 'W' to indicate this is a component, not function)*

```jsx
import React from 'react';

const WithClass = props => (
  <div className={props.classes}>
    {props.children}
  </div>
);

export default WithClass;

```

*containers/App.js*

```jsx
import React from 'react';

// upper-case 'W' to indicate this 
// is a component, not a function
import WithClass from '../hoc/WithClass';

class App extends Component { 
  ...
 
  render() {
    return (
      <WithClass classes={styles.App}>
        ...
      </WithClass>
    );
  } 
}

export default App;
```

**Return a JS Function That Returns a JSX Functional Component**

* In this case, the HOC typically wraps a component and adds extra functionality.
* This approach is recommended for adding behind-the-scenes logic, e.g. error handling or sending analytic data.

*hoc/withClass.js (lower-case 'w' to indicate this is a function, not component)*

```jsx
import React from 'react';

const withClass = 
  (WrappedComponent, className) => {
    return props => (
      <div className={className}>
        <WrappedComponent {...props} />}
      </div>
  );
};

export default withClass;

```
*containers/App.js*

```jsx
import React from 'react';

// lower-case 'w' to indicate this 
// is a function, not component
import withClass from '../hoc/WithClass';
import Wrapper from '../hoc/Wrapper';
  
class App extends Component {
  ...
 
  render() {
    return (
      <Wrapper>
        ...
      </Wrapper>
    );
  } 
}

export default withClass(App, styles.App);
```

</div>
</div>

<div id="state">
<button type="button" class="collapsible">+ Props & State</button>   
<div class="content" style="display: none;" markdown="1">

There are two approaches to handling application state:
   * `state`
   * `props`

**state**

* `state`, as the name suggests, records the current state of a **class** component.
* Not all components need to have state (it can be maintained by a parent component).
* The `state` object is defined at the top of the class definition:

```jsx
import React, { Component } from 'react';
import Town from 'Town';

class App extends Component {
  state = {
    persons: [
      { name: 'Fred', age: 40 },
      { name: 'Wilma', age: 35 },
      { name: 'Barney', age: 38 },
    ],
    location: 'Bedrock'
  };
  
  ...
  
  render() {
    return (
      <Town
        name={this.state.location}
        persons={this.state.persons}
        clicked={this.deleteOldestHandler}
      />
    );
  }
}
```

* In class components, state should be updated using the [`setState()`](https://reactjs.org/docs/react-component.html#setstate) function; it should never be updated directly (e.g. do not use `this.state.name = newName`).
* Be aware that `setState()` is [asynchronous](https://medium.com/@wereHamster/beware-react-setstate-is-asynchronous-ce87ef1a9cf3).  Calling `setState()` should be considered a request that React may ignore.  This is particularly true if `setState()` is called multiple times in the same update cycle; later calls may overwrite earlier ones. 
* In addition, it is good practice to only ever change state properties immutably.  This can be achieved by making a copy of the property to be updated, updating the copy and then overwriting the original property, e.g.

Bearing these issues in mind, the recommended pattern is the following:

```jsx
deleteOldestHandler = () => {
  // create a copy of the person array
  // using the spread operator
  const persons = [...this.state.persons];

  // sort the array by increasing age and 
  // remove the last person
  persons.sort((a, b) => a.age - b.age).pop();
  
  // overwrite the old array with the new one.
  // also update a counter of number of people 
  // deleted.
  // prevState is guaranteed to be the latest
  // state.
  this.setState((prevState, props) => { 
    return {
      persons: persons, 
      deleteCounter: prevState.deleteCounter + 1
    };
  });
}
```

**props**

* Unlike `state`, both Class components and Functional components can access the `props` object.
   * For Class components, this is done use the `this` keyword: `persons = this.props.persons;`.
   * For Functional components, the `props` object is passed in as a function parameter: `const Town = (props) => { persons = props.persons; }`
* The `props` object is read-only.  It is created from the element properties of the component: `<Town persons={persons} />`.
* Since props cannot be updated, the only way to update the state is via callbacks passed via the `props` object.  In this way, the parent object both owns the state and is responsible for updating it.

```jsx
import React from 'react';

const Town = (props) => { 
  return (
    <div>
      <h1>Name: {props.name}</h1>
      <h1>Occupants: {props.persons.length}</h1>
      <button onClick={props.clicked}>
        Remove Oldest Person
      </button>
    </div>
  );
}

export default Town;
```

**useState()**

The `useState()` function is an example of a React Hook, which allows Functional Components to replicate and replace behaviour in Class-Based Components.

For further information, see the React Hooks section, below.

</div>
</div>

<div id="proptypes">
<button type="button" class="collapsible">+ PropTypes</button>   
<div class="content" style="display: none;" markdown="1">

PropTypes allow control of the data types used in the app (i.e. more like a strongly-typed language).  This is a feature provided by React, but it is not included in React Core, so it needs to be installed:

* Install: `npm install prop-types`
* Import: `import PropTypes from 'prop-types';`

PropTypes can be used on both class and functional components.  They are particularly important when you are sharing components with other people.

```jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class Person extends Component {
  render() {
    return (
      <Wrapper>
        <p onClick={this.props.click}>
          I'm {this.props.name} and I 
          am {this.props.age} years old!
        </p>
        <p>{this.props.children}</p>
        <input 
          type="text" 
          onChange={this.props.changed} 
          value={this.props.name} 
        />
      </Wrapper>
    ); 
  }
};

// specify prop values types after 
// component has been defined
Person.propTypes = {
  click: PropTypes.func,
  name: PropTypes.string,
  age: PropTypes.number,
  changed: PropTypes.func
};

export default withClass(Person, styles.Person);
```
</div>
</div>

<div id="refs">
<button type="button" class="collapsible">+ Refs</button>   
<div class="content" style="display: none;" markdown="1">

Refs (i.e. references) are used to accessing specific elements of the DOM.  Specifically, there are used for accessing HTML elements or class components (they cannot be used to reference functional components, although functional components can use refs via React Hooks - see below).

In the following example, a ref is added to the input element.  The ref points to a function that creates a new class property that points to the input element.

The property is the used to ensure that, when the Person components are mounted, the text field for the last Person mounted will be given the focus.

In older code, an example implementation might be:

```jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class Person extends Component {
  constructor() {
    this.inputElement = React.createRef();
  }
  
  componentDidMount() {
    this.myInputElement.focus();
  }
  
  render() {
    return (
      <Wrapper>
        ...
        
        <input 
          ref={
            (el) => {
              this.myInputElement = el
             };
          };
          type="text" 
          onChange={this.props.changed} 
          value={this.props.name} 
        />
      </Wrapper>
    ); 
  }
};
```

In newer code, an alternative approach is to create a generic ref in the constructor and then attach this to the current element of interest:

```jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class Person extends Component {
  constructor(props) {
    super(props);
    this.elementRef = React.createRef();
  }
  
  componentDidMount() {
    // current gives access to the 
    // current reference
    this.elementRef.current.focus();
  }
  
  render() {
    return (
      <Wrapper>
        ...
        
        <input 
          ref={this.elementRef}
          type="text" 
          onChange={this.props.changed} 
          value={this.props.name} 
        />
      </Wrapper>
    ); 
  }
};
```

**Refs and Functional Components**

For further information on how to refs can be emulated in functional components, see the discussion on `useRef()`, in the React Hook section below.

**Further Information*

* [https://reactjs.org/docs/refs-and-the-dom.html](https://reactjs.org/docs/refs-and-the-dom.html)

</div>
</div>

<div id="context">
<button type="button" class="collapsible">+ Context API</button>   
<div class="content" style="display: none;" markdown="1">

The Context API is used to pass state between objects when intervening objects have no interest in the state (e.g. passing a property to a great-grandchild).

First we create a globally available javascript object, e.g.:

*context/auth-context.js*

```jsx
import Read from 'react';

const authContext = React.createContext({
  auth: false, 
  login: () => {}
});

export default authContext;
```

Then, in the parent component, the components (or parents of the components) that need to receive the context are wrapped in a `<AuthContext.Provider />` element,  in the `render()` method:

*App.js*

```jsx
import AuthContext 
        from 'context/auth-context';

class App extends Component {
  constructor(props) {
    super(props);
    
    this.state = {
      persons: [
        { id: 'asfa1', name: 'Max' },
        { id: 'vasdf1', name: 'Manu' },
        { id: 'asdf11', name: 'Stephanie' }
      ],
      auth: false
    }
  }

  loginHandler = () => {
    this.setState( { auth: true } );
  };

  render() {
  
    persons = (
      <Persons 
        persons={this.state.persons}
        isAuthenticated={this.state.auth}
      />
    );
  
    return (
      <Wrapper>
        { /* components not interested in 
             context go outside tags */ }

        <AuthContext.Provider 
          value={ 
            {
              authenticated: this.state.auth, 
              login: this.loginHandler
            } 
          } 
        >
         { /* components interested in 
              context go between tags */ }
         
         <Cockpit />
         {persons}

        </AuthContext.Provider>
      </Wrapper>
    );
  }
}

```

And finally, in the components that need to access the context, the relevant elements in the `render()` method are wrapped in a `<AuthContext.Consumer />` element:

*Person.js (inherits context from Persons.js)*

```jsx
import AuthContext 
        from 'context/auth-context';

class Person extends Component {

  render() {
    return (
      <Wrapper>
        <AuthContext.Consumer>
          {(context) => {
              context.auth ? 
                <p>Authenticated!</p> : 
                <p>Please log in</p>
            }
          }
        </AuthContext.Consumer> 
        
        <p>{this.props.children}</p>
      </Wrapper>
    );
  }
}

```

*Cockpit.js*

```jsx
import AuthContext from 'context/auth-context';

const Cockpit = (props) => {

  render() {
    return (
      <Wrapper>
        <h1>{props.title}</h1>
      
        <AuthContext.Consumer>
          {(context) => {
              <button onClick={context.login}>
                Log in
              </button>
            }
          }
        </AuthContext.Consumer>
      </Wrapper>
    );
  }
}

```

**contextType (class components only)**

For class components, a more elegant approach, which also allows the context to be accessed outside of the `render()` method, can be used.

By creating a static reference to the context called `contextType` this makes the context accessible anywhere within the class using `this.context`.

*Person.js*

```jsx
import AuthContext 
        from 'context/auth-context';

class Person extends Component {

  static contextType = AuthContext;
  
  componentDidMount() {
    console.log(this.context.auth);
    console.log(this.context.login);
  }
  
  render() {
    return (
      <Wrapper>
        {
          this.context.auth ? 
            <p>Authenticated!</p> : 
            <p>Please log in</p>
        }
        
        <p>{this.props.children}</p>
      </Wrapper>
    );
  }
```

**Context and Functional Components**

For further information on how to access context in functional components, see the `useContext()` discussion, in the React Hook section below.

**Further Information**

* [https://reactjs.org/docs/context.html](https://reactjs.org/docs/context.html)

</div>
</div>

<div id="lists">
<button type="button" class="collapsible">+ Lists in JSX</button>   
<div class="content" style="display: none;" markdown="1">

List items must always have a `key` property.  Note that using `index` as the `key` is not recommended, since it is an intrinsic part of the list, rather than part of the objects in the list.

```jsx
deleteHandler = (personIndex) => {
  // create copy of array 
  // before manipulating it.
  const persons = [...this.state.persons];
  persons.splice(personIndex, 1);
  this.setState({persons: persons});
}

render() {
  // create list of persons using map()
  return this.state.persons.map(
    (person, index) => {
      return <Person 
        click={() => this.deleteHandler(index)}
        name={person.name} 
        age={person.age}
        key={person.id} />
    }
  );
}
```

</div>
</div>

<div id="conditionals">
<button type="button" class="collapsible">+ Using Conditionals In JSX</button>   
<div class="content" style="display: none;" markdown="1">

* Conditional statements take advantage of the fact that you can inject javascript into jsx using single curly braces `{}`.
* Having said that, inside jsx, only ternary expressions are available (`test ? a : b`).

```jsx
import React, { Component } from 'react';
import Town from 'Town';

class App extends Component {
  togglePersonsHandler = () => {
    const doesShow = this.state.showPersons;
    this.setState({showPersons: !doesShow});
  }

  render() {
    return (
      <div>
        { this.state.showPersons ? 
          <div>
            ...
          </div> : null
        }
      </div>
    );
  };
}
```

* Alternatively, the following is a more elegant (and recommended) approach:

```jsx
import React, { Component } from 'react';
import Town from 'Town';

class App extends Component {
  togglePersonsHandler = () => {
    const doesShow = this.state.showPersons;
    this.setState({showPersons: !doesShow});
  }

  render() {
    let persons = null;
    
    if (this.state.showPersons) {
      persons = (
          <div>
            ...
          </div> 
      )
    }
    
    return (
      <div>
        {persons}
      </div>
    );
  };
}
```

</div>
</div>

<div id="events">
<button type="button" class="collapsible">+ Events &amp; Binding</button>   
<div class="content" style="display: none;" markdown="1">

**Event Handlers**

The following is an example of a basic implementation of an event handler:

```jsx
class App extends Component {

  // naming convention: 
  // [verb] + [noun] + "Handler"
  // ([noun] + [verb] + "Handler")
  switchNameHandler = () => {
    console.log('Was clicked!');
  }
  
  render() {
    return (
      <button 
        onClick={this.switchNameHandler}>
          Switch Name
      </button>
    );
  }
}
```
Note that we only register a reference to the event handler (`this.switchNameHandler`) with the event, rather than registering it as a method (`this.switchNameHandler()`).  If it were registered as a method, it would be invoked immediately upon registration (due to the `()`), rather than waiting until the event is triggered.

If you need to pass the event handler to a child component (which is a common use case), the handler is registered as a property of the child component:

```jsx
  render() {
    return (
      <Person 
        name={this.state.persons[1].name} 
        age={this.state.persons[1].age} 
        click={this.switchNameHandler} />
    );
  }
```
If you need to pass a value to the event handler, there are two approaches:
   * The `bind()` method.
   * An anonymous function.

**`bind()` method**

By calling the `bind()` method on the handler, a value can be passed as an argument.

```jsx
switchNameHandler = (newName) => {
  this.setState( {
    persons: [
      { name: 'Fred', age: 40 },
      { name: newName, age: 35 },
      { name: 'Barney', age: 38 },
    ],
  } );
}

render() {
  return (
    <button 
      onClick={
        this.switchNameHandler.bind(
          this, 'Betty'
        )
      }>Switch Name</button>
  );
}
```

**Anonymous function**

```jsx
render() {
  return (
    <button 
      onClick={
        () => this.switchNameHandler('Betty')
      }>Switch Name</button>
  );
}
```
Note that in this case `()` must be added to the event handler, since we are registering a reference to the anonymous function, rather than the event handler itself.  This means that we can pass data to the event handler. 

Of the two approaches, **the `bind()` method is generally the most efficient**, so it is recommended to use this rather than the anonymous function.
</div>
</div>

<div id="two-way-bind">
<button type="button" class="collapsible">+ Two-Way Binding</button>   
<div class="content" style="display: none;" markdown="1">

Two-way binding means that when something in the browser changes something in the data store, that change is immediately reflected in the browser.

To achieve this, in addition to passing an event handler to the child, which allows the child to trigger an update of the state, the child also receives the updated state via `props`.

In the following example, the sequence of actions is:

1. `App` renders `Person` while passing it the `state` (via `props`) and a `nameChangedHandler` event handler. 
1. `Person` renders `props.name` and registers the `nameChangedHandler` event handler with the `onChange` event for the `<input>`field.
1. The `<input>` field in `Person` is updated by the user, triggering the `onChange` event.
1. The `nameChangedHandler` receives the updated element (i.e. `<input>`) via `event.target`, and updates the `state` with the value of `value`.
1. `App` then renders `Person` again, passing it the updated `state`.
1. `Person` renders the updated `props.name`.
1. And the cycle repeats...

*App.js*

```jsx
class App extends Component {

  nameChangedHandler = (event) => {
    this.setState( {
      persons: [
        { name: 'Fred', age: 40 },
        { name: event.target.value, age: 35 },
        { name: 'Barney', age: 38 },
      ],
    } );
  }
  
  render() {
    return (
      <Person 
        name={this.state.persons[1].name} 
        age={this.state.persons[1].age} 
        click={this.switchNameHandler}
        changed={this.nameChangedHandler} />
    );
  } 
}
```
*Person.js*

```jsx
const person = (props) => {
  return (
    <div>
      <p>{props.name}</p>
      <input 
        type="text" 
        onChange={props.changed} 
        value={props.name}/>
    </div>
  )
};
```

**Preventing Event Propagation**

To prevent an event being propagated, e.g. preventing a form a being submitted when Submit is clicked, or preventing a link being followed when the link is clicked, use `event.preventDefault()`.

For example:

```
  submitNameHandler = (event) => {
    event.preventDefault();
    // this event will not be propagated further
  };
  
  render() {
    return (
      <div>
        <form>
          <input type="text" name="name" placeholder="Your name" />
          <button onClick={this.submitNameHandler}>Submit</button>
        </form>
      </div>
    );
  }
```
</div>
</div>

<div id="css">
<button type="button" class="collapsible">+ Styling</button>   
<div class="content" style="display: none;" markdown="1">

There are several approaches to styling React pages:
   * Inline
   * Stylesheets
   * Dynamic
   * Radium
   * styled-components
   * CSS modules

**Inline**

This means that the styles are added to tags in the `render()` method using the inline `style` property.  In this case, the styles are scoped to the component.

```jsx
class App extends Component {
  render() {
    const style = {
      backgroundColor: '#fff',
      width: '60%',
      border: '1px solid #eee',
      boxShadow: '0 px 3px #ccc',
      cursor: 'pointer'
    };
    
    return (
      <div style={style}>
        ...
      </div> 
    );
  } 
}
```
Note that there are 3 differences between this approach and standard CSS syntax:
   * Hypenated names are not supported, so `background-color`becomes `backgroundColor`. 
   * Properties are separated by commas, rather than semi-colons.
   * Property values are enclosed in single quotes.

Some CSS features are quite difficult to implement using this approach (e.g. `:hover`).

**Stylesheets**

There are two important things to be aware of when using an imported stylesheet in React:
   * CSS class names for tags are identified using `className` not `class` (because "html" in React is actually JSX, where `class` already has a different meaning).
   * Imported CSS is globally scoped, so implementing a style for `button`, for example, will affect every button in the app. 

*Person.css*

```css
.Person {
  background-color: #fff;
  width: 60%;
  border: 1px solid #eee;
  box-shadow: 0 px 3px #ccc;
  cursor: pointer;
}
```
*Person.js*

```jsx
import './Person.css';

const person = (props) => {
  return (
    <div className="Person">
      ...
    </div>
  )
};
```

**Dynamic**

Dynamic-styling essentially means using JSX features to replace the style identifiers with variables that can be generated on the fly.

*App.css*

```css
.App {
  text-align: center;
}

.red {
  color: red;
}

.bold {
  font-weight: bold;
}
```
*App.js*

```jsx
class App extends Component {
  render() {
    const style = {
      backgroundColor: '#fff'
    };
    
    // dynamically change backgroundColor
    if (this.state.showPersons) {
      style.backgroundColor: 'green';
    }
    
    // dynamically change text
    const classes = [];
    if (this.state.persons.length <= 2) {
      classes.push('red'); // ['red']
    }
    if (this.state.persons.length <= 1) {
      classes.push('bold'); // ['red', 'bold']
    }
    
    return (
      <div className={classes.join(' ')}>
        <button style={style}>Click Me!</button>
        ...
      </div> 
    );
  } 
}
```

**Radium**

Radium allows inline styles to be used with pseudo-selectors and media queries. It is an example of a Higher Order Component.

* Install: `npm install radium;`
* Import: `import Radium from 'radium';`

To use Radium, wrap the component with Radium when exporting:

`export default Radium(App);`

And wrap the entire App with `<StyleRoot>` tags:

*App.js*

```jsx
import Radium, { StyleRoot } from 'radium';

class App extends Component {
  render() {
    return (
      <StyleRoot>
        <div>
          <Person />
          <Person />
          <Person />
        </div>
      </StyleRoot>
    )
  }
}
```
*Person.js*

```jsx
import Radium from 'radium';

const person = (props) => {
  const style= {
    backgroundColor: 'green',
    color: 'white',
    cursor: 'pointer',
    
    // support for :hover and 
    // @media enabled by Radium
    
    ':hover': {       
      backgroundColor: 'lightgreen'
      color: 'black'
    },
    '@media (min-width: 500px)': {
      width: '450px';
    }
  };
  
  if (props.showPersons) {
    style[':hover'] = {
      backgroundColor: 'salmon'
      color: 'black'
    };
  }
  
  return (
    <div style={style}>
      ...
    </div>
  )
};

export default Radium(Person);
```

**styled-components**

See: [https://styled-components.com/](https://styled-components.com/)

* Install: `npm install styled-components;`
* Import: `import styled from 'styled-components';`

* Syntax: ```const Button = styled.button`[css styles]`; ```

This syntax is an example of using [tagged template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates).

All styled methods return a React component.

*Person.js*

```jsx
import styled from 'styled-components';

const StyledDiv = styled.div``
  background-color: ${props => props.alt ?
                            'red' : 'green'};
  color: white;
  cursor: pointer;

  &:hover {
    background-color: lightgreen;
    color: black;
  }

  @media (min-width: 500px) {
    width: '450px';
  }
``

const person = (props) => {
  return (
    <StyledDiv alt={props.showPersons}>
      ...
    </StyledDiv>
  )
};

export default Person;
```

**CSS modules**

The advantage of CSS modules is that they allow you to put styles in CSS files but ensure they are scoped to the current component.

Assuming you are using v2 or higher of create-react-app, you basically just need to move your CSS to files with a `.module.css` extension and then import the styles as an object.

When the `.module.css` file is imported into a component, the classes are assigned random names, which means that, as long as they are accessed from the styles object, they are only accessible in the current component.

If you do want a CSS class with global scope, you can prefix it with `:global` (e.g. `:global .Post { ... }`) 

*MyComponent.module.css*

```css
.myStyle {
  color: #fff
}
```
*MyComponent.js*

```jsx
import React from 'react'
import styles from 'MyComponent.module.css'

export default () => (
  <div className={styles.myStyle}>
    We are styled!
  </div>)
```
For further details about enabling CSS modules, see here:
* [https://stackoverflow.com/questions/50234890/how-to-use-css-modules-with-create-react-app](https://stackoverflow.com/questions/50234890/how-to-use-css-modules-with-create-react-app)

For further details about CSS modules in general, see here:
* [https://github.com/css-modules/css-modules](https://github.com/css-modules/css-modules)

</div>
</div>

<div id="debug">
<button type="button" class="collapsible">+ Debugging</button>   
<div class="content" style="display: none;" markdown="1">

* Simplest: Use Chrome Developer Tools (OPTION + CMD + i)
   * Can combine with [React Developer Tools Extension] (https://chrome.google.com/webstore/search/react%20developer%20tools?hl=en)
* Alternatively, use the "Debugger for Chrome" extension in Visual Studio Code.
</div>
</div>

<div id="errors">
<button type="button" class="collapsible">+ Error Handling</button>   
<div class="content" style="display: none;" markdown="1">

**ErrorBoundary**

Use the ErrorBoundary component to catch errors thrown by components.
   * Caveat: ErrorBoundary does not work in event handlers; in this case use try/catch

```jsx
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = {
      hasError: false,
      message: ''  
    }
  }

  // Can be used for both client- and 
  // server-side.
  // Is called in "render phase" when the 
  // DOM has not yet been updated.
  // Should be used for rendering a 
  // fallback UI.
  static getDerivedStateFromError(error) {
    // Update state so the next render will 
    // show the fallback UI.
    return { hasError: true };
  }
  
  // Can only be used on the client-side.
  // Is called during the "commit phase" 
  // when the DOM has already been updated.
  // Should be used for something like 
  // error reporting.
  componentDidCatch = (error, info) => {
    this.setState(
      {
        hasError: true, 
        message: error
      }
    );
    //logStackToService(info.componentStack);
  }
  
  render() {
    if (this.state.hasError) {
      return <h1>{this.state.message}</h1>;
    }

    return this.props.children;
  }
}

export default ErrorBoundary;
```

Usage:

```html
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

&nbsp;

**try/catch**

For imperative code, use try/catch:

```jsx
try {
  showButton();
} catch (error) {
  // ...
}
```

**withErrorHandler() HOC**

For web communication using Axios, wrap the components that handle the request and response in an HOC that intercepts any errors messages and handles them appropriately:

```jsx
const withErrorHandler = (WrappedComponent, axios) => {
  return class extends Component {
    state = {
      error: null,
    };

    /* Add interceptors before component is loaded 
      (so that any errors during loading can be handled) */
    UNSAFE_componentWillMount() {
      // When a request is submitted, set the error state to null
      this.reqInterceptor = axios.interceptors.request.use((req) => {
        this.setState({ error: null });
        return req;
      });
      
      /* When a response is received and it includes an error, 
         set the error state to be the error object */
      this.resInterceptor = axios.interceptors.response.use(
        (res) => res,  // '(res) => res' indicates that 'res' should be returned
        (error) => {
          this.setState({ error: error });
        }
      );
    }

    /* Remove the interceptors when the component is destroyed,
       to avoid unnecessary handling of web communications */
    componentWillUnmount() {
      axios.interceptors.request.eject(this.reqInterceptor);
      axios.interceptors.response.eject(this.resInterceptor);
    }

    render() {
      return (
        <Wrapper>
          {/* if there is an error, display it */}
          <ErrorMessage show={this.state.error}>
            {this.state.error ? this.state.error.message : null}
          </ErrorMessage>
          
          {/* display the wrapped component */}
          <WrappedComponent {...this.props} />
        </Wrapper>
      );
    }
  };
};

export default withErrorHandler;
```

</div>
</div>

<div id="fetch">
<button type="button" class="collapsible">+ HTTP Requests with fetch</button>   
<div class="content" style="display: none;" markdown="1">

The simplest way to query a URL is the `fetch()` function, which is a feature provided by the browser, and thus does not require additional imports.  

However, to test `fetch()` outside of a browser, the `node-fetch` module can be used:

* Install: `npm i node-fetch`
* Import: `const fetch = require('node-fetch');'

In either case, the `fetch()` function returns a `Promise`.

**Usage**

In its simplest form, the syntax looks like this:

```js
fetch('https://api.kanye.rest')
  .then(response => response.json())
  .then(quote => console.log(quote));
```

By default `fetch()` performs a `GET` request, however this can overridden be passing an options object:

```js
fetch('https://api.kanye.rest', {
  method: 'POST', // 'GET', 'POST', 'PUT', 'DELETE'
  body: JSON.stringify('hello'), // request contents (if any)
  headers: { 'Content-Type': 'application/json' }, // header overrides (if any)
})
  .then(response => response.json())
  .then(quote => console.log(quote));
```

Note that, generally, the response will need to be converted to either JSON (`response.json()`) or text (`response.text()`) before is it useful.

**Query Status**

HTTP responses are identified by codes, of which 200 (success) and 404 (not found) are probably the most familiar.

Any response in the range 200-299 is identified by `response.ok` being `true`.

A more detailed response status can be seen using the following properties:
  * `response.status` - this is the familiar HTTP response code, with 200 indicating a successful query.
  * `response.statusText` - this provides an additional information about the status.

A failure to connect to the resources (for example, due to network or permission issues) will result in a `TypeError` rejection.

**Error Handling**

Errors are handled using `catch`.  An example of this is the following:

```js
fetch('notExists')
  .then(function (response) {
    if (!response.ok) {
      // one option might be to make the promise be rejected
      // by throwing an error
      // throw new Error("Not 2xx response")

      // but a more nuanced approach might be:
      switch (response.status) {
        case 404:
          throw new Error(`Not found: ${response.statusText}`);
        case 500:
          throw new Error(`Server error: ${response.statusText}`);
        default:
          throw new Error(
            `Query failed: ${response.status} - ${response.statusText}`
          );
      }
    } else {
      // go the desired response
    }
  })
  .catch((err) => {
    // some error here
    console.log(`Error: ${err}`);
  });
```

**Further Information**

For further details see:
* [https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch](Using Fetch)
* [https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch](Fetch API)

</div>
</div>

<div id="http">
<button type="button" class="collapsible">+ HTTP Requests with Axios</button>   
<div class="content" style="display: none;" markdown="1">

Axios is a promise-based HTTP client that can be integrated with React:  
   * [https://github.com/axios/axios](https://github.com/axios/axios)

* Install: `npm install axios`
* Import: `import axios from 'axios';`

**Example Usage:**

HTTP requests are typically placed in `componentDidMount()` (which is called after initial render) or `componentDidUpdate` (which is called after subsequent renders) because these can cause side effects.  Normally the state is not updated in these functions, however in this case it can be done because the http request/response is asynchronous.

Errors need to be handled.  An effective way to do this is to make the default state of a page to be an error state, which is only replaced by content in the event of success.  Typically errors would be written to the console, recorded in a log and/or displayed (in a user-friendly manner) to the user.

```jsx
import React, { Component } from 'react';
import axios from 'axios';

class QueryComponent extends Component {
  state = {
    posts: []
    error: false
  }

  // called after render
  componentDidMount () {
    // get() returns a Promise (because query is asynchronous)
    axios.get('http://jsonplaceholder.typicode.com/posts')
      .then(response => {
        const firstFourPosts = response.data.slice(0, 4);
        this.setState({posts:firstFourPosts});
      })       
      .catch(error => {
        this.setState({ error: true });
        console.log(error);
        log(error);
      });
  } 
  
  // called when button clicked
  postDataHandler = () => {
    const data = {
      title: this.state.title,
      body: this.state.content,
      author: this.state.author,
    };

    axios
      .post("http://jsonplaceholder.typicode.com/posts", data)
      .then(response => {
        console.log(response);
      })       
      .catch(error => {
        this.setState({ error: true });
        console.log(error);
        log(error);
      });
  };

  // called when button clicked
  deleteDataHandler = () => {
    axios
      .delete("http://jsonplaceholder.typicode.com/posts/" + this.props.id)
      .then(response => {
        console.log(response);
      })       
      .catch(error => {
        this.setState({ error: true });
        console.log(error);
        log(error);
      });   
  };
  
  // called when response received (and state updated)
  render () {
    let posts = <p>Something went wrong!</p>;
    
    if (!this.state.error) {
      posts = this.state.posts.map(post => {
        return (
          <Post 
            key={post.id} 
            title={post.title} 
            author={post.author}
          />
        );
      });
    }

    return (
      <div>
        <section>{posts}</section>
        
        <section>
          ...
          <button 
            onClick={this.postDataHandler}>
              Add Post
          </button>
        </section>

        <section>
          ...
          <button 
            onClick={this.deleteDataHandler}>
              Add Post
          </button>
        </section>
      </div>
    );
  }
}
```
**Interceptors:**

Interceptors allow HTTP messages to be intecepted globally (i.e. will be applied to every request sent from, or response received by, the app).

Typical uses are: 
   * adding common headers to requests (e.g. for authorization)
   * logging responses and requests
   * error handling
   * setting a default global config (e.g. setting a global base url)

Interceptors are usually enabled in globally significant components (e.g. index.js).

```jsx
import axios from 'axios';

// allows urls to be specified as /posts (for example)
axios.defaults.baseURL = 'http://jsonplaceholder.typicode.com'

// allows headers to be edited or inserted for all messages
axios.defaults.headers.common['Authorization'] = 'MY_AUTH_TOKEN';

// allows headers to be edited or inserted for POST messages only
axios.defaults.headers.post['Content-Type'] = 'application/json';

// intercept all requests
axios.interceptors.request.use(request => {
  // edit request here
  // must always return the request
  return request;
}, error => {
  // return an exception that can be caught
  return Promise.reject(error);
});

// intercept all responses
axios.interceptors.response.use(response => {
  // edit response here
  // must always return the response
  return response;
}, error => {
  // return an exception that can be caught
  return Promise.reject(error);
});
```

It is also possible to set up Axios "instances", which override the global defaults for different parts of the application, e.g.:

*axios.js*

```jsx
import axios from 'axios';

// Axios instances overwrite the global defaults
const instance = axios.create({
  baseURL: 'http://jsonplaceholder.typicode.com'
});

instance.defaults.headers.common['Authorization'] = 'AUTH_TOKEN_FROM_INSTANCE';

export default instance;
```
*MyComponent.js*

```jsx
import axios from '../../axios';

// within this component, values in 
// axios.js override the global defaults

...

```
</div>
</div>
<div id="database">
<button type="button" class="collapsible">+ Accessing a database</button>   
<div class="content" style="display: none;" markdown="1">

This example uses Google's Firebase database service, which is a NoSQL database (similar to MongoDB):  
   * [https://console.firebase.google.com/](https://console.firebase.google.com/)

In general, Firebase is a good choice for smaller scale or startup applications since it provides a highly scaleable, hosted database solution.  The chief downsides are the cost and the limitation that you cannot host the data layer.

For a more complex solution, or one that must be hosted internally, [https://www.mongodb.com/](MongoDB) is generally considered the go-to choice.

**Firebase**

Firebase has offers two types of database:
   * Realtime Database
      * Data is stored as one large JSON tree which makes it easier to store simple data but harder to organize complex, hierarchical data at scale.
   * Firestore
      * Data is stored as documents arranged in collections. Simple data is stored in documents, which is easy and similar to the way data is stored in JSON. Complex, hierarchical data is conveniently organized at scale using subcollections within documents. Cloud Firestore requires less denormalization and data flattening.

In general, Realtime Database is sufficient for simple apps, but Firestore is recommended for larger, more complex ones.

&nbsp;

**Accessing the database**

In this example, a Realtime Database is used with a structure similar to the following:

```
- my-app
   - items
      - item1
      - item2
      - item3
   - user-requests
      - user-request1
      - user-request2
      - user-request3
```

Database access is performed using Axios:

*db.js*
```jsx
import axios from 'axios';

const instance = axios.create({
    baseURL: 'https://my-app.firebaseio.com/'
});

export default instance;
```

*MyApp.js*
```jsx
import db from 'db';

/* Class component so that we can use lifecycle methods */
class MyApp extends Component {
  state = {
    items: null,
    requesting: false,
    loading: false,
    error: false,
  };
  
  /* Query database after component is loaded */
  componentDidMount() {
    db
      .get('/items.json') /* .json suffix is required by Firebase */
      .then((response) => {
        console.log(response);
        this.setState({ myItems: response.data });
      })
      .catch((error) => {
        console.log(error);
        this.setState({ error: true });
      });
  }

  ...
  
  /* Set state as "requesting" so that a confirmation dialog
     can be displayed to the user */
  userRequestHandler = () => {
    // must be an arrow function to use 'this' in an event handler
    this.setState({ requesting: true });
  }
  
  /* User has confirmed request, so set state to "loading" 
     and send the request to the database */
  userRequestConfirmedHandler = () => {
  
    this.setState({ loading: true });

    // package the request up as a simple object
    const userRequest = {
      items: this.state.items,
      user: {
        name: 'Fred Flintstone',
        address: {
          street: '345 Cave Stone Road',
          zipCode: '41351',
          town: 'Bedrock',
        },
        email: 'test@test.com',
      }
    };
    
    // post the request to the database
    db
      .post('/user-requests.json', order)
      .then((response) => {
        console.log(response);
        this.setState({ loading: false, requesting: false });
      })
      .catch((error) => {
        // don't need to set 'error: true' here because error will
        // be handled by withErrorHandler() wrapper
        console.log(error);
        this.setState({ loading: false, requesting: false });
      });
  };
  
  ... 
  
  render() {
    let userRequestSummary = null;

    // while waiting for a result, display a spinner, or an error message if appropriate
    let result = this.state.error ? <p>Items cannot be loaded!</p> : <Spinner />;

    // if items have been selected
    if (this.state.items) {
      // display the results of the user's selection and give the user
      // the option to submit this to the database to be saved.
      result = (
        <Wrapper>
          <Result items={this.state.items} />
          <RequestControls requested={this.userRequestHandler} />
        </Wrapper>
      );
      
      // if the state is "requesting" display a summary of the user's
      // request so that they can be confirm they really want to submit this.
      userRequestSummary = (
        <UserRequestSummary
          show={this.state.requesting}
          items={this.state.items}
          userRequestConfirmed={this.userRequestConfirmedHandler}
        />
      );
    }

    // if state is "loading", display a spinner while waiting
    // for a result
    if (this.state.loading) {
      userRequestSummary = <Spinner />;
    }

    return (
      <Wrapper>
        {userRequestSummary}
        {result}
      </Wrapper>
    );
  }  
}

export default withErrorHandler(MyApp, db);
```
</div>
</div>

<div id="forms">
<button type="button" class="collapsible">+ Forms</button>   
<div class="content" style="display: none;" markdown="1">

* *Form.js*
* *Form.module.css*
* *Input.js*
* *Input.module.css*
* *Button.js*
* *Button.module.css*

</div>
</div>

<div id="validation">
<button type="button" class="collapsible">+ Form Validation</button>   
<div class="content" style="display: none;" markdown="1">

**Validation of Email Addresses**

Some things to consider when validating email addresses:

* The purpose of validating an email address is to confirm that the user didn't accidently enter an invalid value (such as their name). It will be unlikely to catch someone doing this on purpose.
* There is no such thing as the perfect regex for email addresses because email addresses vary so widely.  The only way to truly confirm an email address is to send it an email with a verification link. 
* It is easy to disable javascript validation, so client-side verification cannot be relied on (except as a first pass).  Verification also needs to be done on the server.
* It is generally best to use the simplest "good enough" regex for validating email addresses.  A regex such as `/^\S+@\S+$/i` will catch most user errors but will fail for addresses like "me@here@there.com", which are valid email addresses.  If edge cases like these are a concern, it is better to skip the regex and just go straight to the "email with a link" step.

**Implementation**

Add `validationRules`, `valid` and `touched` values to the form state:

```jsx
  state = {
    orderForm: {
      name: {
        elementType: 'input',
        elementConfig: {
          type: 'text',
          placeholder: 'Your Name',
        },
        value: '',
        validationRules: {
          required: true,
        },
        valid: false,
        touched: false
      },
      zipCode: {
        elementType: 'input',
        elementConfig: {
          type: 'text',
          placeholder: 'Zip Code',
        },
        value: '',
        validationRules: {
          required: true,
          minLength: 5,
          maxLength: 5,
        },
        valid: false,
        touched: false
      }
      deliverymethod: {
        elementType: 'select',
        elementConfig: {
          options: [
            { value: 'fastest', displayValue: 'Fastest' },
            { value: 'cheapest', displayValue: 'Cheapest' },
          ],
        },
        value: '',
        validation: {}, // no rules
        valid: true, // always valid
        touched: false
      },
    },
    formIsValid: false, 
  };
```

Add function to validate values against rules:

```jsx
  checkValidity(value, rules) {
    let isValid = true;

    if (rules) {
      if (rules.required) {
        isValid = value.trim() !== '' && isValid;
      }

      if (rules.minLength) {
        isValid = value.length >= rules.minLength && isValid;
      }

      if (rules.maxLength) {
        isValid = value.length <= rules.maxLength && isValid;
      }

      if (rules.isEmail) {
        const EMAIL_REGEX = /^\S+@\S+$/i;
        isValid = EMAIL_REGEX.test(value) && isValid;
      }

      if (rules.isNumeric) {
        const NUMBER_REGEX = /^\d+$/;
        isValid = NUMBER_REGEX.test(value) && isValid;
      }
    }

    return isValid;
  }
```

As the form is updated, check the validity of the entered values, and the form as a whole.  

Also indicate that the user has interacted with the element.

```jsx
  inputChangedHandler = (event, inputIdentifier) => {

    // create copy of order form state
    const updatedOrderForm = { ...this.state.orderForm };

    // create copy of order form element state
    const updatedFormElement = { ...updatedOrderForm[inputIdentifier] };

    // update the order form element value
    updatedFormElement.value = event.target.value;
    
    // check that form is valid
    updatedFormElement.valid = this.checkValidity(
      updatedFormElement.value,
      updatedFormElement.validationRules
    );
    
    // indicate that the user has interacted with the element
    updatedFormElement.touched = true;
    
    // update the order form with the updated order form element
    updatedOrderForm[inputIdentifier] = updatedFormElement;

    // check if all elements of form are valid
    let formIsValid = true;
    for (const inputIdentifier in updatedOrderForm) {
      formIsValid = updatedOrderForm[inputIdentifier].valid && formIsValid;
    }

    // update state with new order form
    this.setState({ orderForm: updatedOrderForm, formIsValid: formIsValid });
  };
```

Add the following properties to each Input element in the form:
   * `shouldValidate` - avoid validating element if not necessary
   * `invalid` - flag to indicate current state of the entered value
   * `errorMessage` - message to be displayed if validation fails
   * `touched` - flag to indicate user has interacted with element
   * `changed` - handler for validation of element

Also add a `disabled` property to the `Button`, to prevent the user submitting an invalid form (note: because we use a custom `Button`, we need to pass the disabled property to the underlying `button` element).

```jsx
  render() {
    
    ...
    
    let form = (
      <form onSubmit={this.orderHandler}>
        {formElementsArray.map((formElement) => (
          <Input
            key={formElement.id}
            elementType={formElement.config.elementType}
            elementConfig={formElement.config.elementConfig}
            value={formElement.config.value}
            shouldValidate={formElement.config.validation}
            invalid={!formElement.config.valid}
            errorMessage="Please enter a valid {formElement.config.elementType}"
            touched={formElement.config.touched}
            changed={(event) => this.inputChangedHandler(event, formElement.id)}
          />
        ))}
        <Button btnType="Success" disabled={!this.state.formIsValid}>SUBMIT</Button>
      </form>
    );

    return (
      <div>
        {form}
      </div>
    );
  }
```

*Button.js*

```jsx
const Button = (props) => (
  <button
    disabled={props.disabled}
    className={[classes.Button, classes[props.btnType]].join(' ')}
    onClick={props.clicked}
  >
    {props.children}
  </button>
);
```

*Button.module.css*

```css
...

.Button:disabled {
  color: #ccc;
  cursor: not-allowed;
}

...
```

In *Input.js*, for each element, add an `Invalid` style class that can be enabled if validation fails (and user has interacted with the element).  Also, optionally, add a validation error message, with it's own `ValidationError` style class.

Finally, add an `onChange` property that will do the validation as the user updates the element.

```jsx
import classes from './Input.module.css';

const Input = (props) => {
  let inputElement = null;

  // add the Invalid class to the styling if
  // validation fails
  const inputClasses = [classes.InputElement];
  if (props.invalid && props.shouldValidate && props.touched) {
    inputClasses.push(classes.Invalid);
  }

  switch (props.elementType) {
    case 'input':
      inputElement = (
        <input
          className={inputClasses.join(' ')}
          {...props.elementConfig}
          value={props.value}
          onChange={props.changed}
        />
      );
      break;
      
    ...other cases...
  
  }
  
  let validationError = null;
  if (props.invalid && props.shouldValidate && props.touched) {
    validationError = <p className={classes.ValidationError}>{props.errorMessage}</p>;
  }
  
  return (
    <div className={classes.Input}>
      {inputElement}
      {validationError}
    </div>
  );
};
```

*Input.module.css*

```css
.Input {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
}

...other classes...

.Invalid {
  border: 1px solid red;
  background-color: #fda49a;
}

.ValidationError {
  color: red;
  margin: 5px 0;
} 
```

**Further Reading:**

* [https://validatejs.org/](https://validatejs.org/)
* [https://react.rocks/tag/Validation](https://react.rocks/tag/Validation)
* [https://www.npmjs.com/package/react-validation](https://www.npmjs.com/package/react-validation)
* [https://github.com/christianalfoni/formsy-react](https://github.com/christianalfoni/formsy-react)


</div>
</div>

<div id="env">
<button type="button" class="collapsible">+ Environment Variables</button>   
<div class="content" style="display: none;" markdown="1">

*These instructions relate to an installation using webpack (the default type generated by create-react-app)*

**IMPORTANT**: Environment variables for React applications are only referenced during the build process (e.g. when running `npm start`); the build inserts their values into the code during compilation.  The variables are not referenced at runtime (i.e. the running application does not pick up the values on-the-fly).  This means that the variables are not secure; their values are hard-wired into the code where they can be accessed by the user (e.g. you cannot use an environment variable to hide a password). 

**Built-In Environment Variables**

Built-In environment variables for React applications are defined in an `env.js` file.  This file can be found in either `./config/` or in `./node_modules/react-scripts/`.

The variables are defined in the `getClientEnvironment()` function, and can be accessed in the code using `process.env.[VAR]`, e.g. `process.env.NODE_ENV`.

Some of the more commonly used variables are:

* NODE_ENV: When `npm start` is run, it is always equal to 'development'; when `npm test` is run, it is always equal to 'test'; when `npm run build` is run, it is always equal to 'production'. NODE_ENV cannot be overridden manually (to avoid accidently deploying a slow development build in production).
* PUBLIC_URL: Contains the public URL of the app.  In theory this can be used to identify the correct path to static assets (such as images), however this is not recommended (these should really be imported into the code).  It can, however, be used as a fall-back.

A full list of built-in variables may be found here:
* [https://create-react-app.dev/docs/advanced-configuration/](https://create-react-app.dev/docs/advanced-configuration/)

**Custom Environment Variables**

Custom environment variables must be prefixed with `REACT_APP_` (to avoid clashing with the pre-existing environment of the host).  For example, `REACT_APP_NOT_SECRET_CODE` will be exposed in the code as `process.env.REACT_APP_NOT_SECRET_CODE`.

Temporarily environment variables can be set in the shell session in which the application is being run, e.g. on Windows: `set "REACT_APP_NOT_SECRET_CODE=abcdef" && npm start`

Alternatively, custom variables are typically placed in a `.env` file, in the root of the project, however there are several other possible locations:
* `.env`: Default.
* `.env.local`: Local overrides. This file is loaded for all environments except test.
* `.env.development`, `.env.test`, `.env.production`: Environment-specific settings.
* `.env.development.local`, `.env.test.local`, `.env.production.local`: Local overrides of environment-specific settings.

Files on the left have more priority than files on the right:
* `npm start`: `.env.development.local`, `.env.development`, `.env.local`, `.env`
* `npm run build`: `.env.production.local`, `.env.production`, `.env.local`, `.env`
* `npm test`: `.env.test.local`, `.env.test`, `.env` (note `.env.local` is missing)

These variables will act as the defaults if the machine does not explicitly set them.

**Accessing Environment Variables In HTML**

Environment variables can be embedded in HTML in the following manner: `<title>%REACT_APP_WEBSITE_NAME%</title>`

**Using Existing Variables**

Existing variables (i.e. those defined in the current session, or define previously in a `.env` file) can be referenced in a `.env` file in the following manner:
* `REACT_APP_VERSION=$npm_package_version` or `REACT_APP_VERSION=${npm_package_version}`
* `DOMAIN=www.example.com` and `REACT_APP_FOO=$DOMAIN/foo`
</div>
</div>

</div>
</div>

<div id="routing">
<button type="button" class="collapsible">+ Routing</button>   
<div class="content" style="display: none;" markdown="1">

<div id="routing-basics">
<button type="button" class="collapsible">+ Routing Basics</button>   
<div class="content" style="display: none;" markdown="1">
Routing is the functionality that allows a single page to serve multiples pages as if the user was browsing separate URLs.
  
There are three stages to routing:
1. Parse the URL
1. Read the config
1. Render the appropriate component

Routing is enabled by installing and importing the react-router-dom package:

* Install: `npm install react-router-dom`
* Import: 
   * `import { BrowserRouter } from 'react-router-dom';`
   * `import { Router } from 'react-router-dom';`
   * `import { Link } from 'react-router-dom';`
   * `import { NavLink } from 'react-router-dom';`
   * `import { withRouter } from 'react-router-dom';`
   * `import { Switch } from 'react-router-dom';`
   * `import { Redirect } from 'react-router-dom';`
</div>
</div>

<div id="browser-router">
<button type="button" class="collapsible">+ BrowserRouter Component</button>   
<div class="content" style="display: none;" markdown="1">   

To implement routing, the first thing step is to, in either App.js or index.js files, wrap the part of the app that supports routing with the `BrowserRouter` component:

*index.js*

```jsx
...etc...
import { BrowserRouter } from 'react-router-dom';

...etc...

ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById('root')
);

...etc...
```
</div>
</div>

<div id="route">
<button type="button" class="collapsible">+ Route Component</button>   
<div class="content" style="display: none;" markdown="1">   

The next step is to  add the `Route` component to components where the contents should be dependent on the path, e.g.:
```jsx
import React, { Component } from "react";
import { Route } from "react-router-dom";
import Posts from "Posts";
import NewPost from "NewPost";

class Blog extends Component {
  render() {
    return (
      <div className="Blog">
        <header>
          <nav>
            <ul>
              <li>
                <a href="/">Home</a>
              </li>
              <li>
                <a href="/new-post">New Post</a>
              </li>
            </ul>
          </nav>
        </header>
        
        {/* path = the relative path to handle 
            exact = by default, the component will match paths that 
                    start with the path value; the property forces 
                    exact matching
            render = the function to be called if the path matches
            component = the component to be called if the path matches */}
        <Route path="/" exact render={() => <h1>Home</h1>} />
        <Route path="/" exact component={Posts} />
        <Route path="/new-post" component={NewPost} />
        
        {/* The Route component can reference the same path
            multiple times in the same page */}
        <Route path="/" render={() => <h1>Home 2</h1>} />
      </div>
    );
  }
}
```

The `render` property of the `Route` component is only really used in two use-cases:
1. Making small updates to a page, such as simple messages or images (e.g. `render={() => <h1>Hello!</h1>}`)
1. Enabling props to be passed to a component (e.g. `render={ () => <ContactData address={this.state.address} />}`)

Generally, and particularly for larger sections, the `component` property should be preferred.
</div>
</div>

<div id="parse-url">
<button type="button" class="collapsible">+ Parsing URL Parameters</button>   
<div class="content" style="display: none;" markdown="1">   

*Parsing the Route*

Often it is not possible to hardwire a specific path in the route.  In these cases, a route parameter can be used. A route parameter is effectively a wildcard that copies a section of the link into a variable.  

An example might be:
   * `<Route path="/:id/:title" component={MyComponent} />`

The crucial features are the `:` delimiters.  These indicate that everything following them (until the next '/') should be copied into the specified variable.  So, in the above case, the path `/4/Lessons` would be parsed as `id = "4"; title = "Lessons"`.

The parsed variables are passed to the linked component (`MyComponent`) and can be accessed using `this.props.match.params.id; this.props.match.params.title`.

Note that `Route` components are evaluated in sequence, so care must be taken with the order of parsing to ensure that the results are as expected, e.g.:
```jsx
  {/* test 1: if matches "/" exactly */}
  <Route path="/" exact component={Posts} />

  {/* test 2: if matches any route that begins with "/new-post" */}
  <Route path="/new-post" exact component={NewPost} />
  
  {/* test 3: if matches any route that begins with "/";
      anything following "/" will be assigned to the "id" 
      property*/}
  <Route path="/:id" exact component={FullPost} />
```
In this case, both `test 2` and `test 3` will match `/new-post`, so both of their components will be displayed.

An alternative approach is to use the `Switch` component.  If `Route` elements are placed inside a `Switch` element, only the first match succeeds, e.g.:
```jsx
  {/* test 1: if matches "/" exactly */}
  <Route path="/" exact component={Posts} />

  <Switch>
    {/* test 2: if matches any route that begins with "/new-post" */}
    <Route path="/new-post" exact component={NewPost} />

    {/* test 3: else if matches any route that begins with "/";
        anything following "/" will be assigned to the "id" 
        property*/}
    <Route path="/:id" exact component={FullPost} />
  </Switch>
```
In this case, only `test 2` will match `/new-post`, since `test 3` will not be called.

*Parsing the Query/Search Parameters*

To extract search (also referred to as "query") parameters (i.e. `?something=somevalue`, or `<Link to={ { pathname: '/my-path', search: '?start=5' } }`, `props.location.search` is used, however this only returns something like `?start=5`.

To convert this string to a more useful key-value pair, use `URLSearchParams`, e.g.
```jsx
componentDidMount() {
    const query = new URLSearchParams(this.props.location.search);
    for (let param of query.entries()) {
        console.log(param); // yields ['start', '5']
    }
}
```
`URLSearchParams` is a built-in object, shipping with vanilla JavaScript. It returns an object, which exposes the entries()  method. entries() returns an Iterator - basically a construct which can be used in a for...of...  loop (as shown above).

When looping through query.entries(), you get arrays where the first element is the key name (e.g. start ) and the second element is the assigned value (e.g. 5 ).

*Parsing the Fragment/Hash Parameter*

The hash, or fragment, of a path is passed using the following:

`<Link to="/my-path#start-position">Go to Start</Link>`

or,
```jsx
<Link 
    to={ {
        pathname: '/my-path',
        hash: 'start-position'
    } }
    >Go to Start</Link>
```
This value can be accessed using `props.location.hash`.
</div>
</div>

<div id="link">
<button type="button" class="collapsible">+ Link Component</button>   
<div class="content" style="display: none;" markdown="1">

If a link is specified using the familiar `<a href="">` element, this will force the entire page to be re-fetched from the server.  Typically this is not desirable; in modern web apps it is more typical to only refresh those sections of the page that have changed.

To avoid the full page refresh, the `Link` component is used:
```jsx
import React, { Component } from "react";
import Posts from "Posts";
import NewPost from "NewPost";

class Blog extends Component {
  render() {
    return (
      <div className="Blog">
        <header>
          <nav>
            <ul>
              <li>
                {/* 'to' can be a simple string */}
                <Link to="/">Home</Link>
              </li>
              <li>
                {/* 'to' can also be a javascript object */}
                <Link to={ {
                  pathname: '/new-post',
                  hash: '#submit',
                  search: '?quick-submit=true'
                } }>New Post</Link>
              </li>
            </ul>
          </nav>
        </header>
        
        <Route path="/" exact component={Posts} />
        <Route path="/new-post" component={NewPost} />
      </div>
    );
  }
}
```

Note: `Link` paths are *always* absolute, regardless of whether "/new-post" or "new-post" is used.  In the latter case, this will be converted to "/new-post".

If you want to use a relative path, you need to build this dynamically based on knowledge of the current path, e.g. if you are currently at /posts and want to go to /posts/new-post, you would construct a path using `pathname: currentUrl + '/new-post'`.

If the current path was accessed via a `Link`, the current path can be accessed using the local props (in this case, `this.props.match.url`).
</div>
</div>

<div id="route-props">
<button type="button" class="collapsible">+ Route Props</button>   
<div class="content" style="display: none;" markdown="1">

If the props of a component that has been called from a `Link` are examined, it can be seen that a wealth of information is available for use in the component:
```jsx
class NewPost extends Component {
  ...
  componentDidMount() {
    console.log(this.props);
  }  
  ...
}
```

```jsx
{history: {…}, location: {…}, match: {…}, staticContext: undefined}
  history:
    action: "PUSH"
    block: ƒ block(prompt)
    createHref: ƒ createHref(location)
    go: ƒ go(n)
    goBack: ƒ goBack()
    goForward: ƒ goForward()
    length: 21
    listen: ƒ listen(listener)
    location: {pathname: "/new-post", hash: "#submit", search: "?quick-submit=true", key: "5mpy2d"}
    push: ƒ push(path, state)
    replace: ƒ replace(path, state)
    __proto__: Object
  location:
    hash: "#submit"
    key: "5mpy2d"
    pathname: "/new-post"
    search: "?quick-submit=true"
    __proto__: Object
  match:
    isExact: true
    params: {}
    path: "/new-post"
    url: "/new-post"
    __proto__: Object
  staticContext: undefined
  __proto__: Object
```
However, these extra properties are not passed down, by default, to children of the component.  

There are two approaches to passing these properties further down the chain:

**...props**

One approach is to use the spread operator to add the props to the child components:

```jsx
  render() {
        return (
          <Post
            key={post.id}
            title={post.title}
            author={post.author}
            {...this.props} 
            {/* or, {this.props.myProp} for a specific property /*}
            clicked={() => this.postSelectedHandler(post.id)}
          />
        );
    }
```

**withRouter() HOC**

A more sophisticated approach is to use the `withRouter` HOC, which, when wrapped around a component, ensures that the component receives the route props.

```jsx
import React from 'react';
import { withRouter } from 'react-router-dom';

const post = (props) => {
  console.log(props);
  return (
    <article className="Post" onClick={props.clicked}>
      <h1>{props.title}</h1>
      <div className="Info">
        <div className="Author">{props.author}</div>
      </div>
    </article>
  );
};

export default withRouter(post);
```
</div>
</div>

<div id="navlink">
<button type="button" class="collapsible">+ NavLink Component</button>   
<div class="content" style="display: none;" markdown="1">

An extension of the `Link` component is the `NavLink` component.  Both components behave exactly the same when it comes to linking, however `NavLink` also allows styling to be applied to a link.  It also enables the correct focus to be maintained, for accessibility.

When `NavLink` is used in place of `Link`, the resulting `a` element is decorated with two new properties:
   * `aria-current="page"`: this indicates that this is the link for the current page and is chiefly used by screen-readers.
      * For further details, see: [https://tink.uk/using-the-aria-current-attribute/](https://tink.uk/using-the-aria-current-attribute/)
   * `class="active"`: this provides a class that can be used for styling.
      * The class name can be changed using the `activeClassName` property.

e.g. `<NavLink to="/">Home</NavLink>` translates to `<a aria-current="page" class="active" href="/">Home</a>`.

Additional `NavLink` properties include:
   * `activeStyle`, which allows inline CSS to be specified as a javascript object
   * `isActive`, which indicates that the link should be flagged as the active link (overriding the default).
   * `location`, which overrides the current location property.

An example might be:

```jsx
<NavLink
  {/* the link */}
  to="/user"
  
  {/* inline styling */}
  activeStyle={ {
    background: 'red',
    color: 'white',
  } }
  
  {/* override the search property of the current location */}
  location={ {
    search: '?id=2',
  } }
  
  {/* this link is marked as active if match.isExact is true
      and the current search params contain 'id' (which it
      will do because location.search has been overridden) */}
  isActive={(match, location) => {
    if (!match) {
      return false;
    }
    const searchParams = new URLSearchParams(location.search);
    return match.isExact && searchParams.has('id');
  } }
>
  User
</NavLink>
```

For further information see here:
   * [https://www.codementor.io/@packt/using-the-link-and-navlink-components-to-navigate-to-a-route-rieqipp42](https://www.codementor.io/@packt/using-the-link-and-navlink-components-to-navigate-to-a-route-rieqipp42)
</div>
</div>

<div id="prog-nav">
<button type="button" class="collapsible">+ Progammatic Navigation</button>   
<div class="content" style="display: none;" markdown="1">

In the event that navigate must happen in response to some event (rather than directly to user input), the `history` prop can be used.  For example,
```jsx
  postSelectedHandler = (id) => {
    this.props.history.push({ pathname: '/' + id });
  };
  
  render() {
    return (
      <Post
        key={post.id}
        title={post.title}
        author={post.author}
        clicked={() => this.postSelectedHandler(post.id)}
      />
    );
  }
```
</div>
</div>

<div id="nested-routes">
<button type="button" class="collapsible">+ Nested Routes</button>   
<div class="content" style="display: none;" markdown="1">

Routes can be specified anywhere in the app as long as the components fall under the `BrowserRoute` tags.  This means that it is possible for routes to be nested (i.e. a `Route` calls a component that contains another `Route`).  This can be problematic since all of the routes, no matter where they are located, are still evaluated sequentially.  This can lead to a route being "blocked" by a preceding route.

For example:
```jsx
class Blog extends Component {
  render() {
    return (
      <div className="Blog">
        <Switch>
          {/* test 1: if matches "/" exactly */}
          <Route path="/" exact component={Posts} />

          {/* test 2: else if starts with "/new-post" */}
          <Route path="/new-post" exact component={NewPost} />
        </Switch>
      </div>
    );
  }
}

class Posts extends Component {
  render() {
    return (
      <div className="Posts">
        {/* test 3: if matches any route that begins with "/";
            anything following "/" will be assigned to the "id" 
            property*/}
        <Route path="/:id" exact component={FullPost} />
      </div>
    );
  }
}
```
In the above case, if the URL `/5` is specified, this will never be passed down to the `Posts` component because `Posts` is called by the `Route` in the `Blog` component, which is only called if the path is *exactly* `/`.

One solution would be to simply remove the `exact` property from the blog `Route`, so that `Posts` is always called. However, this will cause the additional problem that the `/new-post` route will never be called (since the `Switch` element only allows the first matched `Route` to pass).

A better solution would be to remove the `exact` property *and* change the order of the routes in the `Switch` element:
```jsx
  <div className="Blog">
    <Switch>
      {/* test 1: if starts with "/new-post" */}
      <Route path="/new-post" exact component={NewPost} />
      
      {/* test 2: else if starts with "/" */}
      <Route path="/" component={Posts} />
    </Switch>
  </div>
```
In this case, a URL of `/5` will fail `test 1` but pass `test 2`, which in turn will mean that `test 3` is called in the `Posts` component.

However, an issue remains.  In the following example, `test2` tests for `/posts`, rather than `/`:
```jsx
  <div className="Blog">
    <Switch>
      {/* test 1: if starts with "/new-post" */}
      <Route path="/new-post" exact component={NewPost} />
      
      {/* test 2: else if starts with "/posts" */}
      <Route path="/posts" component={Posts} />
    </Switch>
  </div>
```
This means that all relevant paths need to be updated to be `/posts`, including `test 3`:
```
  <div className="Posts">
    {/* test 3: if matches any route that begins with "/posts";
        anything following "/posts" will be assigned to the "id" 
        property*/}
    <Route path="/posts/:id" exact component={FullPost} />
  </div>
```
This is cumbersome, particularly if the `Posts` component might be moved or re-used elsewhere.

The solution is to get the url dynamically, using the route props:
```
  <div className="Posts">
    {/* test 3: if matches any route that begins with this.props.match.url;
        anything following this.props.match.url will be assigned to the "id" 
        property*/}
    <Route path={this.props.match.url + '/:id'} exact component={FullPost} />
  </div>
```
</div>
</div>

<div id="redirect">
<button type="button" class="collapsible">+ Redirect Component</button>   
<div class="content" style="display: none;" markdown="1">

A simple way to redirect a user is to provide duplicate routes, e.g.:
```jsx
  <div className="Blog">
    <Switch>
      <Route path="/new-post" exact component={NewPost} />
      <Route path="/posts" component={Posts} />
      <Route path="/" component={Posts} />
    </Switch>
  </div>
```

There is, however, a more elegant solution using the `Redirect` component:
```jsx
  <div className="Blog">
    <Switch>
      <Route path="/new-post" exact component={NewPost} />
      <Route path="/posts" component={Posts} />
      <Redirect from="/" to="/posts" />
    </Switch>
  </div>
```
Note: if used outside of a `Switch` element, only the `to` property can be used.  This syntax is typically used in conjunction with a condition, e.g.
```jsx
  render() {
    let redirect = null;
    if (this.state.submitted) {
      redirect = <Redirect to="/posts" />;
    }
    return (
      <div className="NewPost">
        {redirect}
      </div>
    );
  }
```

**Alternative Redirect Using History**

An alternative method of redirecting is to push the new page onto the history:
```
  axios.post('/posts', data).then((response) => {
    this.props.history.push('/posts');
  });
```
This essentially moves the browser forward, so that subsequently clicking "Back" will take the user to the preceeding page.

This is different from the `Redirect` component, which actually replaces the current page in the history, so clicking "Back" will effectively take the user *two* pages back.

This latter behaviour can be reproduced using the `history.replace()`.
</div>
</div>

<div id="guards">
<button type="button" class="collapsible">+ Guards</button>   
<div class="content" style="display: none;" markdown="1">

A guard is essentially a conditional statement that controls access to a component, such as a `Route`, or is called in a lifecycle method to prevent access when a component is loaded.

For example:
```jsx
  <div className="Blog">
    <Switch>
      {this.state.auth ? <Route path="/new-post" exact component={NewPost} /> : null}
      <Route path="/posts" component={Posts} />
      <Redirect from="/" to="/posts" />
    </Switch>
  </div>
```
Or, alternatively:
```jsx
class NewPost extends Component {
  componentDidMount() {
    if (notAuth) this.props.history.replace('/posts');
  }
}
```

An additional solution might be:

*ProtectedRoute.js*
```jsx
class ProtectedRoute extends Component {
  render() {
    const { component: Component, ...props } = this.props

    return (
      <Route 
        {...props} 
        render={props => (
          this.state.authenticated ?
            <Component {...props} /> :
            <Redirect to='/login' />
        )} 
      />
    )
  }
}
```
*Blog.js*
```jsx
  <div className="Blog">
    <Switch>
      <ProtectedRoute path="/new-post" exact component={NewPost} />
      <Route path="/posts" component={Posts} />
      <Redirect from="/" to="/posts" />
    </Switch>
  </div>
```

A crucial concept to understand when using react-router is that components can only be accessed if the developer has chosen to render them; if they are not rendered (for example, because they don't meet some condition), they will be inaccessible.
</div>
</div>

<div id="error-404">
<button type="button" class="collapsible">+ Handling 404 Errors</button>   
<div class="content" style="display: none;" markdown="1">

The simplest way to handle a 404 error (resource not found) is to provide a catch-all `Route` that handles any case where the path is unknown.

For example:
```jsx
  // this.state.auth = false;
  
  <div className="Blog">
    <Switch>
      {/* test 1: if starts with "/new-post" and user is authorized to access this */}
      {this.state.auth ? <Route path="/new-post" exact component={NewPost} /> : null}

      {/* test 2: else if starts with "/posts" */}
      <Route path="/posts" component={Posts} />
      
      {/* test 3: else if nothing matched, display an error message */}
      <Route render={() => <h1>Not found</h1>} />
    </Switch>
  </div>
```
Note that the catch-all `Route` does not have a path specified, so it will always render if all of the previous routes fail.
</div>
</div>

<div id="lazy-load">
<button type="button" class="collapsible">+ Code Splitting/Lazy Loading</button>   
<div class="content" style="display: none;" markdown="1">

Rather than load the entire application when the user first visits the site, it is more efficient (for large applications) to only load the components as the user requests them.  This is known as code splitting or lazy loading.

To achieve this, a new HOC is created:

*asyncComponent.js*

```jsx
import React, { Component } from 'react';

// importComponent will be a function
// reference that returns a Promise
const asyncComponent = (importComponent) => {

  // function component returns a class component
  return class extends Component {
    // state.component will store the component
    // to be rendered.  Initially this is false.
    state = {
      component: null,
    };

    componentDidMount() {
      // comp will be the component being loaded dynamically
      // state.component is set to comp
      importComponent().then((comp) => {
        this.setState({ component: comp.default });
      });
    }

    render() {
      // get state.component (which could be null)
      const C = this.state.component;

      // if state.component exists, return it (with any props)
      return C ? <C {...this.props} /> : null;
    }
  };
};

export default asyncComponent;
```
Wherever we want to eventually render the lazily loaded component, we instead import the `asyncComponent` and initialize it:

*Blog.js*

```jsx
import asyncComponent from './asyncComponent';

// This is known as a dynamic import.
// The import statement will only be called 
// when AsyncNewPost is rendered to the screen.
const AsyncNewPost = asyncComponent(() => {
  return import('./NewPost');
});

class Blog extends Component {
  state = {
    auth: true,
  };
  
  ...check auth...
  
  render() {
    return (
        <Switch>
          {this.state.auth ? <Route path="/new-post" exact component={AsyncNewPost} /> : null}
          <Route render={() => <h1>Not Authorized</h1>} />
        </Switch>
      </div>
    );
  }
}

```

**Lazy Loading with React Suspense**

*At time of writing, this is not supported for server-side apps*

Since React 16.6, a new approach to lazy loading was added.  There are two parts:
   * The `React.lazy()` method - this returns a promise that can be "pending" or "resolved".
   * The `Suspense` component - this handles the promise, either rendering a fallback message/spinner if the promise is still pending, or displaying the component if the promise is resolved.

```jsx
import React, { Component, Suspense } from 'react';
import User from './User';

// When the Posts component is rendered, 
// React.lazy() returns a promise while
// the Posts component is fetched.
const Posts = React.lazy(() => import('./containers/Posts'));

class App extends Component {
  state = { showPosts: false };

  modeHandler = () => {
    this.setState((prevState) => {
      return { showPosts: !prevState.showPosts };
    });
  };

  render() {
    return (
      <React.Fragment>
        <button onClick={this.modeHandler}>Toggle Mode</button>

        {this.state.showPosts ? (
          <Suspense fallback={<div>Loading...</div>}>
            <Posts />
          </Suspense>
        ) : (
          <User />
        )}
      </React.Fragment>
    );
  }
}

export default App;
```
</div>
</div>

<div id="route-deploy">
<button type="button" class="collapsible">+ Routing & Server Deployment</button>   
<div class="content" style="display: none;" markdown="1">

There are two main issues to be aware of what deploying a React app to a server:
1. Always return index.html
   * The server knows nothing about the routes in a React app, which means that the server cannot redirect the browser to the requested part of the app.
   * The solution is to ensure that the server is configured to *always* return index.html, since index.html will then load the React app, which can, in turn, interpret the requested path.
   * This happens by default on the NPM development server.
1. Always provide a `basename` for the `BrowserRouter`
   * `BrowserRouter` assumes that all routes requested in the app are relative to the root `basename` property.
   * If this is not explicitly specified, the `basename` is assumed to be `/` (the server root, e.g. example.com/).
   * If the React app is not located at the server root (e.g. example.com/my-app) and `basename` is not specified, specifying a route in the app (e.g. /posts/) will fail (because the server reads this as example.com/posts/ rather than example.com/my-app/posts/).
   * To avoid this, the `BrowserRouter` element should always be specified as `<BrowserRouter basename="/my-app">`

</div>
</div>

</div>
</div>

<div id="redux">
<button type="button" class="collapsible">+ Redux</button>   
<div class="content" style="display: none;" markdown="1">

<div id="redux-overview">
<button type="button" class="collapsible">+ Redux Overview</button>   
<div class="content" style="display: none;" markdown="1">

Redux is not a part of React, however it is a concept/feature that React can take advantage of via the `react-redux` module.  Essentially, the module is wrapping the Redux logic and providing a way to access it in a more React-friendly manner.

So, just to recap, the basic idea behind Redux is that you are taking an initial state and performing one or more actions on it to "reduce" it to a final state. 

In both the basic and React versions, the application state is maintained by a "store".  You don't need to know the fine details of the store, other than that the state is passed to/from the store as a JavaScript object.  The state object is automatically passed into the reducer whenever an action is triggered. 

The store is maintained in memory and so is reset if the application is refreshed.

The store is initialized by passing it a reducer (or multiple reducers, if `combineReducers` is used).  The state object is initialized the very first time an action runs using a dummy initial state object.

In React, the store is made accessible to the app using the `<Provider />` component.

The reducer contains the logic that actually updates the state/store.  Each function in the reducer maps to a similar function in the actions.

Triggering the reducer logic is done using the actions, which essentially just broadcast (i.e. `dispatch`) an identifier for a particular reducer function, plus the data required by the reducer function.  The reducer listens for these dispatches and ensures that the correct reducer function is triggered with the correct data.

The individual React app components are linked to the Redux store using the `connect` function (provided by `react-redux`).  The `connect` function serves two purposes:
1. It exposes the functions that dispatch the actions to the component via the `mapDispatchToProps` function.
1. It exposes the current state to the component via the `mapStateToProps` function.

So, in summary, the app functions like this:

1. Intialize store with a reducer
1. Wrap app in `<Provider />` tags to make the store accessible
1. In a component that wishes to update the state:
  * Map function to actions using `mapDispatchToProps`
  * Map local props to state properties using `mapStateToProps`
  * Link the map functions to the store using `connect` function.
1. When component calls a mapped function, `dispatch` the related action
1. When the reducer receives the action and current state, trigger the related reducer function.
1. The reducer function updates the state, which is returned to the store.
1. The updated state is exposed to the app via the mapped props.

</div>
</div>

<div id="redux-basics">
<button type="button" class="collapsible">+ Redux Basics</button>   
<div class="content" style="display: none;" markdown="1">

**Redux Lifecycle**

<a href="assets/redux-lifecycle.png" target="_blank"><img src="assets/redux-lifecycle.png" style="width: 100%" /></a>

**A Simple Non-React Redux Example**

This example is standalone code; it does not require React.

* Install: `npm install redux`

To run this: `node redux-basics.js`

*redux-basics.js*

```js
const redux = require('redux'); // nodejs syntax
const createStore = redux.createStore;

const initialState = {
  counter: 0,
};

// Reducer
const rootReducer = (state = initialState, action) => {
  if (action.type === 'INC_COUNTER') {
    return {
      ...state, // get existing state
      counter: state.counter + 1, // overwrite counter
    };
  }

  if (action.type === 'ADD_COUNTER') {
    return {
      ...state, // get existing state
      counter: state.counter + action.value, // overwrite counter
    };
  }

  return state;
};

// Store
const store = createStore(rootReducer);
console.log(store.getState());

// Subscription
store.subscribe(() => {
  console.log('[Subscription]', store.getState());
});

// Dispatching Action
store.dispatch({ type: 'INC_COUNTER' });
store.dispatch({ type: 'ADD_COUNTER', value: 10 });
console.log(store.getState());

```
</div>
</div>

<div id="react-redux">
<button type="button" class="collapsible">+ Redux in React</button>   
<div class="content" style="display: none;" markdown="1">

   * Install: `npm install redux`
   * Import: `import { createStore, combineReducers, applyMiddleware } from 'redux';`

   * Install: `npm install react-redux`
   * Import: `import { Provider, connect } from 'react-redux';`

There are four main stages when hooking the Store up to a React application:
   * Import the Reducer
   * Create the Store using the Reducer
   * Inject the Store into the App using a Provider (imported from `react-redux`)
   * Indicate which components are interested in which state properties using the `connect` function (imported from `react-redux`)

**`<Provider/>`**

Under the covers, the `<Provider store={store}/>` implementation basically boils down to this:

```js
const Provider = (props) => {

  const store = props.store;

  return (
    <div>
      {props.children}
    </div>
  );
}
```

The actual implementation can be reviewed here:
* [https://github.com/reduxjs/react-redux/blob/master/src/components/Provider.js](https://github.com/reduxjs/react-redux/blob/master/src/components/Provider.js)

In this way, the `store` is accessible to all of the children (i.e. the app) of `<Provider>`, although the children cannot access it directly; they need to use the various functions provided by Redux.

**Simple Example of Redux in a React App**

Usually, the Store is created in the *index.js* file (where the `<App />` is added to the DOM).  Note that the Provider component wraps the entire app, including the BrowserRouter component.

*index.js* 

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { createStore } from 'redux';
import { Provider } from 'react-redux';
import './index.css';
import App from './App';
import registerServiceWorker from './registerServiceWorker';

import reducer from './store/reducer';

const store = createStore(reducer);

ReactDOM.render(<App />, document.getElementById('root'));
ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
registerServiceWorker();
```

The Reducer is normally defined in a separate file, which is typically `src/store/reducer.js`.

Note: great care must be taken to ensure that the state is always updated immutably!

*reducer.js*

```jsx
import * as actionTypes from './actions/actions';

const initialState= {
  counter: 0,
  results: [],
}

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionTypes.INCREMENT: {
      // spread existing state into new object, 
      // then override counter value
      return {
        ...state,
        counter: state.counter + 1,
      };
    }
    case actionTypes.DECREMENT: {
      return {
        ...state,
        counter: state.counter - 1,
      };
    }
    case actionTypes.ADD: {
      return {
        ...state,
        counter: state.counter + action.val,
      };
    }
    case actionTypes.SUBTRACT:
      return {
        ...state,
        counter: state.counter - action.val,
      };
    case actionTypes.STORE_RESULT: {
      // spread existing state into new object, 
      // then override results by calling concat(),
      // which returns a new array with the value added,
      // leaving the original array untouched
      // (do not use push(), which will change the existing state)
      return {
        ...state,
        results: state.results.concat({ id: new Date(), value: state.counter }),
      };
    }
    case actionTypes.DELETE_RESULT: {
      // spread existing state into new object, 
      // then override results by calling filter(),
      // which returns a new array with only the values
      // that match the filter function.
      // The original array is untouched.
      // (do not use push(), which will change the existing state)
      const updatedArray = state.results.filter((result) => result.id !== action.id);
      return {
        ...state,
        results: updatedArray,
      };
    }
    default:
      return state;
  }
}

export default reducer;
```

To subscribe to the Store in React, the `connect()()` function is used (imported from `react-redux`):

*Counter.js*

```jsx
import React, { Component } from 'react';
import { connect } from 'react-redux';
import CounterControl from './CounterControl';
import CounterOutput from './CounterOutput';
import * as actionTypes from './actions/actions';

class Counter extends Component {
  // local state is no longer needed
  // state = {
  //   counter: 0,
  // };

  render() {
    return (
      <div>
        {/* get counter value from Redux store */}
        <CounterOutput value={this.props.ctr} />
        <CounterControl label="Increment" clicked={this.props.onIncrementCounter} />
        <CounterControl label="Decrement" clicked={this.props.onDecrementCounter} />
        <CounterControl label="Add 5" clicked={this.props.onAddCounter.bind(this, 5)} />
        <CounterControl label="Subtract 5" clicked={this.props.onSubtractCounter.bind(this, 5)} />
        <hr />
        <button onClick={this.props.onStoreResult}>Store Result</button>
        <ul>
          {this.props.storedResults.map((strResult) => (
            <li key={strResult.id} onClick={this.props.onDeleteResult.bind(this, strResult.id)}>
              {strResult.value}
            </li>
          ))}
        </ul>
      </div>
    );
  }
}

// define function to indicate the state properties
// in which this component is interested
const mapStateToProps = (state) => {
  return {
    // maps state.counter to this.props.ctr
    ctr: state.counter,
    // maps state.results to this.props.storedResults
    storedResults: state.results,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    onIncrementCounter: () => dispatch({ type: actionTypes.INCREMENT }),
    onDecrementCounter: () => dispatch({ type: actionTypes.DECREMENT }),
    onAddCounter: (num) => dispatch({ type: actionTypes.ADD, val: num }),
    onSubtractCounter: (num) => dispatch({ type: actionTypes.SUBTRACT, val: num }),
    onStoreResult: () => dispatch({ type: actionTypes.STORE_RESULT }),
    onDeleteResult: (id) => dispatch({ type: actionTypes.DELETE_RESULT, id: id }),
  };
};

// the connect()() function basically says:
// the Counter component will use the
// state properties defined in mapStateToProps,
// and will update the state using the functions
// defined in mapDispatchToProps; please expose 
// the properties and functions via this.props.
export default connect(mapStateToProps, mapDispatchToProps)(Counter);

```

To reduce bugs due to typos, action types are stored as const values in a separate file, which can then be imported:

*actions/actions.js*

```jsx
export const INCREMENT = 'INCREMENT';
export const DECREMENT = 'DECREMENT';
export const ADD = 'ADD';
export const SUBTRACT = 'SUBTRACT';
export const STORE_RESULT = 'STORE_RESULT';
export const DELETE_RESULT = 'DELETE_RESULT';
```

</div>
</div>

<div id="redux-combine">
<button type="button" class="collapsible">+ Combining Reducers</button>   
<div class="content" style="display: none;" markdown="1">

Rather than locating all reducer functions in a single file, they can be split across multiple files and then combined using the `combineReducers` function, provided by Redux.

For example, in the following example, *reducer.js* (from above) is split into *counter.js* and *result.js* and then combined:

*reducers/counter.js*

```jsx
import * as actionTypes from '../action/actions';

// only need to include state properties relevant
// to the reducers in this file
const initialState = {
  counter: 0,
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionTypes.INCREMENT: {
      return {
        ...state,
        counter: state.counter + 1,
      };
    }
    case actionTypes.DECREMENT: {
      return {
        ...state,
        counter: state.counter - 1,
      };
    }
    case actionTypes.ADD: {
      return {
        ...state,
        counter: state.counter + action.val,
      };
    }
    case actionTypes.SUBTRACT:
      return {
        ...state,
        counter: state.counter - action.val,
      };
    }
    default:
      return state;
  }
};

export default reducer;
```

*reducers/result.js*

```jsx
import * as actionTypes from '../actions/actions';

// only need to include state properties relevant
// to the reducers in this file
const initialState = {
  results: [],
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionTypes.STORE_RESULT: {
      return {
        ...state,
        results: state.results.concat({ id: new Date(), value: action.result }),
      };
    }
    case actionTypes.DELETE_RESULT: {
      const updatedArray = state.results.filter((result) => result.id !== action.id);
      return {
        ...state,
        results: updatedArray,
      };
    }
    default:
      return state;
  }
};

export default reducer;
```

*index.js*

```jsx
...etc...

import { createStore, combineReducers } from 'redux';

...etc...

// import the reducers
import counterReducer from './reducers/counter';
import resultReducer from './reducers/result';

// expose individual reducers as rootReducer properties
const rootReducer = combineReducers({
  ctr: counterReducer,
  res: resultReducer
});

// create the store
const store = createStore(rootReducer);

...etc...

```

When combining reducers, one issue to be aware of is that the individual reducers can no longer directly access the combined state.  The normal workaround for this is to pass any shared state properties as part of the action payload.

*Counter.js*

```jsx
...etc...

class Counter extends Component {
  render() {
    return (
      <div>
      
        ...etc...
        
        // pass current counter value to the event handler
        <button onClick={this.props.onStoreResult.bind(this, this.props.ctr)}>Store Result</button>
      
        ...etc...
        
      </div>
    );
  }
}

// expose individual reducer state properties as local props
const mapStateToProps = (state) => {
  return {
    ctr: state.ctr.counter,
    storedResults: state.res.results,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    ...etc...

    // pass the current counter result to the action payload 
    onStoreResult: (ctrResult) => dispatch({ type: actionTypes.STORE_RESULT, result: ctrResult }),

    ...etc...
  };
};

...etc...

```

</div>
</div>

<div id="redux-when">
<button type="button" class="collapsible">+ When To Use Redux</button>   
<div class="content" style="display: none;" markdown="1">

The following diagram gives a high-level overview of when it is generally considered wise to use Redux, although a quick summary would be: 
   * Use for managing current client/user state.
   * Not normally used for managing UI state.
   * Do not use for persistant state (i.e. it is not a replacement for a database).

<a href="assets/when-to-use-redux.png" target="_blank"><img src="assets/when-to-use-redux.png" style="width: 100%" /></a>

</div>
</div>

</div>
</div>

<div id="redux-middleware">
<button type="button" class="collapsible">+ Advanced Redux Topics</button>   
<div class="content" style="display: none;" markdown="1">

<div id="redux-middleware">
<button type="button" class="collapsible">+ Middleware</button>   
<div class="content" style="display: none;" markdown="1">

In the context of Redux, middleware is a function that can be inserted into a Redux implementation to react to, or alter, an action before it is received by the reducer.

The middleware is defined in index.js:
  
*index.js*

```jsx
// add logger middleware function, to which
// we pass the Redux store
const logger = store => {
  // return another function, to which we
  // pass a 'next' argument.
  // 'next' will be a function which can be
  // executed to let the action continue
  // its journey onto the reducer.
  return next => {
    // return yet another function, to which
    // is passed an 'action' argument.
    // This function will be executed automatically.
    return action => {
      // this is the code we actually want to execute

      console.log('[Middleware] Dispatching', action);
      // this allows the action to continue to 
      // the reducer (the action could be
      // changed in this middleware - with care!)
      const result = next(action);

      console.log('[Middleware] next state', store.getState());

      // return the result of the action
      return result;
    }
  }
}
```
Once defined, the middleware is registered with Redux using the `applyMiddleware()` function.  Multiple middleware functions can be passed into the `applyMiddleware()` function.

*index.js*

```jsx
import { createStore, combineReducers, applyMiddleware } from 'redux';

...etc...

const store = createStore(rootReducer, 
                  applyMiddleware(logger, other1, other2, ...etc...));

...etc...
```
</div>
</div>

<div id="redux-devtools">
<button type="button" class="collapsible">+ Redux DevTools</button>   
<div class="content" style="display: none;" markdown="1">

A useful tool for debugging Redux is the Redux DevTools extension for Chrome.  This can be found here:
   * [https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en)

Further information and instructions can be found here:
   * [https://github.com/zalmoxisus/redux-devtools-extension](https://github.com/zalmoxisus/redux-devtools-extension)

To allow this extension to debug an app, the Redux store needs to be configured in the following manner:

```jsx
import { createStore, combineReducers, 
            applyMiddleware, compose } from 'redux';

...etc...

// simple case:
// testing process.env.NODE_ENV ensures that the dev tools are disabled in production
// const store = createStore(
//   rootReducer, 
//   process.env.NODE_ENV === 'development'
//     ? typeof window !== 'undefined' && 
//     window.__REDUX_DEVTOOLS_EXTENSION__ && 
//       window.__REDUX_DEVTOOLS_EXTENSION__() : null
// );

// enhancer or middleware case:
// testing process.env.NODE_ENV ensures that the dev tools are disabled in production
const composeEnhancers =
  process.env.NODE_ENV === 'development'
    ? typeof window !== 'undefined' && window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
    : null || compose;

const store = createStore(
  rootReducer, 
  composeEnhancers(
    applyMiddleware(logger, other1, other2, ...etc...)
  )
);

...etc...
```

NOTE: the `compose` function is similar to the `combineReducers` function, however it works on enhancers and middleware, rather than reducers.

&nbsp;
&nbsp;
An alternative is the following, which allows diagnostics to be accessed programmatically in an app:
   * [https://github.com/reduxjs/redux-devtools](https://github.com/reduxjs/redux-devtools)
</div>
</div>

<div id="redux-action-creators">
<button type="button" class="collapsible">+ Action Creators</button>   
<div class="content" style="display: none;" markdown="1">
  
A more flexible approach to defining action types is to use action creators, rather than just simple properties.  This approach allows additional actions to be triggered when a particular action type is referenced.

*actions/actions.js*

```jsx
export const INCREMENT = 'INCREMENT';

export const increment = () => {
  return {
    type: INCREMENT,
  };
};
```

Now, rather than import the action types directly, the creator function is imported instead:

*Counter.js*

```jsx
import * as actionCreators from './actions/actions';

...etc...

const mapDispatchToProps = (dispatch) => {
  return {
    onIncrementCounter: () => dispatch(actionCreators.increment())
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(Counter);
```

**Note**

It is common to split the action creators into multiple files, in a similar manner to reducers:

*actions/actions.js*

```jsx
export const INCREMENT = 'INCREMENT';
export const STORE_RESULT = 'STORE_RESULT';
```

*actions/counter.js*

```jsx
import * as actionTypes from './actions';

export const increment = () => {
  return {
    type: actionTypes.INCREMENT,
  };
};
```

*actions/result.js*

```jsx
import * as actionTypes from './actions';

export const storeResult = (result) => {
  return {
    type: actionTypes.STORE_RESULT,
    result: result,
  };
};
```

These can now be imported via an intermediary index file: 

*actions/index.js*

```jsx
export {
  add,
  subtract,
  increment,
  decrement
} from './counter';

export {
  storeResult,
  deleteResult
} from './result';
```

The index file can then be imported into the files that want to reference the actions:

*Counter.js*

```jsx
import * as actionCreators from './actions/index';

...etc...
```

</div>
</div>

<div id="redux-async">
<button type="button" class="collapsible">+ Asynchronous Redux</button>   
<div class="content" style="display: none;" markdown="1">

Redux Thunk is middleware that can intercept Redux actions and then run them asynchronously.  The actions wrap functions that can be executed by the middleware, which can pass the state of the Redux store (plus other arguments) to the wrapped function.

The wrapped function is known as a `thunk`.

Further details can be found here:
   * [https://github.com/reduxjs/redux-thunk](https://github.com/reduxjs/redux-thunk)

To use Redux Thunk:

* Install: `npm install redux-thunk`
* Import: `import thunk from 'redux-thunk';`

To register `redux-thunk` as middleware, do the following:

*index.js*

```jsx
import thunk from 'redux-thunk';

...etc...

const store = createStore(
  rootReducer, 
  composeEnhancers(
    applyMiddleware(logger, thunk)
  )
);

...etc...
```

To make use of Redux Thunk, both synchronous and asynchronous versions of an action are defined, with the asynchronous version calling the synchronous version when it is ready to do so.

*actions/result.js*

```jsx
// synchronous action
// returns immediately
export const saveResult = (result) => {
  return {
    type: actionsTypes.STORE_RESULT,
    result: result,
  };
};

// asynchronous action
// returns eventually
export const storeResult = (result) => {
  // because redux-thunk is middleware,
  // the following function can be intercepted 
  // and then return the result at a
  // later time
  
  // this function is the "thunk"
  return (dispatch) => {
    // simulate a server query use setTimeout
    setTimeout(() => {
      // when the timeout ends, the dispatch
      // function calls the synchronous action.
      dispatch(saveResult(result));
    }, 2000);
  };
};
```
</div>
</div>

<div id="redux-transform-logic">
<button type="button" class="collapsible">+ Transforming Data</button>   
<div class="content" style="display: none;" markdown="1">

When transforming data/state, there are two places this can be done:

**In the Action Creator**

```jsx
export const saveResult = (result) => {

  const updatedResult = /* transform result */

  return {
    type: actionTypes.STORE_RESULT,
    result: updatedResult,
  };
};
```

This has the advantage that it can run asynchronous code, but the it goes against the core Redux concept that only reducers should update the state.

**In the Reducer**

```jsx
const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionTypes.STORE_RESULT: {
      return {
        ...state,
        results: state.results.concat(
          { 
            id: new Date(), 
            value: /* transform action.result */ 
           }
         ),
      };
    }
    default:
      return state;
  }
};
```

This has the advantage that it follows the concept that only reducers should update the state, however they can only handle pure, synchronous code.

**Which approach to use?**

In general, **transformation logic should put in the reducer**, since this is what reducers are intended for, however in some cases it may make sense to include some transformation logic in the action creator.  

For example, if the response from a server needs to be cleaned up before being passed to the rest of the logic it makes sense to do this in the action creator (which receives the raw response), however if properties of the response need to changed this should happen in the reducer (which converts the received data into state).

Avoid putting large amount of transform logic in both the reducer and the action creator, since this can make maintenance of the code difficult.

**Caveat: getState**

A feature of Redux Thunk that can make putting transform logic in the action creator more attractive is that it can pass a getState function into the action creator.  This can then be used to perform actions based on the current state.

```jsx
export const storeResult = (result) => {
  return (dispatch, getState) => {
    setTimeout(() => {
    
      const oldCounter = getState().ctr.counter;
      console.log(oldCounter);
      
      dispatch(saveResult(result));
    }, 2000);
  };
};
```

Although this is useful, it is recommended to avoid doing this too often.  If possible, it would be better to design the app so that  any state properties that are required into the action creator can be passed in as arguments instead.

</div>
</div>

<div id="redux-transform-logic">
<button type="button" class="collapsible">+ Further Redux</button>   
<div class="content" style="display: none;" markdown="1">

To delve into Redux in more depth (since it has far more uses than those discussed above), take a look at the following site:
   * [https://redux.js.org/](https://redux.js.org/)

</div>
</div>

</div>
</div>

<div id="auth">
<button type="button" class="collapsible">+ Authentication In Single Page Applications </button>   
<div class="content" style="display: none;" markdown="1">

<div id="auth-basics">
<button type="button" class="collapsible">+ Basics </button>   
<div class="content" style="display: none;" markdown="1">

1. User signs in via sign-in page
1. Authentication data is sent to server (e.g. email & password)
  * Typically any server that has a stateless RESTful API
1. Server returns a token (typically in JSON format)
1. Client stores token in local storage
1. User requests access to protected resources by passing token to server
   * Server can verify if token was created by the server

To achieve this, the client application needs the following updates:
* Sign-up & Sign-in Views
* Guarded routes (so cannot access them without being authenticated)
* Ability to pass authentication to the backend

</div>
</div>

<div id="auth-signup">
<button type="button" class="collapsible">+ Sign-Up & Sign-In Views</button>   
<div class="content" style="display: none;" markdown="1">

**Validation of Email Addresses**

See the section on <a href="#validation">Form Validation</a> for some considerations when validating email addresses.

**Implementation**

*Auth.js*

```jsx
import React, { Component } from 'react';
import { connect } from 'react-redux';

import * as actions from './actions/auth';
import Input from './Input';
import Button from './Button';
import Spinner from './Spinner';
import classes from './Auth.module.css';

class Auth extends Component {
  state = {
    controls: {
      email: {
        elementType: 'input',
        elementConfig: {
          type: 'email',
          placeholder: 'Email Address',
        },
        value: '',
        validation: {
          required: true,
          isEmail: true,
        },
        valid: false,
        touched: false,
      },
      password: {
        elementType: 'input',
        elementConfig: {
          type: 'password',
          placeholder: 'Password',
        },
        value: '',
        validation: {
          required: true,
          minLength: 6,
        },
        valid: false,
        touched: false,
      },
    },
    isSignup: true,
  };

  checkValidity(value, rules) {
    let isValid = true;

    if (rules) {
      if (rules.required) {
        isValid = value.trim() !== '' && isValid;
      }

      if (rules.minLength) {
        isValid = value.length >= rules.minLength && isValid;
      }

      if (rules.maxLength) {
        isValid = value.length <= rules.maxLength && isValid;
      }

      if (rules.isEmail) {
        const EMAIL_REGEX = /^\S+@\S+$/i;
        isValid = EMAIL_REGEX.test(value) && isValid;
      }

      if (rules.isNumeric) {
        const NUMBER_REGEX = /^\d+$/;
        isValid = NUMBER_REGEX.test(value) && isValid;
      }
    }

    return isValid;
  }

  inputChangedHandler = (event, controlName) => {
    const updatedControls = {
      ...this.state.controls,
      [controlName]: {
        ...this.state.controls[controlName],
        value: event.target.value,
        valid: this.checkValidity(event.target.value, this.state.controls[controlName].validation),
        touched: true,
      },
    };
    this.setState({ controls: updatedControls });
  };

  submitHandler = ( event ) => {
    event.preventDefault();
    this.props.onAuth( this.state.controls.email.value, this.state.controls.password.value, this.state.isSignup );
  }

  signOutHandler = (event) => {
    event.preventDefault();
    this.props.onSignOut();
  };
  
  switchAuthModeHandler = () => {
    this.setState((prevState) => {
      return { isSignup: !prevState.isSignup };
    });
  };
  
  render() {
    const formElementsArray = [];
    for (const key in this.state.controls) {
      formElementsArray.push({
        id: key,
        config: this.state.controls[key],
      });
    }

    const form = formElementsArray.map((formElement) => (
      <Input
        key={formElement.id}
        elementType={formElement.config.elementType}
        elementConfig={formElement.config.elementConfig}
        value={formElement.config.value}
        invalid={!formElement.config.valid}
        shouldValidate={formElement.config.validation}
        touched={formElement.config.touched}
        changed={(event) => this.inputChangedHandler(event, formElement.id)}
      />
    ));

    if (this.props.loading) {
      form = <Spinner />;
    }

    let errorMessage = null;
    if (this.props.error) {
      errorMessage = <p>{this.props.error}</p>;
    }

    return (
      <div className={classes.Auth}>
        {errorMessage}
        <form onSubmit={this.submitHandler}>
          {form}
          <Button btnType="Success">SUBMIT</Button>
        </form>
        <Button clicked={this.switchAuthModeHandler} btnType="Danger">
          SWITCH TO {this.state.isSignup ? 'SIGN-IN' : 'SIGN-UP'}
        </Button>
        <Button clicked={this.signOutHandler} btnType="Success">
          SIGN OUT
        </Button>
      </div>
    );
  }
}

const mapStateToProps = (state) => {
  return {
    loading: state.auth.loading,
    error: state.auth.error,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    onAuth: (email, password, isSignup) => dispatch(actions.auth(email, password, isSignup)),
    onSignOut: () => dispatch(actions.signOut()),
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(Auth);

```

*App.js*

```jsx
import React, { Component } from 'react';
import { Switch, Route, Redirect } from 'react-router-dom';
import Auth from './Auth';

class App extends Component {

  render() {
    return (
      <div>
        <Layout>
          <Switch>
            ...etc...
            <Route path="/auth" component={Auth} />
            ...etc...
          </Switch>
        </Layout>
      </div>
    );
  }
}

export default App;
```

*actions/actionTypes.js*

```jsx
export const AUTH_START = 'AUTH_START';
export const AUTH_SUCCESS = 'AUTH_SUCCESS';
export const AUTH_FAIL = 'AUTH_FAIL';
export const AUTH_SIGN_OUT = 'AUTH_SIGN_OUT';
```

*actions/auth.js*

```jsx
import * as actionTypes from './actionTypes';

export const authStart = () => {
  return {
    type: actionTypes.AUTH_START,
  };
};

export const authSuccess = (authData) => {
  return {
    type: actionTypes.AUTH_SUCCESS,
    authData: authData,
  };
};

export const authFail = (error) => {
  return {
    type: actionTypes.AUTH_FAIL,
    error: error,
  };
};

export const authSignOut = () => {
  return {
    type: actionTypes.AUTH_SIGN_OUT,
  };
};

export const auth = (email, password, isSignup) => {
  return (dispatch) => {
    dispatch(authStart());
    
    /* authentication action will go here */
    
  };
};

export const signOut = () => {
  return (dispatch) => {
  
    /* sign-out action will go here */
    
  };
};
```

*reducers/auth.js*

```jsx
import * as actionTypes from '../actions/actionTypes';
import { updateObject } from '../utility';

const initialState = {
  authData: null,
  error: null,
  loading: false,
};

const authStart = (state, action) => {
  return updateObject(state, { error: null, loading: true });
};

const authSuccess = (state, action) => {
  return updateObject(state, {
    authData: action.authData,
    error: null,
    loading: false,
  });
};

const authFail = (state, action) => {
  return updateObject(state, { error: action.error, loading: false });
};

const authSignOut = (state, action) => {
  return updateObject(state, initialState);
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionTypes.AUTH_START: {
      return authStart(state, action);
    }
    case actionTypes.AUTH_SUCCESS: {
      return authSuccess(state, action);
    }
    case actionTypes.AUTH_FAIL: {
      return authFail(state, action);
    }
    case actionTypes.AUTH_SIGN_OUT: {
      return authSignOut(state, action);
    }
    default:
      return state;
  }
};

export default reducer;
```

*index.js*

```jsx

...etc...

import authReducer from './reducers/auth';

...etc...

const rootReducer = combineReducers({
  ...etc...
  auth: authReducer,
});

const store = createStore(rootReducer, ...etc...);

...etc...
```

</div>
</div>

<div id="auth-firebase">
<button type="button" class="collapsible">+ Firebase Authentication </button>   
<div class="content" style="display: none;" markdown="1">

Reference information for authentication in Firebase can be found here:
* [https://firebase.google.com/docs/reference/rest/auth](https://firebase.google.com/docs/reference/rest/auth)

The Firebase module needs to be installed:
* Install: `npm install firebase`
* Import: `import firebase from 'firebase/app'; import 'firebase/auth';`

NOTE: It is recommended that you only the packages you actually need, rather than importing the entire Firebase module.

**Register App With Firebase**

Before performing authentication using firebase, the application needs to be registered with the project.  The current steps to do this are:
1. Open the Firebase control panel for the project
1. Open "Project Overview" (top-left)
1. Click "+ Add app" (just under the project name, in the main panel)
1. Click "</>" (for web app)
1. When prompted, give the app a nickname and click "Register app".
1. Further information will be provided regarding installing and using the SDK, however this can be ignored for the following purposes.

The configuration details for the Firebase connection can be obtained from:
1. Open "Project settings" (the cog, in the top left)
1. Scroll down to identify the web app
1. Under "Firebase SDK snippet", click "Config"
1. Copy the snippet into `auth.js`

**Implementation**

*App.js*

```jsx
import React, { Component } from 'react';
import { Switch, Route, Redirect } from 'react-router-dom';
import firebase from 'firebase/app';
import 'firebase/auth';
import Auth from './Auth';

class App extends Component {

  // this will be triggered the first time the page is
  // rendered
  componentDidMount() {
    firebase.auth().onAuthStateChanged(function (user) {
      if (user) {
        console.log('Authenticated!', user);
      } else {
        console.log('Denied!');
        // No user is signed in.
      }
    });
  }

  render() {
    return (
      <div>
        <Layout>
          <Switch>
            ...etc...
            <Route path="/auth" component={Auth} />
            ...etc...
          </Switch>
        </Layout>
      </div>
    );
  }
}

export default App;
```

*reducers/auth.js*

```jsx
...etc...

const initialState = {
  user: null,
  error: null,
  loading: false,
};

...etc...

const authSuccess = (state, action) => {
  return updateObject(state, {
    user: action.user,
    error: null,
    loading: false,
  });
};

...etc...
```

*actions/auth.js*

```jsx
// import the Firebase authentication package
import firebase from 'firebase/app';
import 'firebase/auth';

// for security, store config in a separate file
// and exclude this from source control.
import { firebaseConfig } from '../firebase-config';

// initialize connection to firebase
const fire = firebase.initializeApp(firebaseConfig);

export const authStart = () => { ...etc... };

export const authSuccess = (user) => {
  return {
    type: actionTypes.AUTH_SUCCESS,
    user: user,
  };
};

export const authFail = (error) => { ...etc... };

export const authSignOut = () => { ...etc... };

export const auth = (email, password, isSignup) => {

  let doAuth = (email, password) => {
    return fire.auth().createUserWithEmailAndPassword(email, password);
  };

  if (!isSignUp) {
    doAuth = (email, password) => {
      return fire.auth().signInWithEmailAndPassword(email, password);
    };
  }

  return (dispatch) => {
    dispatch(authStart());

    doAuth(email, password)
      .then((response) => {
        dispatch(authSuccess(response.user));
      })
      .catch((err) => {
        console.log(err);
        dispatch(authFail(err.message));
      });
  };
};

export const signOut = () => {
  return (dispatch) => {
    fire
      .auth()
      .signOut()
      .then((response) => {
        dispatch(authSignOut());
      })
      .catch((err) => {
        console.log(err);
        dispatch(authFail(err));
      });
  };
};
```

*firebase-config.js*

```jsx
// Obtain configuration from "Project Settings" 
// in Firebase console
export const firebaseConfig = {
  apiKey: '...',
  authDomain: '...',
  databaseURL: '...',
  projectId: '...',
  storageBucket: '...',
  messagingSenderId: '...',
  appId: '...',
  measurementId: '...',
};
```

**Securing the Firebase Config**

The Firebase configuration settings are not designed to be hidden; no matter what steps you take, the settings will be publically available once loaded into a browser.

In any event, if you want to avoid making the configuration accessible in source control, the standard approach is to store the config in a separate file.  This file can then be excluded from source control.  

In the case of git, add the following to `.gitignore`:

* `relative/path/to/fire.js`

Rather than obfuscation, Firebase security depends on the correct access permissions being setup for the project.  There are two main steps that should be taken:
1. Configure the database to only allow connections from the production domain.
   * For localhost testing, create a separate database instance under a different google id.
1. Setup proper access rules for the database and storage.

These steps are discussed in greater depth in the following document:
* [https://medium.com/@impaachu/how-to-secure-your-firebase-project-even-when-your-api-key-is-publicly-available-a462a2a58843](https://medium.com/@impaachu/how-to-secure-your-firebase-project-even-when-your-api-key-is-publicly-available-a462a2a58843)

</div>
</div>

<div id="auth-generic">
<button type="button" class="collapsible">+ Generic Authentication </button>   
<div class="content" style="display: none;" markdown="1">

In the case of other backends, a more generic approach is to use Axios.

**Implementation**

*reducers/auth.js*

```jsx
...etc...

const initialState = {
  token: null,
  userId: null,
  error: null,
  loading: false,
};

...etc...

const authSuccess = (state, action) => {
  return updateObject(state, {
    token: action.idToken,
    userId: action.userId,
    error: null,
    loading: false,
  });
};

...etc...
```

*actions/auth.js*

```jsx
import axios from 'axios';

export const authStart = () => { ...etc... };

export const authSuccess = (token, userId) => {
  return {
    type: actionTypes.AUTH_SUCCESS,
    idToken: token,
    userId: userId
  };
};

export const authFail = (error) => { ...etc... };

// may need to handle token timeout internally, if not 
// handled by backend
export const checkAuthTimeout = (expirationTimeout) => {
  return dispatch => {
    setTimeout(() => {
      dispatch(authSignOut())
    }, expirationTimeout * 1000) // seconds to ms
  };
};

export const authSignOut = () => { ...etc... };

export const auth = (email, password, isSignup) => {
  return (dispatch) => {
    dispatch(authStart());

    // check API docs for URLs
    let url = isSignup ? "[signup-end-point-url]" : "[signin-end-point-url]";
    
    // check API docs for payload contents
    const authData = {
      email: email,
      password: password,
    };

    axios
      .post(
        url,
        authData
      )
      .then((response) => {
        dispatch(authSuccess(response.data.idToken, response.data.localId));
        dispatch(checkAuthTimeout(response.data.expiresIn));
      })
      .catch((err) => {
        console.log(err);
        dispatch(authFail(err));
      });
  };
};

export const signOut = () => {
  return (dispatch) => {
  
    // check API docs for URLs
    axios
      .post(
        [signout-end-point-url]
      )
      .then((response) => {
        dispatch(authSignOut());
      })
      .catch((err) => {
        console.log(err);
        dispatch(authFail(err));
      });
  };
};
```

**Tokens**

The tokens used to prove authentication are typically JWT tokens, which has the following format:

`header.payload.public_key`

For example, the following is a token, which is base64-encoded:

```
eyJhbGciOiJSUzI1NiIsImtpZCI6IjIxODQ1OWJiYTE2NGJiN2I5MWMzMjhmOD
kxZjBiNTY1M2UzYjM4YmYiLCJ0eXAiOiJKV1QifQ.
eyJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vcmVhY3QtbX
ktYnVyZ2VyLTJkN2M2IiwiYXVkIjoicmVhY3QtbXktYnVyZ2VyLTJkN2M2Iiwi
YXV0aF90aW1lIjoxNTk0NzM3MTg3LCJ1c2VyX2lkIjoiNm5Zb0hMZ2lDOFI2RH
hIOEQ1RjZtRnZmNmhWMiIsInN1YiI6IjZuWW9ITGdpQzhSNkR4SDhENUY2bUZ2
ZjZoVjIiLCJpYXQiOjE1OTQ3MzcxODcsImV4cCI6MTU5NDc0MDc4NywiZW1haW
wiOiJ0ZXN0QGhlcmUuY29tIiwiZW1haWxfdmVyaWZpZWQiOmZhbHNlLCJmaXJl
YmFzZSI6eyJpZGVudGl0aWVzIjp7ImVtYWlsIjpbInRlc3RAaGVyZS5jb20iXX
0sInNpZ25faW5fcHJvdmlkZXIiOiJwYXNzd29yZCJ9fQ.
g_JNsytt0u838Q4tzo5VT0tH9lj7cfzx_zJm7VDZfxs0kss0vy5Zxq4NEysNCY
DSgGbPGCOHIQ8xmxM7D_AAyy3gnNY9mgroV88Zzudyk4CFjGVrwT0HAfSah0BK
nXyteD_mGOzqB52xzw-kauHp7_zctnXWuuonF0X6PEGac_8TQr9aW3wRQDQLs7
fjWTRDCB-DZKsMLVzpTuqoXq7Nx0J1-tzmpElIxL7veoNVyIolCvVERnuroeUk
ypO37Ni15PdNwwlYXLxrd63HTpmp4HHjORdi5StQb2AAzLtZ27nyJMFcHzhTm-
NV-LCLCGbtKTSmrsUNIrTShf9UQNw5sw
```

When decoded, the contents of the tokn are the following:

```
[header]
{
  "alg": "RS256",
  "kid": "218459bba164bb7b91c328f891f0b5653e3b38bf",
  "typ": "JWT"
}

[payload]
{
  "iss": "https://securetoken.google.com/react-my-burger-2d7c6",
  "aud": "react-my-burger-2d7c6",
  "auth_time": 1594737187,
  "user_id": "6nYoHLgiC8R6DxH8D5F6mFvf6hV2",
  "sub": "6nYoHLgiC8R6DxH8D5F6mFvf6hV2",
  "iat": 1594737187,
  "exp": 1594740787,
  "email": "test@here.com",
  "email_verified": false,
  "firebase": {
    "identities": {
      "email": [
        "test@here.com"
      ]
    },
    "sign_in_provider": "password"
  }
}

[public key]
{
  ...etc...
}
```
</div>
</div>

<div id="auth-protected-firebase">
<button type="button" class="collapsible">+ Accessing Protected Resources: Firebase Configuration </button>   
<div class="content" style="display: none;" markdown="1">

In Firebase, authenticated access to protected resources is controlled by rules.  These are set in the control panel via "Database" -> "Rules".

In the fully unprotected case, the rules look something like the following:

```json
{
  "rules": {
    ".read": "true",
    ".write": "true"
  }
}
```

Alternatively, in the fully protected case, the rules look like this:

```json
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

For a more nuanced approach, the rules can be applied on a node-by-node basis.  

Taking the example of the following database scheme:

* react-my-burger-2d7c6
   * ingredients
   * orders

To give unrestricted access to the ingredients while restricting access to the orders, the rules can be applied in the following manner:

```json
{
  "rules": {
    "ingredients": {
      ".read": "true",
      ".write": "true",
    },
    "orders": {
      ".read": "auth != null",
      ".write": "auth != null",
    }
  }
}
```
</div>
</div>

<div id="auth-protected-login">
<button type="button" class="collapsible">+ Accessing Protected Resources: Authentication</button>   
<div class="content" style="display: none;" markdown="1">

Assuming the Firebase instance is correctly configured, authenticatation is achieved by the user logging in and then obtaining a token.  The token is then passed around to prove the user has been authenticated.

*actions/auth.js*

* Define an action to authenticate the user.  If successful, this returns an token.

```jsx
export const authSuccess = (user, token) => {
  return {
    type: actionTypes.AUTH_SUCCESS,
    user: user,
    token: token,
  };
};

export const auth = (email, password, isSignUp) => {
  return (dispatch) => {
    dispatch(authStart());

    fire.auth().signInWithEmailAndPassword(email, password)
      .then((response) => {
        response.user.getIdToken().then((token) => {
          dispatch(authSuccess(response.user, token));
        });
      })
      .catch((err) => {
        console.log(err);
        dispatch(authFail(err.message));
      });
  };
};

```

*reducers/auth.js*

* Define a reducer that updates the store with the token.

```jsx
...etc...

const initialState = {
  user: null,
  token: null,
  error: null,
  loading: false,
};

...etc...

const authSuccess = (state, action) => {
  return updateObject(state, {
    user: action.user,
    token: action.token,
    error: null,
    loading: false,
  });
};

...etc...
```

*Orders.js*

* Obtain the token from the store and pass it where necessary 

```jsx

...etc...

class Orders extends Component {
  componentDidMount() {
    this.props.onFetchOrders(this.props.token);
  }
  
  ...etc...
}

const mapStateToProps = (state) => {
  return {
    token: state.auth.token,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    onFetchOrders: (token) => dispatch(actions.fetchOrders(token)),
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(Orders, axios);
```

*Order.js*

* Obtain the token from the store and pass it where necessary 

```jsx
...etc...

class Order extends Component {

  orderHandler = (event) => {
  
    const order = {
      ...etc...
    };

    this.props.onOrderBurger(order, this.props.token);
  };

  ...etc...

  render() {
    let form = (
      <form onSubmit={this.orderHandler}>
        ...etc...    
      </form>
    );
    
    return (
      <div>
        {form}
      </div>
    );
  }
}

const mapStateToProps = (state) => {
  return {
    token: state.auth.token,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    onOrderBurger: (orderData, token) => dispatch(actions.purchaseBurger(orderData, token)),
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(Order, axios);
```

Finally, the token is passed to the backend via the endpoint URL:

*actions/order.js*

* Pass the token to the Firebase database when data is to be read or written

```jsx
...etc...

export const purchaseBurger = (orderData, token) => {
  return (dispatch) => {
    dispatch(purchaseBurgerStart());
    axios
      .post('/orders.json?auth=' + token, orderData)
      .then((response) => {
        dispatch(purchaseBurgerSuccess(response.data.name, orderData));
      })
      .catch((error) => {
        dispatch(purchaseBurgerFail(error));
      });
  };
};

...etc...

export const fetchOrders = (token) => {
  return (dispatch) => {
    dispatch(fetchOrdersStart());
    axios
      .get('/orders.json?auth=' + token)
      .then((response) => {
        const fetchedOrders = [];

        if (response && response.data) {
          for (const key in response.data) {
            fetchedOrders.push({
              ...response.data[key],
              id: key,
            });
          }
        }

        dispatch(fetchOrdersSuccess(fetchedOrders));
      })
      .catch((error) => {
        dispatch(fetchOrdersFail(error));
      });
  };
};

...etc...

```

</div>
</div>

<div id="use-auth">
<button type="button" class="collapsible">+ Reacting to Authentication State: Logout</button>   
<div class="content" style="display: none;" markdown="1">

The simplest test for whether a user is authenticated is to check if they have a token.  In the following example, the simple case of displaying either a Login or Logout button is demonstrated.

*Logout.js*

* First create a Logout component that can be reused whereever necessary.  This calls the signOut action and then redirects to root.

```jsx
import React, { Component } from 'react';
import { Redirect } from 'react-router-dom';
import { connect } from 'react-redux';

import * as actions from './actions/auth';

class Logout extends Component {
  componentDidMount() {
    this.props.onSignOut();
  }

  render() {
    return <Redirect to="/" />;
  }
}

const mapDispatchToProps = (dispatch) => {
  return {
    onSignOut: () => dispatch(actions.signOut()),
  };
};

export default connect(null, mapDispatchToProps)(Logout);
```

*actions/auth.js*

* The signOut action is exposed here.  This calls the signOut function on the Firebase auth API, and then call returns AUTH_SIGN_OUT if it was successful.

```jsx
import * as actionTypes from './actionTypes';

...etc...

export const authSignOut = () => {
  return {
    type: actionTypes.AUTH_SIGN_OUT,
  };
};

...etc...

export const signOut = () => {
  return (dispatch) => {
    fire
      .auth()
      .signOut()
      .then((response) => {
        console.log('SignOut', response);
        dispatch(authSignOut());
      })
      .catch((err) => {
        console.log(err);
        dispatch(authFail(err));
      });
  };
};
```

*actions/actionTypes.js*

* AUTH_SIGN_OUT is defined here.

```jsx
...etc...

export const AUTH_SIGN_OUT = 'AUTH_SIGN_OUT';

...etc...
```

*reducers/auth.js*

* Resets the Redux store to its initial state (i.e. sets token to null)

```jsx
...etc...

const initialState = {
  user: null,
  token: null,
  error: null,
  loading: false,
};

const updateObject = (oldObject, updatedProperties) => {
  return {
    ...oldObject,
    ...updatedProperties,
  };
};

const authSignOut = (state, action) => {
  return updateObject(state, initialState);
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    
    ...etc...
    
    case actionTypes.AUTH_SIGN_OUT: {
      return authSignOut(state, action);
    }
    
    ...etc...
  }
};

...etc...
```

*App.js*

* The Logout component can be placed wherever the option to sign-out is required.  Here, a redirect is used to forward the `/logout` path to the sign-out routine.

```jsx
...etc...
import Logout from './Logout';

class App extends Component {

  render() {
    return (
      <div>
        <Layout>
          <Switch>
            ...etc...
            <Route path="/logout" component={Logout} />
            ...etc...
          </Switch>
        </Layout>
      </div>
    );
  }
}
...etc...
```

*Layout.js*

* Generally, the authentication state is passed down from a higher-level class component to lower-level functional components.

```jsx
import React, { Component } from 'react';
import { connect } from 'react-redux';
import Toolbar from './Toolbar';

...etc...

class Layout extends Component {
  ...etc...
  
  render() {
    return (
      <Wrapper>
        <Toolbar isAuth={this.props.isAuthenticated} ...etc... />
      </Wrapper>
    );
  }
}

const mapStateToProps = (state) => {
  return {
    isAuthenticated: state.auth.token !== null,
  };
};

export default connect(mapStateToProps)(Layout);
```

*Toolbar.js*

```jsx
import React from 'react';
import NavigationItems from './NavigationItems';
...etc...

const Toolbar = (props) => (
  <header className={classes.Toolbar}>
  
    ...etc...
  
    <nav className={classes.DesktopOnly}>
      <NavigationItems isAuthenticated={props.isAuth} />
    </nav>
  </header>
);

export default Toolbar;

```

*NavigationItems.js*

* Here, we can simply test props.isAuthenticated

```jsx
const NavigationItems = (props) => (
  <ul className={classes.NavigationItems}>
    {props.isAuthenticated ? (
      <NavigationItem link="/logout">Logout</NavigationItem>
    ) : (
      <NavigationItem link="/auth">Login</NavigationItem>
    )}
  </ul>
);

export default NavigationItems;
```

</div>
</div>

<div id="use-auth">
<button type="button" class="collapsible">+ Reacting to Authentication State: Redirect</button>   
<div class="content" style="display: none;" markdown="1">

Depending on the authentication state, the user may need to be redirected to different pages.  For example, if the user builds a burger and want to checkout, they may need to be directed to either the checkout page or the login page, depending on whether they are logged in or not. 

*actions/actionTypes.js*

* Add an action type for setting the post-authentication redirect path.

```jsx
...etc...
export const SET_AUTH_REDIRECT_PATH = 'SET_AUTH_REDIRECT_PATH';
...etc...
```

*reducers/auth.js*

* Add a reducer

```jsx
const initialState = {
  ...etc...
  authRedirectPath: '/',
};

...etc...

const setAuthRedirectPath = (state, action) => {
  return updateObject(state, { authRedirectPath: action.path });
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    ...etc...
    
    case actionTypes.SET_AUTH_REDIRECT_PATH: {
      return setAuthRedirectPath(state, action);
    }
    default:
      return state;
  }
};
```

*actions/auth.js*

* Add action that indicates that the post-authorization redirect path needs to be changed.

```jsx

...etc...

// set the path to be redirected to after authentication
export const setAuthRedirectPath = (path) => {
  return {
    type: actionTypes.SET_AUTH_REDIRECT_PATH,
    path: path,
  };
};

...etc...

```
*Auth.js*

* During authentication, ensure that the redirect path is set correctly (essentially, if the user has not yet built a burger, go to root, otherwise go to elsewhere (e.g. checkout))

```jsx
...etc...
import { Redirect } from 'react-router-dom';

class Auth extends Component {
  ...etc...
  
  componentDidMount() {
    // if user is not building a burger, and the redirect path is not root,
    // set the redirect path to root
    if (!this.props.buildingBurger && this.props.authRedirectPath !== '/') {
      this.props.onSetAuthRedirectPath();
    }
  }
  
  ...etc...
  
  render() {
  {
    // create redirect component (initially set to null, so ignored)
    let authRedirect = null;
    if (this.props.isAuthenticated) {
      authRedirect = <Redirect to={this.props.authRedirectPath} />;
    }

    return (
      <div className={classes.Auth}>
        {authRedirect} // redirect if not null

        ...etc...
      </div>
    );
  }
}

const mapStateToProps = (state) => {
  return {
    ...etc...
    // authentication test
    isAuthenticated: state.auth.token !== null,
    // if true, users wants to go to authRedirectPath
    buildingBurger: state.burgerBuilder.building, 
    // the path to be redirected to
    authRedirectPath: state.auth.authRedirectPath,
  };
};

// expose action that will reset the redirect path to root
const mapDispatchToProps = (dispatch) => {
  return {
    ...etc...
    onSetAuthRedirectPath: () => dispatch(actions.setAuthRedirectPath('/')),
  };
};
```

*reducers/burgerBuilder.js*

* Add a flag to indicate whether or not the user is building a burger (which determines whether the user should be redirected the checkout or not)

```jsx
...etc...

const initialState = {
  ...etc...
  building: false,
};

...etc...

const addIngredientHandler = (state, ingredientType) => {
  ...etc...

  const updatedState = {
    ...etc...
    building: true,
  };
  return updateObject(state, updatedState);
};

const removeIngredientHandler = (state, ingredientType) => {
  ...etc...

  const updatedState = {
    ...etc...
    building: true,
  };
  return updateObject(state, updatedState);
};

const setIngredientsHandler = (state, updatedIngredients) => {

  ...etc...
  
  return updateObject(state, {
    ...etc...
    building: false,
  });
};

...etc...
```

*BurgerBuilder.js*

* If user is successully authenticated, allow them to go to the checkout, otherwise redirect them to the login page.

```jsx
...etc...

class BurgerBuilder extends Component {
  ...etc...
  
  purchaseHandler = () => {
    if (this.props.isAuthenticated) {
    // if user is already authenticated, send them straight
    // to the checkout
      this.setState({ purchasing: true });
    } else {
      // redirect user to login page, and then,
      // if successful, redirect them to the checkout 
      this.props.onSetAuthRedirectPath('/checkout');
      this.props.history.push('/auth');
    }
  };

  render() {
    ...etc...

    if (this.props.ingredients) {
      burger = (
        <Wrapper>
          ...etc...
        
          <BuildControls
            ...etc...
            isAuth={this.props.isAuthenticated}
          />
        </Wrapper>
      );
      
      ...etc...
    }

    return (
      <Wrapper>
        ...etc...
        
        {burger}
      </Wrapper>
    );
  }
}

const mapStateToProps = (state) => {
  if (state) {
    return {
      ...etc...
      isAuthenticated: state.auth.token !== null,
    };
  } else {
    return null;
  }
};

const mapDispatchToProps = (dispatch) => {
  return {
    ...etc...
    onSetAuthRedirectPath: (path) => dispatch(actions.setAuthRedirectPath(path)),
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(withErrorHandler(BurgerBuilder, axios));
```

*BuildControls.js*

* Change the state of the order button depending on whether or not the user is authenticated.

```jsx
...etc...

const BuildControls = (props) => (
  <div className={classes.BuildControls}>
    ...etc...

    <button
      ...etc...
    >
      {props.isAuth ? 'ORDER NOW' : 'LOGIN TO ORDER'}
    </button>
  </div>
);

export default BuildControls;
```

</div>
</div>

<div id="persist-auth">
<button type="button" class="collapsible">+ Persisting Authentication State</button>   
<div class="content" style="display: none;" markdown="1">

If the authentication state is not persisted, refreshing the page will reset the application state.  To avoid this, a standard browser API is used: `localStorage`

*actions/auth.js*

* Write authentication state to localStorage.  Also add functions to test what current authentication state is.

```jsx

...etc...

const AUTH_TOKEN = 'AUTH_TOKEN';
const AUTH_TOKEN_EXPIRATION = 'AUTH_TOKEN_EXPIRATION';
const AUTH_USER_ID = 'AUTH_USER_ID';

...etc...

// remove the token from localStorage when the user logs out
export const authSignOut = () => {
  removeTokenFromLocalStorage();
  return {
    type: actionTypes.AUTH_SIGN_OUT,
  };
};

// get the expiration date from the token
const getExpirationDate = (jwtToken) => {
  if (!jwtToken) {
    return null;
  }

  // token format: header.payload.public_key
  // extract payload (payload.exp = expiry time)
  const jwt = JSON.parse(atob(jwtToken.split('.')[1]));

  // multiply by 1000 to convert seconds into milliseconds
  return (jwt && jwt.exp && jwt.exp * 1000) || null;
};

// check if the token expiry time has passed
const isExpired = (expiryTime) => {
  if (!expiryTime) {
    return false;
  }
  return Date.now() > expiryTime;
};

// write the token to localStorage
// (or remove it if token is not found)
const writeTokenToLocalStorage = (user, token) => {
  if (token) {
    const expirationDate = getExpirationDate(token);

    // if using JSON.stringify() when writing to localStorage, 
    // need to remember to use JSON.parse() when reading values from localStorage
    localStorage.setItem(AUTH_TOKEN, JSON.stringify(token));
    localStorage.setItem(AUTH_TOKEN_EXPIRATION, JSON.stringify(expirationDate));
    localStorage.setItem(AUTH_USER_ID, JSON.stringify(user));
  } else {
    removeTokenFromLocalStorage();
  }
};

// delete the token from localStorage
const removeTokenFromLocalStorage = () => {
  localStorage.removeItem(AUTH_TOKEN);
  localStorage.removeItem(AUTH_TOKEN_EXPIRATION);
  localStorage.removeItem(AUTH_USER_ID);
};

// send the user's credentials to the Firebase instance for authentication
// and then store the returned token if successful
export const auth = (email, password, isSignUp) => {
  let doAuth = (email, password) => {
    return fire.auth().createUserWithEmailAndPassword(email, password);
  };

  if (!isSignUp) {
    doAuth = (email, password) => {
      return fire.auth().signInWithEmailAndPassword(email, password);
    };
  }

  return (dispatch) => {
    dispatch(authStart());

    doAuth(email, password)
      .then((response) => {
        response.user.getIdToken().then((token) => {
          writeTokenToLocalStorage(response.user, token);
          dispatch(authSuccess(response.user, token));
        });
      })
      .catch((err) => {
        console.log(err);
        dispatch(authFail(err.message));
      });
  };
};

// Check the current state of the authentication.
// If token cannot be found in localStorage, or
// it has expired, sign-out, else reconfirm that
// authentication is successful.
export const authCheckState = () => {
  return (dispatch) => {

    // if using JSON.stringify() when writing to localStorage, 
    // need to remember to use JSON.parse() when reading values from localStorage
    const token = JSON.parse(localStorage.getItem(AUTH_TOKEN));
    
    if (!token) {
      dispatch(signOut());
    } else {
      const expirationDate = JSON.parse(localStorage.getItem(AUTH_TOKEN_EXPIRATION));
      if (isExpired(expirationDate)) {
        dispatch(signOut());
      } else {
        const userId = JSON.parse(localStorage.getItem(AUTH_USER_ID));
        dispatch(authSuccess(userId, token));
      }
    }
  };
};

```

*App.js*

* When main app is mounted, test the current authentication state.

```jsx
...etc...
import { Switch, Route, Redirect, withRouter } from 'react-router-dom';
import { connect } from 'react-redux';
import * as actions from './actions/auth';

class App extends Component {

  // when component mounts, test whether user is authenticated
  componentDidMount() {
    this.props.onTryAutoSignup();
  }
  
  ...etc...

}

// get action for testing authentication state
const mapDispatchToProps = (dispatch) => {
  return {
    onTryAutoSignup: () => dispatch(actions.authCheckState()),
  };
};

// use withRouter to ensure that props get passed to App
export default withRouter(connect(null, mapDispatchToProps)(App));
```

</div>
</div>

<div id="auth-sec">
<button type="button" class="collapsible">+ App Security Warning: Refresh Token</button>   
<div class="content" style="display: none;" markdown="1">

Along with the access token that is received by the app, a refresh token is also received.  Unlike the access token, the refresh token never expires, which means that it can be used to automatically refresh the user's session, rather than requiring them to login again.

On the face of it, this offers a better user experience, however it is not recommended to do this.  

If the refresh token is persisted in local storage, there is a risk of [Cross-Site Scripting](https://codeburst.io/web-storage-and-xss-attacks-4f83b0d08725) (XSS) attacks.  While the access token is also at risk of this, the fact that it expires means it is less of a risk.  Since the refresh token never expires, theoretically this gives someone unlimited access to the app resources.

</div>
</div>

<div id="auth-guarded-routes">
<button type="button" class="collapsible">+ Guarded Route</button>   
<div class="content" style="display: none;" markdown="1">

A Guarded Route is essentially one that does not get rendered to the UI except under a specific condition, e.g. if the user is logged in.

**NOTE**: A Guarded Route only protects the user from accidentally accessing pages they shouldn't; it does not prevent a determined user from digging down into the app javascript source code and viewing the pages (since the source code is always sent to the browser).  This is why server-side access permissions are used to control access to the data.

*App.js*

* Only render the checkout, orders and logout pages if the user is logged in.  Also, redirect the user to a warning page if they are not logged in.

```jsx
...etc...

class App extends Component {

  ...etc...

  render() {
    let routes = (
      <Switch>
        <Route path="/auth" component={Auth} />
        <Route path="/burger" exact component={BurgerBuilder} />
        <Redirect from="/" to="/burger" />
        <Redirect to="/" /> {/* this could also redirect to a 404 or 403 page */}
      </Switch>
    );

    if (this.props.isAuthenticated) {
      routes = (
        <Switch>
          <Switch>
            <Route path="/orders" component={Orders} />
            <Route path="/checkout" component={Checkout} />
            <Route path="/logout" component={Logout} />
            <Route path="/burger" exact component={BurgerBuilder} />
            <Redirect from="/" to="/burger" />
          </Switch>
        </Switch>
      );
    }

    return (
      <div>
        <Layout>
          {routes}
        </Layout>
      </div>
    );
  }
}

const mapStateToProps = (state) => {
  return {
    isAuthenticated: state.auth.token !== null,
  };
};

...etc...

export default withRouter(connect(mapStateToProps, mapDispatchToProps)(App));
```

</div>
</div>

<div id="auth-guarded-routes">
<button type="button" class="collapsible">+ Filtering Returned Data</button>   
<div class="content" style="display: none;" markdown="1">

If the results from the backend are not filtered, there is a risk that data belonging to other users will be displayed to the current user.  Consequently we want to make sure we only return the current user's data.

In the case of Firebase, this is achieved using the backend's REST API; specifically, the `orderBy` and `equalTo` properties.

**Firebase Configuration**

To enable this filtering in Firebase, an additional `.indexOn` rule must be added to the database rules:

```json
{
  "rules": {
    "ingredients": {
      ".read": "true",
      ".write": "true",
    },
    "orders": {
      ".read": "auth != null",
      ".write": "auth != null",
      ".indexOn": ["userId"]
    }
  }
}
```

Note that `.indexOn` can accept an array of keys to index, although in this case we are only interested in `userId`.

**Code Example**

*actions/order.js*

* Append `&orderBy="key"&equalTo="value"` to the API (note the double-quotes!).  In this case, the key is `userId`.

```jsx
...etc...

export const fetchOrders = (token, userId) => {
  return (dispatch) => {
    dispatch(fetchOrdersStart());
    
    const queryParams = '?auth=' + token + '&orderBy="userId"&equalTo="' + userId + '"';
    axios
      .get('/orders.json' + queryParams)
      .then((response) => {
          ...etc...
        }
        
        dispatch(fetchOrdersSuccess(fetchedOrders));
      })
      .catch((error) => {
        dispatch(fetchOrdersFail(error));
      });
  };
};
```

*ContactData.js*

* Ensure that the userId is included in the order data sent to the backend.

```jsx
...etc...

class ContactData extends Component {
  
  ...etc...
  
  orderHandler = (event) => {
    ...etc...

    const order = {
      ...etc...
      userId: this.props.userId,
    };

    this.props.onOrderBurger(order, this.props.token);
  };

  ...etc...
}

const mapStateToProps = (state) => {
  return {
    ...etc...
    userId: state.auth.userId,
  };
};

...etc...
```

*Orders.js*

* Ensure that userId is included in data passed to the database query

```jsx
...etc...

class Orders extends Component {
  componentDidMount() {
    this.props.onFetchOrders(this.props.token, this.props.userId);
  }

  ...etc...
}

const mapStateToProps = (state) => {
  return {
    ...etc...
    userId: state.auth.userId,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    onFetchOrders: (token, userId) => dispatch(actions.fetchOrders(token, userId)),
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(withErrorHandler(Orders, axios));
```

</div>
</div>

**Further Information**

* [General SPA Authentication](https://stormpath.com/blog/token-auth-spa)
* [Firebase Authentication REST API](https://firebase.google.com/docs/reference/rest/auth/)

</div>
</div>

<div id="testing">
<button type="button" class="collapsible">+ Testing Overview</button>   
<div class="content" style="display: none;" markdown="1">

<div id="test-tools">
<button type="button" class="collapsible">+ Testing Tools</button>   
<div class="content" style="display: none;" markdown="1">
  
To perform testing of React code, two tools are required:

**Test Runner**

The Test Runner executes the tests and provides validation tools.  The most commonly used one is Jest, since is included in the default create-react-app install.

The documentation for Jest can be found here: 
* [https://jestjs.io/](https://jestjs.io/)

There is an extension that integrates Jest into VS Code, further details regarding which can be found here:
* [https://github.com/jest-community/vscode-jest](https://github.com/jest-community/vscode-jest)


NOTE: Although the following is concerned with React, Jest can be installed manually for any JavaScript project.

* Install: `npm install --save-dev jest`
* Import: [none required]


**Testing Utility**

The Testing Utility "simulates" the React App (i.e. it mounts components), which allows the DOM to be accessed.  Examples include React Test Utils and Enzyme.

The following will concentrate on Enzyme, the documentation for which can be found here:
*  [https://enzymejs.github.io/enzyme/](https://enzymejs.github.io/enzyme/)

* Install: `npm install --save enzyme react-test-renderer enzyme-adapter-react-16`
* Import: `import { configure, shallow } from 'enzyme'; import Adapter from 'enzyme-adapter-react-16';`

</div>
</div>

<div id="test-basic">
<button type="button" class="collapsible">+ Basic Test Implementation (using Enzyme &amp; Jest)</button>   
<div class="content" style="display: none;" markdown="1">

The basic test implementation revolves around the following functions provided by Jest:
* `describe()`: This describes the test bundle, and contains all the tests in the bundle
* `it()`: This describes and performs a single test.
* `expect()`: This evaluates the test.

And the following functions provided by Enzyme:
* `shallow()`: This renders the component and its immediate children, but it doesn't render any deeper.
* `find()`: This returns a list of the instances of the specified component that were output during rendering.

For example:

*NavigationItems.test.js* (the *test.js* suffix is required, so that it can be identified as containing tests)

```jsx
import React from 'react';
import { configure, shallow } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

import NavigationItems from './NavigationItems';
import NavigationItem from './NavigationItem/NavigationItem';

// connects Enzyme to the test
configure({ adapter: new Adapter() });

describe('<NavigationItems />', () => {
  it('should render two <NavigationItem /> elements if not authenticated', () => {
    // shallow() renders the component and its immediate children, but it doesn't render any deeper.
    const wrapper = shallow(<NavigationItems />);

    // expect() evaluates whether the specified test was successful (true/false)
    // find() returns a list of the instances of the specified component
    expect(wrapper.find(NavigationItem)).toHaveLength(2);
  });
  
  it('should render three <NavigationItem /> elements if authenticated', () => {  
    const wrapper = shallow(<NavigationItems authenticated />);
    expect(wrapper.find(NavigationItem)).toHaveLength(3);
  });
});
```
</div>
</div>

<div id="test-run">
<button type="button" class="collapsible">+ Running Tests</button>   
<div class="content" style="display: none;" markdown="1">

Tests are run using the `npm test` command.  This is run on the command line and, after some initialization, produces an output similar to the following:

```
 PASS  src/components/Navigation/NavigationItems/NavigationItems.test.js
  <NavigationItems />
    ✓ should render two <NavigationItem /> elements if not authenticated (18ms)
    ✓ should render three <NavigationItem /> elements if authenticated (6ms)

Test Suites: 1 passed, 1 total
Tests:       2 passed, 2 total
Snapshots:   0 total
Time:        2.589s
Ran all test suites related to changed files.

Watch Usage: Press w to show more.
```

As can be seen, this lists the descriptions of the tests being run, followed by statistics regarding the results of the tests.

The test runner will now monitor the tests and re-run them if it identifies any changes (in either the tests or codebase).

**NOTE:** If you encounter an error similar to `Error: Invariant failed: You should not use <Route> outside a <Router>`, delete the `src\App.test.js` file.

</div>
</div>

<div id="test-refine">
<button type="button" class="collapsible">+ Refined Test Implementation</button>   
<div class="content" style="display: none;" markdown="1">

A slightly more refined test implementation can be achieved with the following functions:
* `beforeEach()`: This is one of several global functions provided by Jest.  In this case, the function is called before each test.
   * For further information on Jest globals, see here: [https://jestjs.io/docs/en/api](https://jestjs.io/docs/en/api)
* `setProps()`: This is a function exposed by Enzyme that allows props to be passed to a test (in the form of a Javascript object).
   * This is one of many functions exposed by the `shallow()` rendering API; a full list can be found here: [https://enzymejs.github.io/enzyme/docs/api/shallow.html](https://enzymejs.github.io/enzyme/docs/api/shallow.html)

In addition, the `expect()` function provided by Jest exposes many "matchers" that can be used to validate tests.  A full list of these can be found here: [https://jestjs.io/docs/en/expect](https://jestjs.io/docs/en/expect).


For example:

*NavigationItems.test.js*

```jsx
import React from 'react';
import { configure, shallow } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

import NavigationItems from './NavigationItems';
import NavigationItem from './NavigationItem/NavigationItem';

// connects Enzyme to the test
configure({ adapter: new Adapter() });

describe('<NavigationItems />', () => {
  let wrapper;

  beforeEach(() => {
    // factor out the shallow() function since it is common to all tests
    wrapper = shallow(<NavigationItems />);
  });

  it('should render two <NavigationItem /> elements if not authenticated', () => {
    expect(wrapper.find(NavigationItem)).toHaveLength(2);
  });

  it('should render three <NavigationItem /> elements if authenticated', () => {
    // pass props using setProps()
    wrapper.setProps({ 
      isAuthenticated: true 
    });
    expect(wrapper.find(NavigationItem)).toHaveLength(3);
  });
  
  it('test that the logout <NavigationItem /> element is rendered if authenticated', () => {
    wrapper.setProps({ isAuthenticated: true });

    expect(wrapper.contains(<NavigationItem link="/logout">Logout</NavigationItem>)).toEqual(true);
  });
});
```

</div>
</div>

<div id="test-refine">
<button type="button" class="collapsible">+ Testing Containers</button>   
<div class="content" style="display: none;" markdown="1">

Although Redux containers deal with state rather than props, a container can be tested via props by wrapping the default export with `connect()` (so that the state can be converted to props) and also marking the container component as an export.

NOTE: that all props must be initialized *including functions exposed by the props*.

For example:

*BurgerBuilder.js*

```jsx
import React, { Component } from 'react';
import { connect } from 'react-redux';

...etc...

export class BurgerBuilder extends Component {
  state = {
    purchasing: false,
  };

  //
  componentDidMount() {
    this.props.onInitIngredients();
  }

  ...etc...
}

const mapStateToProps = (state) => {
  if (state) {
    return {
      ...etc...
    };
  } else {
    return null;
  }
};

const mapDispatchToProps = (dispatch) => {
  return {
    ...etc...
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(withErrorHandler(BurgerBuilder, axios));
```

The following is an example of test that might be written for the above code:

*BurgerBuilder.test.js*

```jsx
import React from 'react';
import { configure, shallow } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

import { BurgerBuilder } from './BurgerBuilder';
import BuildControls from './BuildControls';

// connects enzyme to the test
configure({ adapter: new Adapter() });

describe('<BurgerBuilder />', () => {
  let wrapper;

  beforeEach(() => {
    // for the onInitIngredients() prop, just pass in a dummy function
    wrapper = shallow(<BurgerBuilder onInitIngredients={() => {} } />);
  });

  it('should render <BuildControls /> when receving ingredients', () => {
    wrapper.setProps({
      ingredients: { salad: 0 },
    });
    expect(wrapper.find(BuildControls)).toHaveLength(1);
  });
});

```
</div>
</div>

<div id="test-redux">
<button type="button" class="collapsible">+ Testing Redux</button>   
<div class="content" style="display: none;" markdown="1">

We don't want to test complex chains of actions, reducers and state.  All we really want to test are the reducers.

Testing reducers is relatively straightforward since we don't need to worry about rendering (and this don't need enzyme).

For example, to test the authentication reducer:

*auth.js*

```jsx
...etc...

const initialState = {
  userId: null,
  token: null,
  error: null,
  loading: false,
  authRedirectPath: '/',
};

const authSuccess = (state, action) => {
  return updateObject(state, {
    userId: action.userId,
    token: action.token,
    error: null,
    loading: false,
  });
};

...etc...

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionTypes.AUTH_SUCCESS: {
      return authSuccess(state, action);
    }
    ...etc...
  }
};

export default reducer;
```

A test for this might be the following:

*auth.test.js*

```jsx
import reducer from './auth';
import * as actionTypes from '../actions/actionTypes';

describe('auth reducer', () => {
  it('should return the initial state', () => {
    expect(reducer(undefined, {})).toEqual({
      userId: null,
      token: null,
      error: null,
      loading: false,
      authRedirectPath: '/',
    });
  });

  it('should store the token upon login', () => {
    expect(
      reducer(
        {
          userId: null,
          token: null,
          error: null,
          loading: false,
          authRedirectPath: '/',
        },
        {
          type: actionTypes.AUTH_SUCCESS,
          token: 'some-token',
          userId: 'some-user-id',
        }
      )
    ).toEqual({
      userId: 'some-user-id',
      token: 'some-token',
      error: null,
      loading: false,
      authRedirectPath: '/',
    });
  });
});
```
</div>
</div>

</div>
</div>

<div id="deploy">
<button type="button" class="collapsible">+ Deploying Single Page Applications</button>   
<div class="content" style="display: none;" markdown="1">

1. Check (&amp; Adjust) basepath
   * `<BrowserRouter basename="/my-app/">`
1. Build &amp; Optimize Project
   * `npm run build`
1. Check that server ALWAYS returns index.html
   * including 404 cases!
1. Upload build artifacts to static server
   * Found in /build folder when using create-react-app

Deployment instructions will vary host-to-host.  A couple of examples:

**Firebase**
1. `npm install -g firebase-tools`
1. `firebase login`
1. `firebase init`
   * Firebase CLI -> Hosting
   * Firebase Project -> [choose project name]
   * Public directory -> build
   * Single-page app -> y
   * Overwrite build/index.html -> n
1. `firebase deploy`
1. Confirm that the app is accessible at `https://[project-name].firebaseapp.com`

**GitHub Pages**
1. Create a repository containing the app
1. Install dependencies: `npm install`
1. Install gh-pages: `npm install gh-pages --save-dev`
1. Add the following to the package.json file (just above `"dependencies"`):
   * `"homepage": "https://[github-username].github.io/[github-repo-name]"`
1. Also add the following to `"scripts"`:
   * `"predeploy": "npm run build"`
   * `"deploy": "gh-pages -d build"`
1. Commit all files
1. Run: `npm run deploy`
1. Confirm that the app is accessible at `https://[github-username].github.io/[github-repo-name]`

NOTE: The GitHub application is deployed to a `gh-pages` branch.  If the app is not automatically visible at the expected URL, check that the `gh-pages` branch has been used for the application source: [repo] -> Settings -> GitHub Pages -> Source.

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="webpack">
<button type="button" class="collapsible">+ Webpack</button>
<div class="content" style="display: none;" markdown="1">

<div id="webpack-intro">
<button type="button" class="collapsible">+ Introduction</button>
<div class="content" style="display: none;" markdown="1">

Webpack is the de-facto standard for setting up projects.  At its core, Webpack is a bundler; it packages a collection of files into a bundle.  In addition to this however, Webpack also analyzes connections between files and optimizes, transforms and transpiles them. 

1. Needs at last one entry point (e.g. app.js), but can handle more than this.
1. From the entry point, webpack builds up a map of all its the dependencies.
1. It packages all of the dependencies into a single, concatenated bundle (e.g. dist/bundle.js)
1. During the packaging, loaders can be applied to the files (e.g. babel-loader, css-loader etc.).  Loaders apply file-dependent transformations.
1. Additionally, after the loaders have acted on each file, plugins can be applied to the concatenated bundle before it is output (e.g. uglify).

The configuration for these steps is defined in a `webpack.config.js` file.

**NOTE**: The create-react-app script uses Webpack under the covers, so theoretically Webpack could be used directly, however this is not recommended as normal practice (since CRA handles a lot of the complexities).

</div>
</div>

<div id="webpack-basics">
<button type="button" class="collapsible">+ Basic Workflow Requirements</button>
<div class="content" style="display: none;" markdown="1">

To partially emulate create-react-app, the basic webpack workflow requirements are:

* Compile Next-Gen JavaScript Features
* Handle JSX
* CSS Autoprefixing
* Support Image Imports
* Optimize code

</div>
</div>

<div id="webpack-example">
<button type="button" class="collapsible">+ Example Implementation</button>
<div class="content" style="display: none;" markdown="1">

The following details how to create a React project without using create-react-app.

1. Create a new folder
1. If using git, add a `.gitignore` (see below)
1. Run `npm init` (to enable support for NodeJS; this will create an initial `package.json` file)
1. Run `npm install --save-dev webpack webpack-dev-server webpack-cli`
1. Create a `src` folder
1. Create `src/index.html`
1. If using VS Code, in the empty `index.html` file type `html:5` and click return.  This will add boiler-plate HTML code to the file.
1. Add the following to the `<body />` of the HTML: `<div id="root"></div>` (see below)
1. Now add the following to the `src` folder:
   * `assets` folder
   * `components` folder
   * `containers` folder
   * `index.js` (see below)
   * `index.css` (see below)
   * `App.js` (see below)
1. Install root dependencies: `npm install react react-dom react-router-dom`
1. Create the app.

*.gitignore*

```
node_modules
.DS_Store
/dist
```

*src/index.html*

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

*src/index.css*

```css
body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}
```

*src/index.js*

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

import './index.css';
import App from './App';

const app = (
  <BrowserRouter>
    <App />
  </BrowserRouter>
);

ReactDOM.render(app, document.getElementById('root'));
```

*src/App.js*

```jsx
import React, { Component } from 'react';
import { Link } from 'react-router-dom';

// if require lazy-loading
import asyncComponent from './hoc/asyncComponent';

const AsyncComp = asyncComponent(() => {
  return import('./LazyLoadedComponent');
});

class App extends Component {
  render() {
    return (
      <div>
        ...etc...
      </div>
    );
  }
}
```

</div>
</div>

<div id="webpack-config">
<button type="button" class="collapsible">+ Configuring Webpack</button>
<div class="content" style="display: none;" markdown="1">

Add `"start": "webpack-dev-server"` to `"scripts"` in `package.json`

Create the following file in the same folder as `package.json`: `webpack.config.js`

The following example demonstrates the bare minimum config to get Webpack to run.  Full documentation for Webpack can be found here:
* [https://webpack.js.org/guides/](https://webpack.js.org/guides/)

*webpack.config.js*

```js
// NodeJS syntax

// NodeJS package
const path = require('path'); 

module.exports = {
  mode: 'development',
  // entry point
  entry: './src/index.js',
  output: {
    // __dirname = absolute path for folder containing webpack.config.js
    // dist = folder under __dirname where output is to be written
    path: path.resolve(__dirname, 'dist'),
    // name of output file
    filename: 'bundle.js',
    publicPath: '',
  },
  // controls how source maps are created (to aid debugging)
  // check official docs for further options
  devtool: 'cheap-module-eval-source-map',
};
```

</div>
</div>

<div id="webpack-babel">
<button type="button" class="collapsible">+ Babel Loader</button>
<div class="content" style="display: none;" markdown="1">

Babel is a third-party library that transpiles JavaScript code.  Specifically, it converts next-gen JavaScript code (including JSX) to older code that can be understood by older browsers.

For further documentation on Babel, see here:
* [https://babeljs.io/docs/en/](https://babeljs.io/docs/en/)

The packages installed depend on the exact configuration being used.  In this case:

Install: `npm install --save-dev @babel/core @babel/preset-env @babel/preset-react @babel/preset-stage-2 babel-loader @babel/plugin-proposal-class-properties`

To enable Babel, it must be added as a module in the Webpack config:

*webpack.config.js*

```js
...etc...

module.exports = {
  ...etc...
  
  module: {
    rules: [
      {
        // for all .js files
        test: /\.js$/,
        // (but exclude anything in node_modules)
        exclude: /node_modules/,
        // process all found files using this loader
        loader: 'babel-loader',
      },
    ],
  },
};
```

To configure Babel, a `.babelrc` is added to the project:

*.babelrc*

```js
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          // browsers with more than 1% of market share,
          // or the last 2 versions
          "browsers": ["> 1%", "last 2 versions"]
        }
      }
    ],
    // presets for React plugins 
    "@babel/preset-react"
  ],
  // plugins to perform additional processing of code
  "plugins": [
    // prevents errors due to code that is only at the
    // proposal stage and not officially supported
    "@babel/plugin-proposal-class-properties"
  ]
}
```

**Babel Polyfill**

The current setup won't support all browsers theoretically supported by React. Features like Promises and Object.assign() are missing in older browsers - especially in IE.

Support for these browsers can by added using a polyfill (a package which provides these features for older browsers).

The Babel docs explain how you can take advantage of Babel's built-in "Polyfill auto injecting" feature: [https://babeljs.io/docs/en/babel-polyfill](https://babeljs.io/docs/en/babel-polyfill)

First, install the following two packages:
* core-js
* regenerator-runtime

Install: `npm install core-js regenerator-runtime`

Then, change the config of your @babel/preset-env babel preset in the .babelrc file: 

"presets": [
    ["@babel/preset-env", {
        "targets": {
            "browsers": [
                "> 1%",
                "last 2 versions"
            ]
        },
        "useBuiltIns": "usage"
     }],
    ...
 ],

*.babelrc*

```js
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          // browsers with more than 1% of market share,
          // or the last 2 versions
          "browsers": ["> 1%", "last 2 versions"]
        },
        "useBuiltIns": "usage"
      }
    ],
    
    ...etc...
  ],
  
  ...etc...
}
```

</div>
</div>

<div id="webpack-css">
<button type="button" class="collapsible">+ CSS Loader</button>
<div class="content" style="display: none;" markdown="1">

The CSS loader actually has four components:
* `css-loader`: analyzes css imports
* `style-loader`: takes all of the found css and injects it into an HTML page
* `postcss-loader`: allows styles to be transformed using plugins
* `autoprefixer`: a plugin to parse CSS and add vendor prefixes to CSS rules

For further information on PostCSS and Autoprefixer, see here: 
* [https://postcss.org/](https://postcss.org/)

Install: `npm install --save-dev style-loader css-loader postcss-loader autoprefixer`

*webpack.config.js*

```js
const autoprefixer = require('autoprefixer'); // NodeJS package

...etc...

module.exports = {
  ...etc...
  
  module: {
    rules: [
      ...etc...
      {
        // for all .css files
        test: /\.css$/,
        // (but exclude anything in node_modules)
        exclude: /node_modules/,
        // process all found files using these loaders
        use: [ // mutiple loaders
          { loader: 'style-loader' },
          { 
            loader: 'css-loader', options: {
              importLoaders: 1,
              modules: {
                localIdentName: '[name]__[local]__[hash:base64:5]'
              }
            }
          },
          {
            loader: 'postcss-loader',
            options: {
              ident: 'postcss',
              plugins: () => [autoprefixer],
            },
          },
        ]
      },
    ],
  },
};
```

In addition, Autoprefixer requires that the list of browsers to be targeted be added to the package.json file:

*package.json*

```js
...etc...

  "license": "ISC",
  "browserslist": "> 1%, last 2 versions", // same as in .babelrc
  "devDependencies": {

...etc...
```

</div>
</div>

<div id="webpack-asset">
<button type="button" class="collapsible">+ Asset Loader</button>
<div class="content" style="display: none;" markdown="1">

Processing assets that need to be referenced by URL (such as images) is done using `url-loader`.  If files are below a set file size limit, `url-loader` inlines them within the JavaScript files using base64 encoding (rather than uploading them as separate files).  This is typically used for image files.  It provides performance advantages if an app contains many small files, since it avoids repeated server requests when the app is loaded.

If the files exceed the file size limit, `url-loader` defers to `file-loader`, which uploads each file separately rather than inlining them.  For large files, the performance benefits of inlining them can be lost since the JavaScript can get very large.

Install: `npm install --save-dev url-loader file-loader`

*webpack.config.js*

```js
...etc...

module.exports = {
  ...etc...
  
  module: {
    rules: [
      ...etc...
      {
        // for all image files
        test: /\.(png|jpe?g|gif)$/,
        // (but exclude anything in node_modules)
        exclude: /node_modules/,
        // process all found files using this loader
        // for demo purposes, options are specified using
        // an alternative, inline syntax.
        // limit = max image size in kb
        // name = output path
        loader: 'url-loader?limit=8192&name=images/[name].[ext]',
      },
    ],
  },
};
```

</div>
</div>

<div id="webpack-inject">
<button type="button" class="collapsible">+ Injecting The JavaScript Into The HTML</button>
<div class="content" style="display: none;" markdown="1">

Once all of the preceding file transformations have been completed, the results are passed to a final transformation that injects them into the app HTML.

Install: `npm install --save-dev html-webpack-plugin`

The `html-webpack-plugin` is instantiated in the `plugins` array, which is separate to the `module` array.

*webpack.config.js*

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');

...etc...

module.exports = {
  ...etc...
  
  module: {
    ...etc...
  },
  plugins: [
    new HtmlWebpackPlugin({
      // file to be used as basis for app
      template: __dirname + '/src/index.html',
      // file to be generated by the plugin
      filename: 'index.html',
      // where to inject the results
      inject: 'body',
    }),
  ],
};
```

</div>
</div>

<div id="webpack-inject">
<button type="button" class="collapsible">+ Building &amp; Optimizing The App</button>
<div class="content" style="display: none;" markdown="1">

To build and start the development version of the app, simply run `npm start`.

To build and run the production version of the app:

1. Copy `webpack.config.js` to `webpack.config.prod.js`.
1. In `webpack.config.prod.js` change the `mode` to be `'production'`.
1. Also, change `devtool` to be `'none'`.
1. In `package.json` add the following to the `scripts`:
   * `"build:prod": "webpack --config webpack.config.prod.js"`
1. Run the build using the following command:
   * `npm run build:prod`

The optimized app is deployed to the `\dist` sub-folder.

</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="nextjs">
<button type="button" class="collapsible">+ Next.js - Server-Side Rendering</button>
<div class="content" style="display: none;" markdown="1">

<div id="nextjs-intro">
<button type="button" class="collapsible">+ Introduction</button>
<div class="content" style="display: none;" markdown="1">

Next.js is a library that builds on top of React.  It forces a particular folder structure and enables server-side rendering "out-of-the-box".  It also simplifies some of the configuration.

Server-side rendering is particularly useful if an app is highly dependent on being found by search engines.

Further information about Next.js can be found here: [https://nextjs.org/](https://nextjs.org/).

**Server-Side Rendering*

During server-side rendering, when the first page load occurs (which would normally respond with just the app bundle), the server also generates a rendered version of the first page and passes this back with the app bundle.  This means the first page will always be rendered as expected.  Subsequent page accesses will be rendered by the client as normal.

This is particularly useful when the app is being crawled by a search engine (or an machine-based form of access), since these do not normally perform page rendering.

Folders & Files to reflect URLs in file system.  Automatically parse this using internal Router.  Also, pre-renders the pages on the server and code-splits the code.

</div>
</div>

<div id="nextjs-setup">
<button type="button" class="collapsible">+ Setting up a Project</button>
<div class="content" style="display: none;" markdown="1">

**Setting Up The Project**

The following details how to create a Next.js-based project without using create-react-app.

1. Create a new folder
1. If using git, add a `.gitignore` (see below)
1. Run `npm init` (to enable support for NodeJS; this will create an initial `package.json` file)
1. Install root dependencies: `npm install react react-dom next`
1. In `package.json`, add the scripts required by Next.js (see below)
1. Create a `.\pages` folder in the root folder
   * Note that the URL scheme maps to the folder scheme under the `pages` folder.  So, `.\pages\auth\user.js` will map to `https://localhost:3000/auth/user.js`.
1. All pages are placed under this folder (or its sub-folders).
   * React components are typically placed outside of this folder (but imported into the pages as normal).
1. Start the development server using the following command, provided by Next:
   * `npm run dev`

*.gitignore*

```
node_modules
.DS_Store
/dist
```

*package.json*

```js
{
  ...etc...
  
  "scripts": {
    "dev": "next",
    "build": "next build",
    "start": "NODE_ENV=production next start",
    "prod": "npm run build; npm run start"
  },
  
    ...etc...
}
```

</div>
</div>

<div id="nextjs-pages">
<button type="button" class="collapsible">+ Creating Pages</button>
<div class="content" style="display: none;" markdown="1">

Pages are typically created using stateless functional components, although class components and functional components that use `useState()` will also work.

To handle linking between pages, Next.js provides components that can be used in place of those provided by React.  For example:
   * `<Link href="url"><a>Text</a></Link>` (imported using: `import Link from 'next/link';`)
   * `<button onClick={() => Router.push('url')} }>Text</button>` (imported using: `import Router from 'next/router';`)
   
For example:

*pages/index.js*

```jsx
import React from 'react';
import Link from 'next/link';
import Router from 'next/router';

const indexPage = () => (
  <div>
    <h1>The Main Page</h1>
    <p>
      Go to{' '}
      <Link href="/auth">
        <a>Auth</a>
      </Link>
    </p>
    <button
      onClick={() => {
        Router.push('/auth');
      } }
    >
      Got to Auth
    </button>
  </div>
);

export default indexPage;
```

*pages/auth/index.js*

```jsx
import React from 'react';

const authIndexPage = () => (
  <div>
    <h1>The Auth Index Page</h1>
  </div>
);

export default authIndexPage;
```

</div>
</div>

<div id="nextjs-components">
<button type="button" class="collapsible">+ Creating Components</button>
<div class="content" style="display: none;" markdown="1">

Components are created outside of the `./pages` folder (for example under `./components`).

For example:

*components/User.js*

```jsx
import React from 'react';

const user = (props) => (
  <div>
    <h1>{props.name}</h1>
    <p>Age: {props.age}</p>
  </div>
);

export default user;
```

These can then be imported as normal into the pages:

*pages/auth/index.js*

```jsx
import React from 'react';

import User from '../../components/User';

const authIndexPage = () => (
  <div>
    <h1>The Auth Index Page</h1>
    <User name="Max" age={28} />
  </div>
);

export default authIndexPage;
```

</div>
</div>

<div id="nextjs-styling">
<button type="button" class="collapsible">+ Styling Pages</button>
<div class="content" style="display: none;" markdown="1">

* The latest version of Next.js has support for CSS modules, however previous versions did not.  
* Next.js has always supported other forms of styling, such as Inline Styles and Radium.  
* It also supports `styled-jsx`, which provides isolated scope CSS using a `<style />` tag.
   * [https://github.com/vercel/styled-jsx](https://github.com/vercel/styled-jsx)

*User.js*

```js
import React from 'react';

import classes from './User.module.css';

const user = (props) => (
  <div className={classes.User}>
    <h1>{props.name}</h1>
    <p>Age: {props.age}</p>
  </div>
);

export default user;
```

*User.module.css*

```css
.User {
  border: 1px solid #eee;
  box-shadow: 0 2px 3px #ccc;
  padding: 20px;
  text-align: center;
}
```

</div>
</div>

<div id="nextjs-errors">
<button type="button" class="collapsible">+ Error Handling</button>
<div class="content" style="display: none;" markdown="1">

404 errors, which can happen frequently and thus put a strain on the server, are typically handled by placing a `404.js` file in the root of the `./pages` folder.  A 404 error page is then statically generated at build time.

*pages/404.js*

```jsx
export default function Custom404() {
  return <h1>404 - Page Not Found</h1>;
}
```

For handling 500 (or other) error codes, a default page is provided by Next.  This page is generated dynamically so that details of the error can be passed to it (hence why it is separate from the 404 error page).

*pages/getStarCount.js*

```jsx
import Error from 'next/error';

function tryParse(suspect) {
  ...etc... 
  return return { value: parsedSuspect, valid: isValid };
}
JSON['tryParse'] = tryParse;

export async function getServerSideProps() {
  const res = await fetch('https://api.github.com/repos/vercel/next.js');

  const statusCode = res.statusCode;
  let errorCode = res.ok ? false : statusCode ? statusCode : 500;

  // initially get response as text, in case json wasn't returned
  const resText = await res.text();
  // then try to convert JSON to object
  const result = JSON.tryParse(resText);
  const resObj = result.value;

  // if conversion was successful, use resObj
  let count = 0;
  if (result.valid) {
    count = resObj.stargazers_count;
    if (!count) count = 0;
  }

  return {
    props: { errorCode, stars: count, errorDetails: resObj },
  };
}

export default function Page({ errorCode, stars, resObj }) {
  if (errorCode) {
    return (
      <Error statusCode={errorCode} title={JSON.stringify(resObj)} />
    );
  }

  return <div>Next stars: {stars}</div>;
}
```

Alternatively, the default error page can be overridden by placing an `_error.js` file in the root of the `./pages` folder.  This must be imported instead of `next/error`.  

*pages/_error.js*

```jsx
const Error = (props) => {
  return (
    <p>
      {props.statusCode
        ? `An error ${props.statusCode} occurred on server: ${props.metadata}`
        : 'An error occurred on client'}
    </p>
  );
};

Error.getInitialProps = ({ res, err }) => {
  const statusCode = res ? res.statusCode : err ? err.statusCode : 404
  return { statusCode, metadata: err }
}

export default Error
```

*pages/getStarCount.js*

```jsx
// import _error, rather than next/error;
import ErrorPage from './_error';

...etc...

export default function Page({ errorCode, stars, errorDetails }) {
  if (errorCode) {
    return (
      <ErrorPage
        statusCode={errorCode}
        title={'Something went wrong'}
        metadata={JSON.stringify(errorDetails)}
      />
    );
  }

  return <div>Next stars: {stars}</div>;
}
```

</div>
</div>

<div id="nextjs-hooks">
<button type="button" class="collapsible">+ Lifecycle Hooks</button>
<div class="content" style="display: none;" markdown="1">

One of the challenges for SEO is that search engine crawlers will typically not register content that is not rendered immediately when the page loads.  This is one of the main reasons why the following lifecycle hooks have been added by Next.js.

The following is an example of a page that doesn't use hooks (it simply fetches the data as necessary whenever the page is loaded).  Implementing this page, while sure to always display the latest data, gives slow performance and a potentially heavy impact on the backend API.  Compare with this with the other options discussed in the next sections.

**Example without Next.js Hooks (uses useEffect())**

```jsx
// users/page.jsx
// data fetched from an external data source with axios
import { useEffect, useState } from 'react';
import axios from 'axios';

const Users = () => {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(false);
  const fetchData = async () => {
    await axios.get('https://jsonplaceholder.typicode.com/users')
      .then(res => {
        setError(false);
        setUsers(prevState => [...prevState, ...res.data]);
      })
      .catch(() => {
        setError(true);
      })
      .finally(() => {
        setLoading(false);
      });
  };

  useEffect(() => {
    fetchData();
  }, []);

  return (
    <section>
      <header>
        <h1>List of users</h1>
      </header>
      {!error && loading && <div>Loading data...</div>}
      {error && <div>There was an error.</div>}
      {!error && users && (
        <table>
          <thead>
            <tr>
              <th>Username</th>
              <th>Email</th>
              <th>Name</th>
            </tr>
          </thead>
          <tbody>
            {users.map((user, key) => (
              <tr key={key}>
                <td>{user.username}</td>
                <td>{user.email}</td>
                <td>{user.name}</td>
              </tr>
            ))}
          </tbody>
        </table>
      )}
    </section>
  );
};

export default Users;
```

Behaviour:
* Emitted File Size: 1.11 kB
* Page Type: Static
   * Client always fetches data from backend API and renders it.
* XMLHttpRequest: Yes (fetch(App) + XHR(JSON), then XHR(JSON))
* Slow fetch; slow render.

</div>
</div>

<div id="nextjs-gip">
<button type="button" class="collapsible">+ Lifecycle Hooks: getInitialProps()</button>
<div class="content" style="display: none;" markdown="1">

`getInitialProps()` runs on both the server and the client.  Its goal is to present a static page on first hit, but then act in a traditional, dynamic manner for subsequent accesses.  

The first time the page is requested (e.g. if the user manually enters the URL or refreshes the page), the initial props (hence the name) are obtained by the server querying the backend API and then returning a rendered HTML page to the client.  Subsequent renders of the page are done on the client-side, with props being fetched from the backend API by the client.  Typically, this method will access the data store API via an intermediate API layer (to avoid publically exposing the low-level backend API). 

**NOTE 1**: This method has been deprecated in favour of the other hooks, however it is still commonly used.  It is recommended that future development should use the other hooks.

**NOTE 2**: If this method is present in a page, the page will always be treated as server-side (i.e. it will not be pre-rendered as HTML).

Example:

```jsx
// users/page.jsx
// data fetched from an external data source with axios
// using `getInitialProps`
import axios from 'axios';

const fetchData = async () =>
  await axios
    .get('http://jsonplaceholder.typicode.com/users')
    .then((res) => ({
      error: null,
      users: res.data,
    }))
    .catch((error) => ({
      error: JSON.stringify(error),
      users: null,
    }));

const UsersPage = ({ users, error }) => {
  return (
    <section>
      <header>
        <h1>List of users</h1>
      </header>
      {error && <div>There was an error: {error}</div>}
      {!error && users && (
        <table>
          <thead>
            <tr>
              <th>Username</th>
              <th>Email</th>
              <th>Name</th>
            </tr>
          </thead>
          <tbody>
            {users.map((user, key) => (
              <tr key={key}>
                <td>{user.username}</td>
                <td>{user.email}</td>
                <td>{user.name}</td>
              </tr>
            ))}
          </tbody>
        </table>
      )}
    </section>
  );
};

UsersPage.getInitialProps = async () => {
  const data = await fetchData();

  return { users: data.users, error: data.error };
};

export default UsersPage;
```

Behaviour:
* Emitted File Size: 670 bytes
* Page Type: Lambda (dynamic)
   * Initially, server fetches data and renders page.
   * Then, client fetches data and renders page.
* XMLHttpRequest: Yes (Initially fetch(App), then XHR(JSON))
* Initial fast fetch & fast render; subsequent slow fetch and slow render.

</div>
</div>

<div id="nextjs-gssp">
<button type="button" class="collapsible">+ Lifecycle Hooks: getServerSideProps()</button>
<div class="content" style="display: none;" markdown="1">

`getServerSideProps()` is a lifecycle hook that runs *only* on the server.  

The first time the page is hit, a fully rendered HTML page is returned (effectively presenting a static page to the world).  Subsequent accesses will return only the props, in JSON format, which the client then uses to update the previously received HTML.  Every time the page is rendered, the server-side function will run.  This is subtely different from `getInitialProps()`, which only calls the server-side function on first hit.  

Because the function runs on the server, it can access the backend directly (and locally), without an intervening API layer, which can have performance advantages when accessing data infrequently.  It also improves security by reducing the information passed back-and-forth, and improves compatibility (since the data fetching process is less dependent on the browser).  

**NOTE 1**: The downside of this method is that it can impact performance if data must be fetched frequently.  In this case, the recommended solution is to use `getServerSideProps()` for first access, and then `useSWR()` for further accesses.

**NOTE 2**: If this method is present in a page, the page will always be treated as server-side (i.e. it will not be pre-rendered as HTML).

Example:

```jsx
// users/page.jsx
// data fetched from an external data source with axios
// using `getServerSideProps`
import axios from 'axios';

const fetchData = async () => await axios.get('https://jsonplaceholder.typicode.com/users')
  .then(res => ({
    error: false,
    users: res.data,
  }))
  .catch(() => ({
      error: true,
      users: null,
    }),
  );

const Users = ({ users, error }) => {
  return (
    <section>
      <header>
        <h1>List of users</h1>
      </header>
      {error && <div>There was an error.</div>}
      {!error && users && (
        <table>
          <thead>
            <tr>
              <th>Username</th>
              <th>Email</th>
              <th>Name</th>
            </tr>
          </thead>
          <tbody>
            {users.map((user, key) => (
              <tr key={key}>
                <td>{user.username}</td>
                <td>{user.email}</td>
                <td>{user.name}</td>
              </tr>
            ))}
          </tbody>
        </table>
      )}
    </section>
  );
};

export const getServerSideProps = async () => {
  const data = await fetchData();

  return {
    props: data,
  };
}

export default Users;
```

Behaviour:
* Emitted File Size: 440 bytes
* Page Type: Lambda (dynamic)
   * Initially, server fetches data and renders page.
   * Then, server fetches data and client renders page.
* XMLHttpRequest: No (Initially fetch(App), then fetch(JSON))
* Initial fast fetch and fast render; subsequent slower fetch and slower render.

</div>
</div>

<div id="nextjs-gsp">
<button type="button" class="collapsible">+ Lifecycle Hooks: getStaticProps()</button>
<div class="content" style="display: none;" markdown="1">

`getStaticProps()` *always* serves a pre-rendered version of the page from the server.  The rendering happens *at build time*, which means the page can be effectively considered a traditional, static HTML page at runtime.  

This approach is particularly useful for SEO and/or ultra-fast access to a page is required.  Also, it avoids expensive, real-time data transformations, or exposure of private APIs.  

The chief downside to this approach is that the page only presents data captured at build-time; it cannot present data that changes regularly.

**NOTE**: This hook only works properly in a production build.  In a development build, there will be an additional XHR call at runtime to fetch the data.

Example:

```jsx
// users/page.jsx
// data fetched from an external data source with axios
// using `getStaticProps`
import axios from 'axios';

const fetchData = async () => await axios.get('https://jsonplaceholder.typicode.com/users')
  .then(res => ({
    error: false,
    users: res.data,
  }))
  .catch(() => ({
      error: true,
      users: null,
    }),
  );

const Users = ({ users, error }) => {
  return (
    <section>
      <header>
        <h1>List of users</h1>
      </header>
      {error && <div>There was an error.</div>}
      {!error && users && (
        <table>
          <thead>
            <tr>
              <th>Username</th>
              <th>Email</th>
              <th>Name</th>
            </tr>
          </thead>
          <tbody>
            {users.map((user, key) => (
              <tr key={key}>
                <td>{user.username}</td>
                <td>{user.email}</td>
                <td>{user.name}</td>
              </tr>
            ))}
          </tbody>
        </table>
      )}
    </section>
  );
};

export const getStaticProps = async () => {
  const data = await fetchData();

  return {
    props: data,
  };
}

export default Users;
```

Behaviour:
* Emitted File Size: 442 bytes
* Page Type: Static
   * Returns static HTML.
* XMLHttpRequest: No (Initially fetch(App), then from cache)
* Fast fetch; ultra-fast render.

</div>
</div>

<div id="nextjs-swr">
<button type="button" class="collapsible">+ Lifecycle Hooks: useSWR()</button>
<div class="content" style="display: none;" markdown="1">

`useSWR()` can be thought of as the replacement for the client-side aspects of `getInitialProps()`.  It handles caching, revalidation, focus tracking, refetching on interval, and more.  The name `SWR` derives from `stale-while-revalidate`, an HTTP cache invalidation strategy that first returns the data from cache (stale), then sends a fetch request (revalidate) and finally, if the data has changed, returns the up-to-date data.

This approach means that pages render fast initially (albeit with potentially out-of-date data), but can subsequently be updated when the latest data is available.

By default, revalidation (ie. re-fetch to check data state) is performed under the following conditions:
* When the component is mounted
* When the window is focused (with a minimum interval of 5 seconds)
* When the browser regains a network connection

If it also possible to configure `useSWR` to constantly poll the data source at a set interval using the `refreshInterval` configuration option.

For further details regarding the various configuration options available, see the `useSWR` documentation:
* [https://github.com/vercel/swr](https://github.com/vercel/swr)

```jsx
// users/page.jsx
// data fetched from an external data source with axios
// using `useSWR`
import useSWR from 'swr';

import axios from 'axios';

const fetchData = async (url) =>
  // errors are handled by useSWR
  await axios.get(url).then((res) => ({
    users: res.data,
  }));

const UsersPage = () => {
  const { data, error } = useSWR(
    'http://jsonplaceholder.typicode.com/users',
    fetchData,
    // optionally set a refreshInterval
    // {
    //   refreshInterval: 5000,
    // }
  );

  let users = null;
  if (data) users = data.users;

  return (
    <section>
      <header>
        <h1>List of users</h1>
      </header>
      {!error && !users && <div>Loading data...</div>}
      {error && <div>There was an error: {error}</div>}
      {!error && users && (
        <table>
          <thead>
            <tr>
              <th>Username</th>
              <th>Email</th>
              <th>Name</th>
            </tr>
          </thead>
          <tbody>
            {users.map((user, key) => (
              <tr key={key}>
                <td>{user.username}</td>
                <td>{user.email}</td>
                <td>{user.name}</td>
              </tr>
            ))}
          </tbody>
        </table>
      )}
    </section>
  );
};

export default UsersPage;
```

Behaviour:
* Emitted File Size: 4.46 kB
* Page Type: Static
   * Fetches data from backend API, which is rendered on client.
* XMLHttpRequest: Yes (Initially fetch(App) + XHR(JSON), then from cache + XHR(JSON))
* Initial slow fetch & slow render; later ultra-fast render, followed by slow fetch, then fast render if data changed.

</div>
</div>

<div id="nextjs-deploy">
<button type="button" class="collapsible">+ Deploying a Next.js App</button>
<div class="content" style="display: none;" markdown="1">

**NOTE**: Next.js is dependent in Node.js, so Node.js must be installed on the host to which the app is deployed.

To build the app:

1. Add the following to the package.json scripts:
   * "build": "next build",
   * "start": "NODE_ENV=production next start",
1. Then run the build using: `npm run build`
   * This builds the app into a `.next` folder, in the project root.
1. In theory, the `.next` folder contains everything that needs to be deployed, however in practice the entire project folder should be deployed, since items such as the `node_modules` folder also need to be deployed.
1. Once copied to the host, initialize the app using: `npm install`
1. Then start the app using: `npm run start`

</div>
</div>

<div id="nextjs-info">
<button type="button" class="collapsible">+ Further Information</button>
<div class="content" style="display: none;" markdown="1">

* [https://nextjs.org/docs/getting-started](Next.js Documentation)
* [https://www.youtube.com/playlist?list=PLYSZyzpwBEWSQsrukurP09ksi49H9Yj40](Next.js Video Tutorials)
* [https://medium.com/swlh/fetching-and-hydrating-a-next-js-app-using-getserversideprops-and-getstaticprops-65bfe42afed8](Fetching and hydrating a Next.JS app)
* [https://github.com/vercel/swr](SWR Documentation)

</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="animation">
<button type="button" class="collapsible">+ Animation</button>   
<div class="content" style="display: none;" markdown="1">

<div id="animation-showhide">
<button type="button" class="collapsible">+ Simple Show/Hide</button>   
<div class="content" style="display: none;" markdown="1">

A simple way to hide/show a component is to use the `display` CSS property:

*Modal.css*

```jsx
.Modal {
  position: fixed;
  z-index: 200;
  border: 1px solid #eee;
  box-shadow: 0 2px 2px #ccc;
  background-color: white;
  padding: 10px;
  text-align: center;
  box-sizing: border-box;
  top: 30%;
  left: 25%;
  width: 50%;
}

.ModalOpen {
  display: block;
}

.ModalClosed {
  display: none;
}
```

*Modal.js*

```jsx
import React from 'react';

import './Modal.css';

const modal = (props) => {
  const cssClasses = ['Modal', props.show ? 'ModalOpen' : 'ModalClosed'];

  return (
    <div className={cssClasses.join(' ')}>
      <h1>A Modal</h1>
      <button className="Button" onClick={props.closed}>
        Dismiss
      </button>
    </div>
  );
};

export default modal;
```

*App.js*

```jsx
import React, { Component } from 'react';

import './App.css';
import Modal from './components/Modal/Modal';

class App extends Component {
  state = {
    modalIsOpen: false,
  };

  showModal = () => {
    this.setState({ modalIsOpen: true });
  };

  closeModal = () => {
    this.setState({ modalIsOpen: false });
  };

  render() {
    return (
      <div className="App">
        <Modal show={this.state.modalIsOpen} closed={this.closeModal} />
        <button className="Button" onClick={this.showModal}>
          Open Modal
        </button>
      </div>
    );
  }
}

export default App;
```

</div>
</div>

<div id="animation-csstrans">
<button type="button" class="collapsible">+ CSS Transitions</button>   
<div class="content" style="display: none;" markdown="1">

An alternative approach is to use the CSS transition properties.  

For further information regarding these, see here:
* [https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)

*Modal.css*

```jsx
.Modal {

  ...etc...

  transition: all 0.3s ease-out;
}

.ModalOpen {
  opacity: 1;
  transform: translateY(0);
}

.ModalClosed {
  opacity: 0;
  transform: translateY(-100%);
}
```

</div>
</div>

<div id="animation-cssanim">
<button type="button" class="collapsible">+ CSS Animations</button>   
<div class="content" style="display: none;" markdown="1">

A more sophisticated approach is to use CSS animation keyframes, which allow much finer control of the behaviour.

For further information regarding these, see here:
* [https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)

*Modal.css*

```jsx
.Modal {

  ...etc...

  transition: all 0.3s ease-out;
}

.ModalOpen {
  animation: openModal 0.4s ease-out forwards;
}

.ModalClosed {
  animation: closeModal 0.4s ease-out forwards;
}

@keyframes openModal {
  0% {
    opacity: 0;
    transform: translateY(-100%);
  }
  50% {
    opacity: 1;
    transform: translateY(20%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes closeModal {
  0% {
    opacity: 1;
    transform: translateY(0);
  }
  50% {
    opacity: 0.8;
    transform: translateY(60%);
  }
  100% {
    opacity: 0;
    transform: translateY(-100%);
  }
}

```

</div>
</div>

<div id="animation-limits">
<button type="button" class="collapsible">+ Limitations of CSS Transitions &amp; Animations</button>   
<div class="content" style="display: none;" markdown="1">

Although CSS transitions and animations are fine for most simple cases, they have one potentially significant drawback: they always present in the page HTML regardless of whether they are shown or not.  This could impact the performance of the page.

It would be better to take a more React approach and only embed the animated elements when they actually need to be displayed.

A naive implementation might be to use the `modalIsOpen` state to embed the component:

*App.js*

```jsx
import React, { Component } from 'react';

import './App.css';
import Modal from './components/Modal/Modal';

class App extends Component {
  state = {
    modalIsOpen: false,
  };

  showModal = () => {
    this.setState({ modalIsOpen: true });
  };

  closeModal = () => {
    this.setState({ modalIsOpen: false });
  };

  render() {
    return (
      <div className="App">
        {this.state.modalIsOpen ? (
          <Modal show={this.state.modalIsOpen} closed={this.closeModal} />
        ) : null}
        <button className="Button" onClick={this.showModal}>
          Open Modal
        </button>
      </div>
    );
  }
}

export default App;
```

The main limitation with this approach is that the component will be removed instantly; it won't have time to display the animations.

A better approach would be to use tools provided by React to help with this.

</div>
</div>

<div id="animation-rtg">
<button type="button" class="collapsible">+ react-transition-group</button>   
<div class="content" style="display: none;" markdown="1">

The `react-transition-group` package is a community-produced package that exposes components to help entering and exiting transitions.

For further information about the package, see here:
* [https://reactcommunity.org/react-transition-group/](https://reactcommunity.org/react-transition-group/)

* Install: `npm install react-transition-group`
* Import: `import Transition from 'react-transition-group/Transition'`

For example, consider the following code where a button toggle the display of a `<div>`:

*App.js*

```jsx
...etc...

class App extends Component {
  state = {
    showBlock: false,
  };

  render() {
    return (
      <div className="App">
        <button
          className="Button"
          onClick={() =>
            this.setState((prevState) => ({ showBlock: !prevState.showBlock }))
          }
        >
          Toggle
        </button>
        <br />
        {this.state.showBlock ? (
          <div
            style={ {
              backgroundColor: 'red',
              width: 100,
              height: 100,
              margin: 'auto',
            } }
          ></div>
        ) : null}
      </div>
    );
  }
}

export default App;
```

After installing `react-transition-group`, this can be refactored to be:

*App.js*

```jsx
...etc...

import Transition from 'react-transition-group/Transition';

class App extends Component {

  ...etc...

  render() {
    return (
      <div className="App">
        
        ...etc...
        
        <Transition
          in={this.state.showBlock}
          timeout={1000}
          mountOnEnter
          unmountOnExit
        >
          {(state) => (
            <div
              style={ {
                ...etc...
                
                transition: 'opacity 1s ease-out',
                opacity: state === 'exiting' ? 0 : 1,
              } }
            ></div>
          )}
        </Transition>
      </div>
    );
  }
}

export default App;
```

Note that the `Transition` component has several properties.  In this case they are:
* in = the trigger for the transition 
* timeout = time between transitions in ms
* mountOnEnter = "if in === true, add component to DOM"
* unmountOnExit = "if in === false, remove component from DOM"

It also emits the `state` object (not to be confused with the `state` of the App), which can have one of four values:
* 'entering' (component is being displayed)
* 'entered' (component has been displayed)
* 'exiting' (component is being hidden)
* 'exited' (component has been hidden)

The `state` values are used to control which style properties are applied to the component.

If pattern is now applied to the `Modal` component, something like the following results:

*Modal.js*

```jsx
import React from 'react';

import './Modal.css';

const modal = (props) => {
  const cssClasses = [
    'Modal',
    props.show === 'entering'
      ? 'ModalOpen'
      : props.show === 'exiting'
      ? 'ModalClosed'
      : null,
  ];
  
  return (
    <div className={cssClasses.join(' ')}>
      <h1>A Modal</h1>
      <button className="Button" onClick={props.closed}>
        Dismiss
      </button>
    </div>
  );
};

export default modal;
```

*App.js*

```jsx
...etc...

import Transition from 'react-transition-group/Transition';

class App extends Component {

  ...etc...
  
  render() {
    return (
      <div className="App">
        <Transition
          in={this.state.modalIsOpen}
          timeout={300}
          mountOnEnter
          unmountOnExit
        >
          {(state) => <Modal show={state} closed={this.closeModal} />}
        </Transition>
        <button className="Button" onClick={this.showModal}>
          Open Modal
        </button>
      </div>
    );
  }
}

export default App;
```

</div>
</div>

<div id="animation-rtgwrap">
<button type="button" class="collapsible">+ Wrapping The Transition Component</button>   
<div class="content" style="display: none;" markdown="1">

Of course, it is also possible to wrap the Transition in the Modal component, in the following manner:

*Modal.js*

```jsx
import React from 'react';

import './Modal.css';

const modal = (props) => {

  return (
    <Transition in={props.show} timeout={1000} mountOnEnter unmountOnExit>
      {(state) => {
        const cssClasses = [
          'Modal',
          state === 'entering'
            ? 'ModalOpen'
            : state === 'exiting'
            ? 'ModalClosed'
            : null,
        ];

        return (
          <div className={cssClasses.join(' ')}>
            <h1>A Modal</h1>
            <button className="Button" onClick={props.closed}>
              Dismiss
            </button>
          </div>
        );
      } }
    </Transition>
  );
};

export default modal;
```

*App.js*

```jsx
...etc...

class App extends Component {

  ...etc...
  
  render() {
    return (
      <div className="App">
        <Modal show={this.state.modalIsOpen} closed={this.closeModal} />
        <button className="Button" onClick={this.showModal}>
          Open Modal
        </button>
      </div>
    );
  }
}

export default App;
```

</div>
</div>

<div id="animation-timing">
<button type="button" class="collapsible">+ Animation Timing</button>   
<div class="content" style="display: none;" markdown="1">

Care should be taken when setting the timings for animations.  Timings can be set in several places, for example:
* The `timeout` property of the `Transition` component.
   * Determines how long each state ('entering' &amp; 'exiting') will be held before transitioning.
   * If this is much shorter than 
* The `duration` property of the `animation` CSS property.
   * Determines how long the animation will last.
* The `duration` property of the `transition` CSS property.

If the transition time is much shorter than the animation time, the animation will be cut-off too soon.

It is also possible to set different timings for the enter and exit transitions.  This is done in the following manner:

*Modal.js* 

```jsx
...etc...

const animationTiming = {
  enter: 400,
  exit: 1000,
};

const modal = (props) => {
  ...etc...

  return (
    <Transition
      ...etc...
      timeout={animationTiming}
    >
      ...etc...
    </Transition>
  );
};

export default modal;
```

</div>
</div>

<div id="animation-events">
<button type="button" class="collapsible">+ Transition Events</button>   
<div class="content" style="display: none;" markdown="1">

The `Transition` components provides events for specific parts of the transitions:
* onEnter = Before entering 'entering' mode
* onEntering = Upon entering 'entering' mode
* onEntered = Upon entering 'entered' mode
* onExit = Before entering 'exiting' mode
* onExiting = Upon entering 'exiting' mode
* onExited = Upon entering 'exited' mode

```jsx
  <Transition
    ...etc...
    
    onEnter={() => console.log('onEnter')}
    onEntering={() => console.log('onEntering')}
    onEntered={() => console.log('onEntered')}
    
    onExit={() => console.log('onExit')}
    onExiting={() => console.log('onExiting')}
    onExited={() => console.log('onExited')}
  >
    ...etc...
  </Transition>
```
</div>
</div>

<div id="animation-csstrans">
<button type="button" class="collapsible">+ CSSTransition Component</button>   
<div class="content" style="display: none;" markdown="1">

Although the animation styling can be embedded in the JavaScript, as in the previous examples, it is often more convenient to be able to create some pre-defined CSS classes for the different animation states and ensure that these get attached depending on the state of the animation.  This is the functionality provided by the `CSSTransition` component.

Essentially, `CSSTransition` replaces the need to embed the conditions for controlling the transition in the JavaScript file.  Instead, these can be specified in a CSS file, which can be local or global, where they can be shared by other components.

Rather then specifying the transition conditions, a prefix is specified (can be anything).  This identified CSS classes that relate to these transitions.

In the CSS file, the prefix is combined with well-known suffixes to indicate the applicable styles.  The well-known suffixes are:
* [prefix]-enter : appears for one frame at the start of the enter animation (use to initialize the animation, e.g. set initial opacity)
* [prefix]-enter-active : controls the enter animation
* [prefix]-exit : appears for one frame at the start of the exit animation (use to initialize the animation, e.g. set initial opacity)
* [prefix]-exit-active : controls the exit animation

The following only apply to components that are hardcoded in the DOM (such as the `<button>` in App.js) and are only called the first time the component is mounted.
* [prefix]-appear : appears for one frame at the start of the appear animation (use to initialize the animation, e.g. set initial opacity)
* [prefix]-appear-active : controls the appear animation

*Modal.js*

Note the `classNames` prop added to the `CSSTransition` component.

```jsx
...etc...

import CSSTransition from 'react-transition-group/CSSTransition';

...etc...

const modal = (props) => {
  return (
    <CSSTransition
      ...etc...
      
      {/* Note: classNames (plural), not className (singular) */}
      {/* Indicates the prefix for the CSS classes to be used for the transition */}
      classNames="fade-slide"
    >
      <div className="Modal">
        <h1>A Modal</h1>
        <button className="Button" onClick={props.closed}>
          Dismiss
        </button>
      </div>
    </CSSTransition>
  );
};

export default modal;

```

*Modal.css*

```jsx
...etc...

.fade-slide-enter {
}

.fade-slide-enter-active {
  animation: openModal 0.4s ease-out forwards;
}

.fade-slide-exit {
}

.fade-slide-exit-active {
  animation: closeModal 1s ease-out forwards;
}

// ignored
.ModalOpen {}
.ModalClosed {}

...etc...
```

**Customizing CSS Classnames**

If there is a need to avoid using the standard [prefix]-[suffix] class names, custom class names can be used in the following manner:

*Modal.js*

Note that `classNames` prop added to the `CSSTransition` component.

```jsx
...etc...

import CSSTransition from 'react-transition-group/CSSTransition';

...etc...

const modal = (props) => {
  return (
    <CSSTransition
      ...etc...
      
      classNames={ {
        enter: '',
        enterActive: 'ModalOpen',
        exit: '',
        exitActive: 'ModalClosed',
      } }
    >
      <div className="Modal">
        <h1>A Modal</h1>
        <button className="Button" onClick={props.closed}>
          Dismiss
        </button>
      </div>
    </CSSTransition>
  );
};

export default modal;

```

*Modal.css*

```jsx
...etc...

.ModalOpen {
  animation: openModal 0.4s ease-out forwards;
}

.ModalClosed {
  animation: closeModal 1s ease-out forwards;
}

// ignored
.fade-slide-enter {}
.fade-slide-enter-active {}
.fade-slide-exit {}
.fade-slide-exit-active {}

...etc...
```
</div>
</div>

<div id="animation-lists">
<button type="button" class="collapsible">+ Animating Lists (TransitionGroup)</button>   
<div class="content" style="display: none;" markdown="1">

The `TransitionGroup` component can be used to animate lists.  Note, however, that it can only wrap either the `Transition` or `CSSTransition` components (e.g. `<li>` must be wrapped in `Transition` or `CSSTransition`).

Essentially, the `TransitionGroup` controls the `in` prop of the child `Transition` or `CSSTransition` components.  Other than that, these components behave as described above.

The `TransitionGroup`

*List.js*

```jsx
import React, { Component } from 'react';
import TransitionGroup from 'react-transition-group/TransitionGroup';
import CSSTransition from 'react-transition-group/CSSTransition';

import './List.css';

class List extends Component {
  state = {
    items: [1, 2, 3],
  };

  addItemHandler = () => {
    this.setState((prevState) => {
      return {
        items: prevState.items.concat(prevState.items.length + 1),
      };
    });
  };

  removeItemHandler = (selIndex) => {
    this.setState((prevState) => {
      return {
        items: prevState.items.filter((item, index) => index !== selIndex),
      };
    });
  };

  render() {
    const listItems = this.state.items.map((item, index) => (
      <CSSTransition key={index} classNames="fade" timeout={300}>
        <li className="ListItem" onClick={() => this.removeItemHandler(index)}>
          {item}
        </li>
      </CSSTransition>
    ));

    return (
      <div>
        <button className="Button" onClick={this.addItemHandler}>
          Add Item
        </button>
        <p>Click Item to Remove.</p>
        <TransitionGroup component="ul" className="List">
          {listItems}
        </TransitionGroup>
      </div>
    );
  }
}

export default List;
```

*List.css*

```jsx
.List {
  list-style: none;
  margin: 0 auto;
  padding: 0;
  width: 280px;
}

.ListItem {
  margin: 0;
  padding: 10px;
  box-sizing: border-box;
  width: 100%;
  border: 1px solid #521751;
  background-color: white;
  text-align: center;
  cursor: pointer;
}

.ListItem:hover,
.ListItem:active {
  background-color: #ccc;
}

.fade-enter {
  opacity: 0;
}

.fade-enter-active {
  opacity: 1;
  transition: opacity 0.3s ease-out;
}

.fade-exit {
  opacity: 1;
}

.fade-exit-active {
  opacity: 0;
  transition: opacity 0.3s ease-out;
}
```

*App.js*

```jsx
...etc...

import List from './components/List/List';

class App extends Component {
  
  ...etc...

  render() {
    return (
      <div className="App">

        ...etc...

        <h3>Animating Lists</h3>
        <List />
      </div>
    );
  }
}

export default App;
```
</div>
</div>

<div id="animation-alt">
<button type="button" class="collapsible">+ Alternative Animation Packages</button>   
<div class="content" style="display: none;" markdown="1">

**react-motion**

* Further information: [https://github.com/chenglou/react-motion](https://github.com/chenglou/react-motion)

This package behaves in a totally different way to `react-trasition-group`.  `react-motion` tries to use real-world physics to interpolate between states, rather than leaving the configuration to the user.  It can be complex to use, and cannot handle some types of animation.

**react-move**

* Further information: [https://github.com/sghall/react-move](https://github.com/chenglou/react-motion)

`react-move` always works with objects that describe the state of an animation.  This enables much more complex animations (and accordingly is a bit more complex to use).

**react-router-transition**

* Further information: [https://github.com/maisano/react-router-transition](https://github.com/maisano/react-router-transition)

This builds on top of `react-motion` to create animated transitions between routes (switching between pages).  It is much easier to do route transitions using this package than `react-transition-group`.

</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="saga">
<button type="button" class="collapsible">+ Redux Saga</button>   
<div class="content" style="display: none;" markdown="1">

<div id="saga-intro">
<button type="button" class="collapsible">+ Introduction</button>   
<div class="content" style="display: none;" markdown="1">
  
Redux Saga is an alternative to Redux Thunk.  The goal of Redux Saga is to provide a clearer separation between actions and side-effects, so that code is cleaner and easier to test.

Full documentation for Redux Saga can be found here:
* [https://redux-saga.js.org/](https://redux-saga.js.org/)

* Install: `npm install redux-saga`
* Import: `import { put, take, takeEvery, call, delay, race } from 'redux-saga/effects'`

A "saga" is essentially a function that runs in response to actions and handles all of the side-effects (e.g. accessing local storage, or querying a server) associated with the action.
   * A side-effect is any behaviour that does not directly affect the Redux store (it might change the state, but is not directly consumed by the reducer).

More specifically, a saga is an example of a **Generator**, which is a special form of function that allows code to be paused and resumed.

The basic pattern for the Redux Saga approach is:
1. A central saga file is created that exposes all other sagas: 
   * `export function rootSaga() { yield takeEvery(actionTypes.INITIATE_SOMETHING, doSideEffectsSaga); ...etc... }`
1. The sagas are registered with the middleware:
   * `sagaMiddleware.run(rootSaga);`
1. An action is requested somewhere in the app:
   * `doSomething = () => { dispatch(actions.initiateSomething()); }`
1. An action trigger id is returned by an action creator:
   * `initiateSomething = () => { return { type: actionTypes.INITIATE_SOMETHING, }; }`
1. The watcher intercepts the action trigger id and triggers the related saga, which performs side-effects and then returns a reducer trigger id:
   * `function* doSideEffectsSaga() { yield sideEffect(); yield put({ type: actionTypes.COMPLETE_SOMETHING, }); }`
1. The reducer intercepts the trigger id and triggers a related action:
   * `switch (action.type) { case actionTypes.COMPLETE_SOMETHING: { return updateStateOfSomethingInStore(state, action); } }`
1. The action updates the Redux store:
   * `updateStateOfSomethingInStore = (state, action) => { return updateStore(state, updatedState); };`

</div>
</div>

<div id="saga-functions">
<button type="button" class="collapsible">+ Common Functions</button>   
<div class="content" style="display: none;" markdown="1">

The functions provided by Redux Saga are generally known as "effects", since they tend to trigger side-effects (actions other than those that update the store).

## put() 

This is a non-blocking function is the equivalent of Redux's `dispatch()`.

The function passes an object to the middleware, which will forward it to the reducer, which can then update the store.  

The object consists of a well-known `type` pattern and (optionally) any additional properties required by the reducer.

An example might be:

`put({type: 'SET_INCREMENT', inc: 5})`

This returns an object with the form `{ PUT: {type: 'SET_INCREMENT', inc: 5} }` to the middleware.  
* The `type` is the trigger pattern that `takeEvery()` (or a similar function) is watching for.  
* The middleware will combine any other properties into a single `action` object before passing it to the reducer.

## takeEvery()

`takeEvery()` is a non-blocking function that watches for objects passed to the middleware by `put()` and then checks if they have a specific `type` property. When the property is matched, a specific "saga" function is triggered.

An example might be:

```js
yield takeEvery('SET_INCREMENT', function* setIncrementSaga(action) {
  yield put(actions.setIncrement(action.inc));
});
```

Any properties required by the saga function (e.g. `inc` in the above example) will be included in the object passed by `put()`.  The middleware extracts these properties and passes them to the saga function as a single `action` object.

**Under The Covers**

The `takeEvery()` function is actually a wrapper on a more powerful, lower-level implementation that use the `take()` and `fork()` functions.  An example of what the lower-level implementation might look like this is the following:

```js
const takeEvery = (patternOrChannel, saga, ...args) => fork(function*() { // start function in parallel
  while (true) {
    const action = yield take(pattern) // wait for pattern to be matched and take() to yield an action
    yield fork(saga, ...args.concat(action)) // start action in parallel
    // loop back to take() and wait for pattern
  }
})
```

This approach allows `takeEvery()` to handle multiple saga functions in parallel, although there is no guarantee that the tasks will complete in the same order they were started.  

Note that there is a similar function called `takeLatest()`, which will only allows the latest requested action to complete (all previously started ones will be canceled).

For finer control of the flow of actions, the lower-level `take()` function needs to be used.

## take()

As noted above, the `takeEvery()` function is based on the `take()` function, which waits for a specified pattern to be passed by `put()` and then returns a specific saga function.  Unlike `takeEvery()`, `take()` is a blocking function, which will wait until the pattern is matched. 

One particular use of `take()` is if there is a desire to control the flow of actions, such as in the following example:

```js
function* loginFlow() {
  while (true) {
    yield take('LOGIN') // wait for login
    // ... perform the login logic
    yield take('LOGOUT') // wait for logout
    // ... perform the logout logic
  }
}
```

In this case, 'LOGIN' will always be followed by 'LOGOUT', which in turn will always be followed by 'LOGIN', etc.

For further discussion of how to implement non-blocking flow control using `take()`, see here:
* [https://redux-saga.js.org/docs/advanced/NonBlockingCalls.html](https://redux-saga.js.org/docs/advanced/NonBlockingCalls.html)

## call()

`call()` is a function that allows another function or generator to be passed to the middleware for execution.

For example, the following function:

`server.doQuery(url, queryId)`

could be written as:

`call([server, "doQuery"], url, queryId)`

One of the primary reasons why this is desirable is that it makes it much easier to test the generator.

`call()` returns an object with the form `{ CALL: {fn: [server, doQuery], args: [url, queryId]} }` to the middleware.  The middleware then invokes the function and evaluates the result.  The subsequent behaviour depends upon the result:
* If the result is a generator function, the parent generator will be suspended until the child generator completes.  The parent will then resume with the value returned by the child.
* If the result is a normal function that returns a promise, the parent generator will be suspended until the promise is settled.  The parent will then resume with the value resolved by the promise.
* If the result is neither a generator nor a promise, the result will be immediately returned and the parent generator will resume.

For comparison, if, rather than using `call()`, the function is yielded directly (`yield doQuery(url, queryId)`), `doQuery()` will be invoked *first*, with the *result* being returned to the middleware.  Using `call()`, the middleware controls when the function is invoked.

## delay()

`delay()` is the Redux Saga equivalent of `setTimeout()` and is a blocking function.

If an existing action creator looks like this:

*actions/cleanUp.js*

```js
export const checkCloseWindow = (timeout) => {
  return dispatch => {
    setTimeout(() => {
      dispatch(closeWindow());
    }, timeout);
  };
};

export const closeWindow = () => {
  // close window
};
```

An alternative approach, using `delay` could be:

*actions/cleanUp.js*

```js
export const checkCloseWindow = (timeout) => {
  return {
    type: 'CHECK_CLOSE_WINDOW',
    timeout: timeout
};

export const closeWindow = () => {
  // close window
};
```

*sagas/actions.js*

```js
export {
  checkCloseWindowSaga
} from './cleanUp';
```

*sagas/watcher.js*

```js
export function* watcher() {
  yield takeEvery('CHECK_CLOSE_WINDOW', checkCloseWindowSaga);
}
```

*actions/actions.js*

```js
export {
  closeWindow
} from './cleanUp';
```

*sagas/cleanUp.js*

```js
export function* checkCloseWindowSaga(action) {
  yield delay(action.timeout)
  yield put(actions.closeWindow);
}
```

## fork()

As the name suggests, `fork()` launches Effects in parallel and is non-blocking.  However, the parent Saga can only complete once all attached child effects have also completed.

Take, for example, the following:

```js
import { fork, call, put, delay } from 'redux-saga/effects'
import api from './somewhere/api' // app specific
import { receiveData } from './somewhere/actions' // app specific

function* fetchAll() {
  const task1 = yield fork(fetchResource, 'users')
  const task2 = yield fork(fetchResource, 'comments')
  yield delay(1000)
}

function* fetchResource(resource) {
  const {data} = yield call(api.fetch, resource)
  yield put(receiveData(data))
}

function* main() {
  yield call(fetchAll)
}
```

`call(fetchAll)` will terminate after:

1. The `fetchAll()` body itself terminates, this means all 3 effects are performed. Since fork effects are non blocking, the task will block on `delay(1000)`
1. The 2 forked tasks terminate, i.e. after fetching the required resources and putting the corresponding receiveData actions

So the whole task will block until a delay of 1000 millisecond passed and both task1 and task2 finished their business.

Say for example, the delay of 1000 milliseconds elapsed and the 2 tasks haven't yet finished, then `fetchAll()` will still wait for all forked tasks to finish before terminating the whole task.

With regard to error handling, if at a moment, for example, `fetchAll()` is blocked on the `delay(1000)` Effect, and say, task1 failed, then the whole `fetchAll()` task will fail causing cancellation of all other pending tasks. This includes:

1. The main task (the body of `fetchAll()`): cancelling it means cancelling the current Effect `delay(1000)`
1. The other forked tasks which are still pending. i.e. task2 in our example.
1. The `call(fetchAll)` will raise itself an error which will be caught in the catch body of main

Note we're able to catch the error from `call(fetchAll)` inside main only because we're using a blocking call. And that we can't catch the error directly from `fetchAll()`. This is a rule of thumb, **you can't catch errors from forked tasks**. 

```js
...etc...

function* main() {
  try {
    yield call(fetchAll)
  } catch (e) {
    // handle fetchAll errors
  }
}
```

## spawn()

The `spawn()` function is essentially the same as `fork()` except that the launched processes are detached from the parent saga; once started they have no connection back to the parent.  This means that each spawned saga must be cancalled individually, and any errors will not be propagated back to the parent.

## all()

An alternative to using `fork()` is the `all()` Effect, where an array of Effects is passed to `all()`, each of which will be launched as a process in parallel.

Taking the example used in the `fork()` section above, note that this can be rewritten as:

```js
function* fetchAll() {
  yield all([
    call(fetchResource, 'users'),
    call(fetchResource, 'comments'),
  ])
  yield delay(1000)
}
```

The result will be similar except for two significant details:
* The `all()` effect is blocking, so `delay(1000)` is not executed until all children sagas complete, while `fork()` effects are non-blocking so `delay(1000)` is executed immediately after yielding the fork effects.
* You can get task descriptors when using `fork()` effects, so in the subsequent code you can cancel/join the forked task via task descriptors. This is not possible in the `all()` case.

A work around for these two differences is to combine `all()` and `fork()` in the following manner:

`const [task1, task2, task3] = yield all([ fork(saga1), fork(saga2), fork(saga3) ])`

In this case, since the `fork()` effects are non-blocking, `all()` will return immediately, and the returned tasks can be used to cancel/join a process.  It is not possible, however, to catch errors in the parent task.

## race()

The `race()` function is useful in cases where you want to run several effects in parallel but you only care about the result from the first to complete.  Essentially, the effects "race" to complete.

A simple example of this would be setting a timeout for an effect, e.g.:

```js
import { race, take, put, call, delay } from 'redux-saga/effects'

function* startPollingSaga(action) {
    // Race the following commands with a timeout of 1 minute
    const { response, cancel, failed, timeout } = yield race({
      response: call(checkJobStatus), // start the effect
      cancel: take("CANCEL_POLLING"), // check if effect canceled
      failed: take("POLLING_FAILED"), // check if effect failed
      timeout: call(delay, 60000)     // check if timeout exceeded
    });
    
    // handle failure scenario
    if (failed) {
      yield put({type: "HANDLE_POLLING_FAILURE"});
    }
}
```

</div>
</div>

<div id="saga-compare">
<button type="button" class="collapsible">+ Thunk vs Saga</button>   
<div class="content" style="display: none;" markdown="1">

## Redux Thunk Example

*index.js*

* Register the thunk middleware.

```js
...etc...

import thunk from 'redux-thunk';

...etc...

const store = createStore(
  rootReducer,
  composeEnhancers(applyMiddleware(thunk))
);

...etc...
```

*store/actions/actionTypes.js*

* Create identifiers for sign-out actions.

```js
...etc...

export const AUTH_SIGN_OUT = 'AUTH_SIGN_OUT';

...etc...
```

*store/actions/auth.js*

* Create sign-out actions.

```js
...etc...

const AUTH_TOKEN = 'AUTH_TOKEN';
const AUTH_TOKEN_EXPIRATION = 'AUTH_TOKEN_EXPIRATION';
const AUTH_USER_ID = 'AUTH_USER_ID';

...etc...

// delete the token from localStorage
const removeTokenFromLocalStorage = () => {
  localStorage.removeItem(AUTH_TOKEN);
  localStorage.removeItem(AUTH_TOKEN_EXPIRATION);
  localStorage.removeItem(AUTH_USER_ID);
};

// Remove the token from localStorage when the user logs out.
// Note that this function executes both side-effects and notifies
// that sign-out should occur.
export const authSignOut = () => {
  removeTokenFromLocalStorage();
  return {
    type: actionTypes.AUTH_SIGN_OUT,
  };
};

// Log the user out of the firebase instance
// and delete the token.
// Called from wherever logout is required
// using dispatch(actions.authSignOut()).
export const signOut = () => {

  // this is the "thunk"
  return (dispatch) => {
    fire
      .auth()
      .signOut()
      .then((response) => {
        dispatch(authSignOut());
      })
      .catch((err) => {
        console.log(err);
        dispatch(authFail(err));
      });
  };
};
```

*store/actions/index.js*

* Export action creators related to sign-out

```js
...etc...

export {
  ...etc...
  signOut,
} from './auth';
```

*store/reducers/auth.js*

* Create a reducer that updates the Redux store with the new login state.

```js
import * as actionTypes from '../actions/actionTypes';
import { updateObject } from '../../shared/utility';

const initialState = {
  userId: null,
  token: null,
  error: null,
  loading: false,
  authRedirectPath: '/',
};

...etc...

const authSignOut = (state, action) => {
  return updateObject(state, { token: null, userId: null });
};;

...etc...

const reducer = (state = initialState, action) => {
  switch (action.type) {
    ...etc...

    case actionTypes.AUTH_SIGN_OUT: {
      return authSignOut(state, action);
    }
    
    ...etc...
  }
};

export default reducer;
```

---------------------------------------------------------------

## Redux Saga Example

*index.js*

* Register the logout watcher with the saga middleware.

```js
...etc...

import createSagaMiddleware from 'redux-saga';

import { watchAuth } from './store/sagas/index';

...etc...

const sagaMiddleware = createSagaMiddleware();

const store = createStore(
  rootReducer,
  composeEnhancers(applyMiddleware(thunk, sagaMiddleware))
);

sagaMiddleware.run(watchAuth);

...etc...
```

*store/actions/actionTypes.js*

* Create identifiers for sign-out actions.

```js
...etc...

export const AUTH_INITIATE_SIGN_OUT = 'AUTH_INITIATE_SIGN_OUT';
export const AUTH_SIGN_OUT = 'AUTH_SIGN_OUT';
export const AUTH_SIGN_OUT_SUCCEED = 'AUTH_SIGN_OUT_SUCCEED';

...etc...
```

*store/sagas/auth.js*

* Create a saga that executes the sign-out actions.

```js
import { put } from 'redux-saga/effects';

...etc...

const AUTH_TOKEN = 'AUTH_TOKEN';
const AUTH_TOKEN_EXPIRATION = 'AUTH_TOKEN_EXPIRATION';
const AUTH_USER_ID = 'AUTH_USER_ID';

...etc...

// delete the token from localStorage
function* removeTokenFromLocalStorage() {
  yield localStorage.removeItem(AUTH_TOKEN);
  yield localStorage.removeItem(AUTH_TOKEN_EXPIRATION);
  yield localStorage.removeItem(AUTH_USER_ID);
}

// logout from firebase
function doLogout() {
  return fire.auth().signOut();
}

// clean-up local storage
export function* authInitiateSignOutSaga() {
  // run side-effects (i.e. clean-up)
  yield removeTokenFromLocalStorage();
  // attempt to logout from server
  yield put(actions.authSignOut());
}

// log the user out of the firebase instance
export function* authSignOutSaga(action) {
  try {
    yield doLogout();
    yield put(actions.authSignOutSucceed());
  } catch (err) {
    console.log(err);
    yield put(actions.authFail(err));
  }
}
```

*store/sagas/index.js*

* Create a watcher for the sign-out actions.

```js
import { takeEvery } from 'redux-saga/effects';

import * as actionTypes from '../actions/actionTypes';
import {
  authInitiateSignOutSaga,
  authSignOutSaga,
} from './auth';


export function* watchAuth() {
  // sets up a listener for id and then
  // executes function when it appears
  yield takeEvery(actionTypes.AUTH_INITIATE_SIGN_OUT, authInitiateSignOutSaga); // clean-up
  yield takeEvery(actionTypes.AUTH_SIGN_OUT, authSignOutSaga); // sign-out
}
```

*store/actions/auth.js*

* Create the sign-out actions.

```js
import * as actionTypes from '../actions/actionTypes';

...etc...

// clean-up local storage before sign-out
export const authInitiateSignOut = () => {
  return {
    type: actionTypes.AUTH_INITIATE_SIGN_OUT,
  };
};

// log the user out of the firebase instance
export const authSignOut = () => {
  return {
    type: actionTypes.AUTH_SIGN_OUT,
  };
};

// clear the token from the Redux store
export const authSignOutSucceed = () => {
  return {
    type: actionTypes.AUTH_SIGN_OUT_SUCCEED,
  };
};
```

*store/actions/index.js*

* Export action creators related to sign-out

```js
...etc...

export {
  ...etc...
  authInitiateSignOut,
  authSignOut,
  authSignOutSucceed,
} from './auth';
```

*store/reducers/auth.js*

* Create a reducer that updates the Redux store with the new login state.

```js
import * as actionTypes from '../actions/actionTypes';
import { updateObject } from '../../shared/utility';

const initialState = {
  userId: null,
  token: null,
  error: null,
  loading: false,
  authRedirectPath: '/',
};

...etc...

const authSignOutSucceed = (state, action) => {
  return updateObject(state, { token: null, userId: null });
};;

...etc...

const reducer = (state = initialState, action) => {
  switch (action.type) {
    ...etc...

    case actionTypes.AUTH_SIGN_OUT_SUCCEED: {
      return authSignOutSucceed(state, action);
    }
    
    ...etc...
  }
};

export default reducer;
```

</div>
</div>

<div id="saga-promises">
<button type="button" class="collapsible">+ Handling Promises</button>   
<div class="content" style="display: none;" markdown="1">

In cases where a function returns a promise (such as when querying a web server), the `promise().then().catch()` syntax is not used (due to the complications present by the asynchronous nature of generators).

So, if we consider the following example:

```js
export const queryIngredients = () => {
  return (dispatch) => {
    axios
      .get('/ingredients.json')
      .then((response) => {
        dispatch(setIngredients(response.data));
      })
      .catch((error) => {
        console.log(error);
        dispatch(fetchIngredientsFailed());
      });
  };
};
```

To be converted to a saga, this should be implemented in the following manner:

```js
export function* queryIngredientsSaga(action) {
  try {
    // yield wait until the promise is resolved and
    // then return the *value* of the promise
    const response = yield axios.get('/ingredients.json');
    
    // the resolved value can then be returned using the
    // usual yield put() pattern.
    yield put(actions.setIngredients(response.data));
  } catch (error) {
    // for error handling, try/catch is used, rather
    // than .catch().
    yield console.log(error);
    yield put(actions.fetchIngredientsFailed());
  }
}
```

</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="hooks">
<button type="button" class="collapsible">+ React Hooks</button>   
<div class="content" style="display: none;" markdown="1">

<div id="hooks-intro">
<button type="button" class="collapsible">+ Introduction</button>   
<div class="content" style="display: none;" markdown="1">
  
React Hooks were introduced in React 16.8.  They extend the functionality of Functional Components to reproduce - and replace - functionality seen in Class-Based Components.  In particular they introduce State Management and the equivalent of Lifecycle Hooks.  They make it possible to build complete applications without using Class-Based Components.  Hooks are intended to be highly re-usable and are independent of components.

* Lifecycle Hooks (a.k.a. Lifecycle Methods) are not related to React Hooks, although React Hooks can replicate their functionality.
* React Hooks are functions (as opposed to components).  
* The de-facto standard naming convention for React Hooks is `useXYZ()` (e.g. `useState()`).

Hooks can be used for the following:
   * Managing state
   * Side effects (e.g. http requests)
   * Sharing stateful or stateless logic across multiple components

**Rules for Hooks**
1. Hooks can only be used in Functional Components (or other castables ?????).
1. Hooks can only be used on the root level of a component (you cannot use them inside child functions or blocks, such as `if` statements).

</div>
</div>

<div id="hooks-useState">
<button type="button" class="collapsible">+ useState()</button>   
<div class="content" style="display: none;" markdown="1">

**Overview**

Probably the most important hook is the `useState()` function, which allows Functional Components to update the application state.
  * When using `useState()`, the state can be initialized with any value (unlike class-based state that can only use simple objects).
  * `useState()` returns an array with exactly two elements.
     * The first element is the current state.
     * The second element will always be a update function that allows the state to be overwritten.
  * This update function returned by `useState()` requires that the **entire** state be overwritten; it does not allow specific properties to be updated (unlike `setState()`).

NOTE: If the state is updated multiple times in the same render, there is a risk that the current state may be out of date (due to the unpredictable way in which rendering happens).  To avoid this, the actual updating can be delegated to a function that can be passed as an argument to the update function.  In this case, the delegate function will receive the latest state, even if it hasn't yet been fully committed for this render cycle.

**Using useState()**

An example implementation using `useState()` is the following:

*IngredientForm.js*

```jsx
import React, { useState } from 'react';

...etc...

const IngredientForm = React.memo((props) => {
  
  // get initial state at beginning of render cycle
  const [initialState, updateState] = useState({ title: '', amount: '' });

  const submitHandler = (event) => {
    event.preventDefault();
    // ...
  };

  return (
    <section className="ingredient-form">
      <Card>
        <form onSubmit={submitHandler}>
          <div className="form-control">
            <label htmlFor="title">Name</label>
            <input
              type="text"
              id="title"
              value={initialState.title}
              onChange={(event) => {
                // assign new value to variable, to avoid
                // issues with closure (function in function)
                const newTitle = event.target.value;

                /* Update latest state, not initial state */
                updateState((latestState) => ({
                  title: newTitle,
                  amount: latestState.amount,
                }));
              } }
            />
          </div>
          <div className="form-control">
            <label htmlFor="amount">Amount</label>
            <input
              type="number"
              id="amount"
              value={initialState.amount}
              onChange={(event) => {
                // assign new value to variable, to avoid
                // issues with closure (function in function)
                const newAmount = event.target.value;

                /* Update latest state, not initial state */
                updateState((latestState) => ({
                  title: latestState.title,
                  amount: newAmount,
                }));
              } }
            />
          </div>
          <div className="ingredient-form__actions">
            <button type="submit">Add Ingredient</button>
          </div>
        </form>
      </Card>
    </section>
  );
});

export default IngredientForm;
```

Note that this example has three issues:
1) There is a closure issue that means that care needs to be taken to ensure the correct value is passed into the update function.
2) Since there is only a since state object, care must be taken to merge in values for all properties, even if they haven't changed.
3) Since unchanged values must be merged, care must be taken to ensure that the latest version of the values are used.

These three issues can be avoided if, rather than using a single state object, a different state is used for each property.

If the above example is updated along these lines, the following is the result:

*IngredientForm.js*

```js
import React, { useState } from 'react';

...etc...

const IngredientForm = React.memo((props) => {

  // get initial state at beginning of render cycle
  const [enteredTitle, setEnteredTitle] = useState('');
  const [enteredAmount, setEnteredAmount] = useState('');

  const submitHandler = (event) => {
    event.preventDefault();
    // ...
  };

  return (
    <section className="ingredient-form">
      <Card>
        <form onSubmit={submitHandler}>
          <div className="form-control">
            <label htmlFor="title">Name</label>
            <input
              type="text"
              id="title"
              value={enteredTitle}
              onChange={(event) => {
                setEnteredTitle(event.target.value);
              } }
            />
          </div>
          <div className="form-control">
            <label htmlFor="amount">Amount</label>
            <input
              type="number"
              id="amount"
              value={enteredAmount}
              onChange={(event) => {
                setEnteredAmount(event.target.value);
              } }
            />
          </div>
          <div className="ingredient-form__actions">
            <button type="submit">Add Ingredient</button>
          </div>
        </form>
      </Card>
    </section>
  );
});

export default IngredientForm;
```

**Passing State Between Components**

`props` are used to pass state from parent to child.

Extending the example above, IngredientForm is a child of the Ingredients component, which controls the list of ingredients.  This means that Ingredients can pass props (in the following case, an `addIngredientHandler()` function) to IngredientForm.

The Ingredients component maintains its own state, which can be updated by addIngredientHandler

*Ingredients.js*

This is the parent object that controls the list of ingredients.

```js
import React, { useState } from 'react';

import IngredientForm from './IngredientForm';
import IngredientList from './IngredientList';
import Search from './Search';

function Ingredients() {
  const [ingredients, setIngredients] = useState([]);

  const addIngredientHandler = (ingredient) => {
    setIngredients((latestIngredients) => [
      ...latestIngredients,
      { id: Math.random().toString(), ...ingredient },
    ]);
  };

  return (
    <div className="App">
      {/* Pass handler to form via props */}
      <IngredientForm onAddIngredient={addIngredientHandler} />

      <section>
        <Search />
        <IngredientList ingredients={ingredients} onRemoveItem={() => {} } />
      </section>
    </div>
  );
}

export default Ingredients;
```

*IngredientForm.js*

The form is a child of the list of ingredients.

```js
...etc...

const IngredientForm = React.memo((props) => {

  ...etc...

  const submitHandler = (event) => {
    event.preventDefault();

    // call handler from props passed by parent Ingredients component
    props.onAddIngredient({ title: enteredTitle, amount: enteredAmount });
  };

  return (
    <section className="ingredient-form">
      <Card>
        <form onSubmit={submitHandler}>
        
          ...etc...
          
          <div className="ingredient-form__actions">
            <button type="submit">Add Ingredient</button>
          </div>
        </form>
      </Card>
    </section>
  );
});

export default IngredientForm;
```

</div>
</div>

<div id="hooks-perf-overview">
<button type="button" class="collapsible">+ Overview of Performance-Related Hooks</button>   
<div class="content" style="display: none;" markdown="1">

There are 3 hooks that can be used to improve rendering performance for functional components:
  * `useEffect()` 
    * Behaviour: controls whether a function runs.
    * Returns: does not return a result.
  * `useCallback()`
    * Behaviour: controls whether a function is re-created.
    * Returns: returns a call-back to either a new function or a cached function.
  * `useMemo()`
    * Behaviour: controls whether a function returns a new result.
    * Returns: returns either a new result or a cached result.

There is also `React.memo()`, which is effectively the same as `useMemo()` but is not a hook (it's an HOC).  This can also be used with class components.
</div>
</div>

<div id="hooks-useEffect">
<button type="button" class="collapsible">+ useEffect()</button>   
<div class="content" style="display: none;" markdown="1">

**Overview**

Another important hook is the `useEffect()` function, which allows side-effects, such as querying data sources, to be performed.  A side-effect is any action that cannot be handled as part of the normal rendering flow.

The function can be reference multiple times in the same component (as long as it obeys the general rules for hooks).

By default, `useEffect()` is called **after every** render cycle.  This can be a problem because if `useEffect()` updates the app, this will force a re-render, which will call `useEffect()` again, which will force a re-render, etc.

**Controlling The Function**

To avoid an infinite loop, `useEffect()` can be controlled by passing a dependency (an object, or array of objects) into the function and the function only reacts if the dependency has changed.  In this case, the function emulates `componentDidUpdate()`.

For example,

```js
useEffect( () => { somefunction; }, [someobject] ); )
```

To have the function run only the **first time** an object is rendered, pass an empty array.  In this case, the function emulates `componentDidMount()`.

```js
useEffect( () => { somefunction; }, [] ); )
```

NOTE: the dependencies should be listed only if they actually change so, for example, `props` should not be listed as a dependency unless the goal is for the component to rerender whenever any child of `props` changes.  A typical fix for this is to use object destructing to extract out the specific objects of interest from `props`, e.g.

```js

const { onLoadIngredients } = props;

// avoid useEffect( () => { somefunction; }, [props.onLoadIngredients] ); )
useEffect( () => { somefunction; }, [onLoadIngredients] ); )
```

NOTE: the dependencies must exist in the enclosing context if there are to be used as triggers.

**Cleaning Up**

The `useEffect()` function can also be used to clean-up after a render cycle, or when a component is unmounted (destroyed).

This is done by returning a function from `useEffect()`, e.g.

```js
useEffect( () => { somefunction; return () => { cleanupfunction }; }, [props.somedata] );
```

The returned function runs **BEFORE** the main `useEffect()` function runs, but **AFTER** the (first) render cycle.

If an empty array is passed, the cleanup function will only run when the component is unmounted (destroyed).

</div>
</div>

<div id="hooks-useCallback">
<button type="button" class="collapsible">+ useCallback()</button>   
<div class="content" style="display: none;" markdown="1">

To understand `useCallback()`, it is crucial to remember that JavaScript functions are objects, which means that, by default, they get created anew whenever they are called.  If this is not desirable, it is necessary to cache the function and re-use the cached version.

At first glance, the `useCallback()` hook appears to work in a similar fashion to the `useEffect()` hook: it allows control over how a function behaves based on changes to a dependency.  It does not, however, actually run a function; it merely returns a callback to a function.

The hook works by caching the wrapped function and then only re-creating it once a dependency has changed.

For example, in the following case it may not be desirable for `setIngredients()` to be created anew every time `filterIngredientsHandler` is triggered (e.g. this might involve an expensive HTTP call):

```js
  const filteredIngredientsHandler = (filteredIngredients) => {
    setIngredients(filteredIngredients);
  };
```

To avoid the unnecessary re-runs, the call to `setIngredients()` is wrapped with `useCallback()`:

```js
  const filteredIngredientsHandler = useCallback((filteredIngredients) => {
    setIngredients(filteredIngredients);
  }, []);
```

NOTE: in this particular case, an empty array is passed as the dependency, which means that the function will be created the **first time**, but in future a cached version will always be used.

NOTE: as in the `useEffect()` case, the dependencies must exist in the enclosing context (so, in the above example, `setIngredients()` could be used as a dependency but `filterIngredients` cannot).

</div>
</div>

<div id="hooks-useMemo">
<button type="button" class="collapsible">+ useMemo() vs React.memo()</button>   
<div class="content" style="display: none;" markdown="1">

In terms of functionality, there is no significant difference between `useMemo()` and `React.memo()`; both memorize the result of a function and only re-run the function if the `props` change.  Having said that, `React.memo()` can be used in both class and functional components (it is not a hook!), whereas `useMemo()` can only be used in functional components.

Note that these functions differ from `useCallback()` in that `useCallback()` returns a **function**, whereas `useMemo()` and `React.memo()` both return the **result** of a function.

`React.memo()`:

```js
const Counter = (props) => {
  console.log('Render: ', props.children);

  return (
    <div>
      {props.children}: {props.value}
    </div>
  );

  // areEqual is an optional function that allows finer
  // controls over how changes in props are detected
  const areEqual = (prevProps, nextProps) => {
    /*
      return true if passing nextProps to render would return
      the same result as passing prevProps to render,
      otherwise return false
    */
  };
};

// if neither value nor children change, the Counter 
// function is not re-run.
// areEqual is an optional argument
export default React.memo(Counter, areEqual);
```

`useMemo()`:

```js
const renderCounter = (props) => {
  console.log('Render: ', props.children);

  return (
    <div>
      {props.children}: {props.value}
    </div>
  );
};

const Counter = (props) => {
  return useMemo(() => renderCounter(props), [props.children, props.value]);
};

export default Counter
```

**NOTE:** It is possible to make performance worse by use `useMemo()` in small apps, since more time may be spent checking if rendering should happen than actually doing the rendering.

</div>
</div>

<div id="hooks-useRef">
<button type="button" class="collapsible">+ useRef()</button>   
<div class="content" style="display: none;" markdown="1">

In the section on Refs, it is discussed how these are used to access specific elements of the DOM.  Specifically, they are used for accessing HTML elements or class components.  They cannot, however, be used to refer to functional components.

To emulate this behaviour with functional components, the `useRef()` hook is used.

The basic pattern is:
1. Create ref to null before the `return` method: `const myBtnRef = useRef(null);`
1. Add the ref to the element of interest: `<button ref={myBtnRef} onClick={props.clicked}>`
1. Call the ref using the `useEffect()` hook (`.current` gives the current value of the referenced element): `useEffect(() => { myBtnRef.current.click(); }, []);`

The reason the ref must be called from `useEffect()` is that it cannot be called before the functional component has returned (since the elements of the component must be initialized).  

Since `useEffect()` is only called after the `return` method, this makes it an appropriate place to access the ref.

```jsx
import React, { useEffect, useRef } 
        from 'react';

const Cockpit = (props) => {
  const toggleBtnRef = useRef(null);

  // clicks the button after *first* render cycle
  useEffect(() => {
  
    toggleBtnRef.current.click();
    
  }, []); // empty array, so only runs first time

  ...

  return (
    <div>
      <button 
        ref={toggleBtnRef} 
        onClick={props.clicked}
      >
        Toggle Persons
      </button>
    </div>
  );
};
```

</div>
</div>

<div id="hooks-useReducer">
<button type="button" class="collapsible">+ useReducer()</button>   
<div class="content" style="display: none;" markdown="1">

In the case where there are multiple, closely related state changes (e.g. setIngredients, addIngredient, deleteIngredient), an alternative approach to using `useState()` is `useReducer()`.  This can often result in cleaner code as well.

NOTE: There is no connection between `useReducer()` and Redux!

The general pattern for a reducer is:

```js
const myReducer = (currentState, action) => {
  switch (action.type) {
    case 'ACTION1': {
      return doAction1(currentState, action.prop1);
    }
    case 'ACTION2': {
      return doAction2(currentState, action.prop2);
    }
    case 'ACTION3': {
      return doAction2(currentState, action.prop2, action.prop3);
    }
    default: {
      // typically this wouldn't be reached, so maybe:
      throw new Error('Should not get here!');
    }
  }
};

function MyComponent() {
  // startingState could be an empty array []
  const [updatedState, dispatch] = useReducer(myReducer, startingState);
  
  return (
    ...etc...
  );
}
```

For a more concrete example:

```js
import React, { useReducer, useCallback } from 'react';

const ingredientReducer = (currentIngredients, action) => {
  switch (action.type) {
    case 'SET': {
      return action.ingredients;
    }
    case 'ADD': {
      return [...currentIngredients, action.ingredient];
    }
    case 'DELETE': {
      return currentIngredients.filter((ing) => ing.id !== action.id);
    }
    default: {
      throw new Error('Should not get here!');
    }
  }
};

function Ingredients() {
  const [ingredients, dispatch] = useReducer(ingredientReducer, []);

  const filteredIngredientsHandler = useCallback((filteredIngredients) => {
    dispatch({ type: 'SET', ingredients: filteredIngredients });
  }, []);

  const addIngredientHandler = (ingredient) => {
      dispatch({
        type: 'ADD',
        ingredient: { id: ingredient.id, ...ingredient },
      });
  };

  const removeIngredientHandler = (id) => {
    dispatch({ type: 'DELETE', id: id });
  };

  return (
    ...etc...
  );
}

export default Ingredients;
```

</div>
</div>

<div id="hooks-useContext">
<button type="button" class="collapsible">+ useContext()</button>   
<div class="content" style="display: none;" markdown="1">

`useContext()` allows the Context API (discussed previously) to be emulated for functional components.  Its purpose is to share some common context between the multiple components of an app. 

There are two main steps to accomplist this:
1) Wrap the app in an `AuthContextProvider` component, provides access to the shared context throughout the app.
2) Use `useContext()` to access the shared context in a specific functional component.

*context/auth-context.js*

Initially create a context using `React.createContext()`, as in the class component case, but also add an `AuthContextProvider` component that exposes the shared context to any children it wraps.

```jsx
import React, { useState } from 'react';

export const AuthContext = React.createContext({
  isAuth: false,
  logn: () => {},
});

const AuthContextProvider = (props) => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  const loginHandler = () => {
    setIsAuthenticated(true);
  };

  return (
    <AuthContext.Provider
      value={ { login: loginHandler, isAuth: isAuthenticated } }
    >
      {props.children}
    </AuthContext.Provider>
  );
};

export default AuthContextProvider;
```

*index.js*

Wrap the app in the `AuthContextProvider` component.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

import './index.css';
import App from './App';
import AuthContextProvider from './context/auth-context';

ReactDOM.render(
  <AuthContextProvider>
    <App />
  </AuthContextProvider>,
  document.getElementById('root')
);
```

*components/Auth.js*

Obtain a reference to the shared context (using `useContext()`) and then use the shared `login()` function in this component.

```jsx
import React, { useContext } from 'react';

import { AuthContext } from '../context/auth-context';
import './Auth.css';

const Auth = (props) => {
  const authContext = useContext(AuthContext);
  const loginHandler = () => {
    authContext.login();
  };

  return (
    <div className="auth">
      <Card>
        <h2>You are not authenticated!</h2>
        <p>Please log in to continue.</p>
        <button onClick={loginHandler}>Log In</button>
      </Card>
    </div>
  );
};

export default Auth;
```

*App.js*

Obtain a reference to the shared context (using `useContext()`) and then use the shared `isAuth()` property in this component.

```jsx
import React, { useContext } from 'react';

import Ingredients from './components/Ingredients/Ingredients';
import Auth from './components/Auth';
import { AuthContext } from './context/auth-context';

const App = (props) => {
  const authContext = useContext(AuthContext);

  let content = <Auth />;
  if (authContext.isAuth) {
    content = <Ingredients />;
  }
  return content;
};

export default App;
```
</div>
</div>

<div id="hooks-customHooks">
<button type="button" class="collapsible">+ Custom Hooks</button>   
<div class="content" style="display: none;" markdown="1">

If there is duplicate logic that affects the state of the components that use that logic, it not possible extract that logic to a normal function and re-use it (because an event in a child function cannot change the state of the parent function).  This can be done, however, using hooks.

Note: when using custom hooks, you don't have one function shared by multiple components; each functional component get its own snapshot of the hook (i.e. each component gets the same logic, but not the same state).

Also note that hooks get executed for every render cycle, so they need to be coded accordingly.

At its most basic, a simple custom handler might be:

*hooks/error-handler.js*

```js
import { useState, useEffect } from 'react';

// does not need a named function, but must be assigned
// one beginning with "use" in whichever component uses it.
export default (myClient) => {
  const [error, setError] = useState(null);

  const errorHandler = (err) => {
    setError(err ? err : null);
  };

  const errorConfirmedHandler = () => {
    setError(null);
  };

  const trySomething = myClient.doSomething(errorHandler);

  useEffect(() => {
    return trySomething();
  }, [trySomething]);
  
  return [error, errorConfirmedHandler];
};
```

This might be used in the following manner:

*hoc/withErrorHandler.js*

```js
import React from 'react';
import useErrorHandler from '../hooks/error-handler';

const withErrorHandler = (myClient) => {
  return (props) => {
    const [error, clearError] = useErrorHandler(myClient);

    return (
      <Wrapper>
        <Modal show={error} modalClosed={clearError}>
          {error ? error.message : null}
        </Modal>
      </Wrapper>
    );
  };
};

export default withErrorHandler;
```

A slightly more robust example might have the following basic structure:

1. An internal state.
1. A reducer function that inputs an initial state and returns an updated state based on an action.
1. An exported hook (function), with a name beginning with "use".
   * The hook can return anything it wishes (including nothing).  It does not need to have a return pattern similar to `useState()`, for example.
   * The methods that update the state do so by dispatching actions (and data related to the actions) to the reducer.

A generic example might be:

*hooks/useMyHook.js*

```js
import { useReducer, useCallback } from 'react';

const ACTION_TYPE_1 = 'ACTION_TYPE_1';
const ACTION_TYPE_2 = 'ACTION_TYPE_2';
const ACTION_TYPE_3 = 'ACTION_TYPE_3';
const CLEAR = 'CLEAR';

const initialState = {
  prop1: null,
  isActive: false,
  prop3: null,
};

const myHookReducer = (currentHookState, action) => {
  switch (action.type) {
    case ACTION_TYPE_1: {
      return {
        ...currentHookState,
        prop1: action.prop1,
        prop3: action.prop3,
      };
    }
    case ACTION_TYPE_2: {
      return {
        ...currentHookState,
        isActive: true,
      };
    }
    case ACTION_TYPE_3: {
      return {
        ...currentHookState,
        isActive: false,
      };
    }
    case CLEAR: {
      return initialState;
    }
    default: {
      throw new Error('Should not get here!');
    }
  }
};

const useMyHook = () => {
  const [myHookState, dispatch] = useReducer(myHookReducer, initialState);

  // use useCallback(), with an empty array, to avoid this action being
  // re-created every time the parent component is rendered.
  const clear = useCallback(() => dispatch({ type: CLEAR }), []);

  // use useCallback(), with an empty array, to avoid this action being
  // re-created every time the parent component is rendered.
  const updateProps = useCallback((prop1, prop3) => {
    // something to update prop values
  }, []);

  // use useCallback() to avoid this action being
  // re-created every time the parent component is rendered.
  // updateProps() is passed as a dependency, since it too is wrapped
  // with useCallback().
  const doSomething = useCallback(
    (val1, val3) => {
      dispatch({ type: ACTION_TYPE_2 });

      const { updatedVal1, updatedVal3 } = updateProps(val1, val3);
      dispatch({
        type: ACTION_TYPE_1,
        prop1: updatedVal1,
        prop3: updatedVal3,
      });

      dispatch({ type: ACTION_TYPE_3 });
    },
    [updateProps]
  );

  // can return any type of object; in this case a simple
  // JavaScript object
  return {
    prop1: myHookState.prop1,
    isActive: myHookState.isActive,
    prop3: myHookState.prop3,
    doSomething: doSomething,
    clear: clear,
  };
};

export default useMyHook;
```

This hook could then be used in the following manner:

*MyComponent.js*

```js
import React, { useEffect } from 'react';

import useMyHook from './hooks/useMyHook';

// React.memo() is used to ensure that the function 
// only re-runs if props changes
const MyComponent = React.memo((props) => {

  // get references to properties and methods of interest from hook
  const { prop1, isActive, prop3, doSomething, clear } = useMyHook();
  
  // useEffect() runs *after* the render but only if prop1,
  // prop3 or doSomething() have changed
  useEffect(() => {  
    // update the state stored in the hook
    doSomething(prop1, prop3);
  }, [prop1, prop3, doSomething]);

  return (
    <div>
      {isActive ? <span>Prop1: {prop1}</span> : <span>Prop3: {prop3}</span>}
      <button type="button" onClick={clear}>
        Clear
      </button>
    </div>
  );
});

export default MyComponent;
```

</div>
</div>

<div id="hooks-useDispatch">
<button type="button" class="collapsible">+ Redux Hooks: useDispatch &amp; useSelector</button>   
<div class="content" style="display: none;" markdown="1">

Two hooks introduced by Redux allow the `connect()()` function to be replaced.  These hooks are:
   * `useDispatch` - effectively the same as `mapDispatchToProps`
   * `useSelector` - effectively the same as `mapStateToProps`

**`useDispatch()`**

WIP

**`useSelector()`**

`useSelector()` allows specific properties of the current state to be accessed.  For example, in the following case, the `ingredients` object can be accessed directly.

```js
const ingredients = useSelector((state) => state.burgerBuilder.ingredients);
```

WIP

**An Example**

The following is an example of converting a component to use these hooks:

```js
import React, { useState, useEffect } from 'react';
import { connect } from 'react-redux';

...etc...

export const BurgerBuilder = (props) => {

  const onQueryIngredients = props.onQueryIngredients;

  useEffect(() => {
    onQueryIngredients();
  }, [onQueryIngredients]);

  const purchaseHandler = () => {
    if (props.isAuthenticated) {
      setPurchasing(true);
    } else {
      props.onSetAuthRedirectPath('/checkout');
      props.history.push('/auth');
    }
  };

  ...etc...

  return (
    ...etc...
  );
};

const mapStateToProps = (state) => {
  if (state) {
    return {
      ingredients: state.burgerBuilder.ingredients,
      totalPrice: state.burgerBuilder.totalPrice,
      error: state.burgerBuilder.error,
      isAuthenticated: state.auth.token !== null,
    };
  } else {
    return null;
  }
};

const mapDispatchToProps = (dispatch) => {
  return {
    onAddIngredient: (ingName) => dispatch(burgerBuilderActions.addIngredient(ingName)),
    onRemoveIngredient: (ingName) => dispatch(burgerBuilderActions.removeIngredient(ingName)),
    onQueryIngredients: () => dispatch(burgerBuilderActions.queryIngredients()),
    onInitPurchase: () => dispatch(burgerBuilderActions.purchaseInit()),
    onSetAuthRedirectPath: (path) => dispatch(burgerBuilderActions.setAuthRedirectPath(path)),
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(BurgerBuilder);
```

1. Remove the `connect` import, but add imports for `useDispatch` and `useSelector`.
1. Call `useDispatch()` to create a new `dispatch` constant
1. Refactor the contents of `mapDispatchToProps()` into multiple `dispatch()` statements.
1. Refactor the contents of `mapStateToProps` into multiple `useSelector()` statements.
1. Remove the `connect()()` wrapper from the export statement.
1. Remove all references to `props` for all of the constants created by the `dispatch()` and `useSelector()` statements.
1. As necessary, wrap the new calls to `dispatch()` and `useSelector()` with `useCallback()` to avoid infinite calls to `useEffects()`.

```js
import React, { useEffect, useCallback } from 'react';
import { useDispatch, useSelector } from 'react-redux';

...etc...

export const BurgerBuilder = (props) => {

  const dispatch = useDispatch();

  const ingredients = useSelector((state) => state.burgerBuilder.ingredients);
  const totalPrice = useSelector((state) => state.burgerBuilder.totalPrice);
  const error = useSelector((state) => state.burgerBuilder.error);
  const isAuthenticated = useSelector((state) => state.auth.token !== null);

  const onAddIngredient = (ingName) => dispatch(burgerBuilderActions.addIngredient(ingName));
  const onRemoveIngredient = (ingName) => dispatch(burgerBuilderActions.removeIngredient(ingName));
  const onQueryIngredients = useCallback(() => dispatch(burgerBuilderActions.queryIngredients()), [
    dispatch,
  ]);
  const onInitPurchase = () => dispatch(burgerBuilderActions.purchaseInit());
  const onSetAuthRedirectPath = (path) => dispatch(burgerBuilderActions.setAuthRedirectPath(path));

  useEffect(() => {
    onQueryIngredients();
  }, [onQueryIngredients]);
  
  const purchaseHandler = () => {
    if (isAuthenticated) {
      setPurchasing(true);
    } else {
      onSetAuthRedirectPath('/checkout');
      props.history.push('/auth');
    }
  };

  ...etc...

  return (
    ...etc...
  );
};

export default BurgerBuilder;
```
  
</div>
</div>

<div id="hooks-convert">
<button type="button" class="collapsible">+ Converting An App To Use Hooks</button>   
<div class="content" style="display: none;" markdown="1">

**Convert class components to functional components**

```js
import React, { Component } from 'react';

class App extends Component { 
  ...etc...

  render() {

    ...etc...
    
    if (this.props.isAuthenticated) {
    }
    
    return (
      <div>
        ...etc...
      </div>
    );
  }
}
```

1. Remove `Component` and convert to arrow function
1. Extract `return()` from `render()`
1. Remove `render()`
1. Replace `this.props` with `props`

```js
import React from 'react';

const App = (props) => {
  ...etc...
  
  if (props.isAuthenticated) {
  }
  
  return (
    <div>
      ...etc...
    </div>
  );
};
```

&nbsp;

**Replace `componentDidMount()` with `useEffect()`**

```js
import React from 'react';

const App = (props) => {

  componentDidMount() {
    this.props.doSomething();
  }
  
  ...etc...
}
```

1. Import `useEffect`
1. Replace `componentDidMount()` from `useEffect()`
1. Replace `this.props` with `props`
1. Avoid using `props` as a dependency for `useEffect()`

```js
import React, { useEffect } from 'react';

const App = (props) => {

  const doSomething = props.doSomething;
  
  useEffect(() => {
    doSomething();
  }, [doSomething]);
  
  ...etc...
};
```

&nbsp;

**Replace `asyncComponent()` with `React.lazy()`**

```js
import React from 'react';

const asyncCheckout = asyncComponent(() => {
  return import('./containers/Checkout/Checkout');
});

const App = (props) => {  

  let routes = (
    <Switch>
      <Route path="/checkout" component={asyncCheckout} />
      <Redirect to="/" />
    </Switch>
  );
  
  return (
    <div>
      {routes}
    </div>
  );
};
```

1. Replace `asyncComponent()` with `React.lazy()`
1. Rename `asyncCheckout` variable to `Checkout` (so that it can be used as a component)
1. In `Route`, replace `component` with `render`
1. Ensure `props` are passed to components
1. Import `Suspense`
1. Wrap lazy loading code with `Suspense`

```js
import React, { Suspense } from 'react';

const Checkout = React.lazy(() => {
  return import('./containers/Checkout/Checkout');
});

const App = (props) => {  

  let routes = (
    <Switch>
      <Route path="/checkout" render={(props) => <Checkout {...props} />} />
      <Redirect to="/" />
    </Switch>
  );

  return (
    <div>
      <Suspense fallback={<p>Loading...</p>}> 
        {routes}
      </Suspense>
    </div>
  );
};
```

&nbsp;

**Replace `state` with `useState()`**

```js
import React, { Component } from 'react';

class Layout extends Component {
  state = {
    showSideDrawer: false,
  };

  sideDrawerToggleHandler = () => {
    this.setState((prevState) => {
      return { showSideDrawer: !prevState.showSideDrawer };
    });
  };

  render() {
    return (
      <div>
        <Toolbar toggle={this.sideDrawerToggleHandler} />

        <SideDrawer
          isAuth={this.props.isAuthenticated}
          open={this.state.showSideDrawer}
          closed={this.sideDrawerToggleHandler}
        />
      </div>
    );
  }
}
```

1. Import `useState`
1. Replace local `state` with `useState`
   * For large or complex states, use multiple `useState` functions.
1. Replace `setState()` with `useState` setter
1. Replace `this.state` with `useState` value

```js
import React, { useState } from 'react';

const Layout = (props) => {
  const [sideDrawerIsVisible, setSideDrawerIsVisible] = useState(false);

  const sideDrawerToggleHandler = () => {
    setSideDrawerIsVisible(!sideDrawerIsVisible);
  };

  return (
    <div>
      <Toolbar toggle={sideDrawerToggleHandler} />

      <SideDrawer
        isAuth={props.isAuthenticated}
        open={sideDrawerIsVisible}
        closed={sideDrawerToggleHandler}
      />
    </div>
  );
}
```

&nbsp;

**Refactor `componentWillMount()`**

```js
  UNSAFE_componentWillMount() {
    this.reqInterceptor = axios.interceptors.request.use((req) => {
      this.setState({ error: null });
      return req;
    });
    
    this.resInterceptor = axios.interceptors.response.use(
      (res) => {
        return res;
      },
      (error) => {
        this.setState({ error: error });
      }
    );
  }
  
  render() {
    return (
      ...etc...
    );
  }
```

Cannot use `useEffect()` because `componentWillMount()` runs before rendering.

The solution is simply to move the contents of `componentWillMount()` out of the function so that it runs inline.  This will then run before the function renders (i.e. the `return` statement), which is effectively the same behaviour as `componentWillMount()`.

**NOTE:** When wrapping a functional app in `StrictMode` (which create-react-app now does by default), you need to ensure that the Axios error handler explicitly returns a rejected `Promise`, otherwise behaviour may be unexpected (this is related to the face that `StrictMode` causes some functions to run multiple times in dev mode - see [https://stackoverflow.com/questions/60305074/react-strictmode-setstate-function-in-useeffect-is-run-multiple-times-when-effe](here) for further details.)

```js
  const reqInterceptor = axios.interceptors.request.use((req) => {
    setError(null);
    return req;
  });
  
  const resInterceptor = axios.interceptors.response.use(
    (res) => {
      return res;
    },
    (err) => {
      setError(err);
      // required by StrictMode
      return Promise.reject(err);
    }
  );
     
  return (
    ...etc...
  );
```

&nbsp;

**Replace `componentWillUnmount()` with `useEffect()`**

```js
  componentWillUnmount() {
    axios.interceptors.request.eject(this.reqInterceptor);
    axios.interceptors.response.eject(this.resInterceptor);
  }
```

In this case, the purpose of `componentWillUnmount()` is to ensure the code runs when the component exits.  This is effectively the same behaviour as only specifying a clean-up function for `useEffect()`.

```js
import React, { useEffect } from 'react';

  useEffect(() => {
    return () => {
      axios.interceptors.request.eject(reqInterceptor);
      axios.interceptors.response.eject(resInterceptor);
    };
  }, [reqInterceptor, resInterceptor]);
```

&nbsp;

**Assign functions to constants**

```js
  errorConfirmedHandler = () => {
    setError(null);
  };

  render() {
    return (
      <div>
        <Modal modalClosed={this.errorConfirmedHandler} />
      </div>
    );
  }
```

1. Make function a `const`, rather than a method.
1. Call the function without using `this`

```js
  const errorConfirmedHandler = () => {
    setError(null);
  };
    
  return (
    <div>
      <Modal modalClosed={errorConfirmedHandler} />
    </div>
  )
```

&nbsp;

**Replace `shouldComponentUpdate()` with `React.memo()`**

```js
class Modal extends Component {

  shouldComponentUpdate(nextProps, nextState) {
    return nextProps.show !== this.props.show || nextProps.children !== this.props.children;
  }

}

export default Modal;
```

1. Wrap the exported component in `React.memo()`
1. Take the test from `shouldComponentUpdate` and add it to `React.memo()` as a function. 
1. Invert the test (`React.memo()` expects the inverse of `shouldComponentUpdate()`)

```js
const Modal = (props) => {

export default React.memo(
  Modal,
  (prevProps, nextProps) =>
    nextProps.show === prevProps.show && nextProps.children === props.children
);
```
  
</div>
</div>

<div id="hooks-replace-redux">
<button type="button" class="collapsible">+ Replacing Redux With Hooks</button>   
<div class="content" style="display: none;" markdown="1">

Reasons for using Hooks rather than Redux:

1. Want to stay in the React world, to avoid learning Redux
1. Want to avoid including `react-redux` and `redux` in your bundle (to reduce its size)

**Approach 1: Using the Context API**

Downside: the Context API is not optimized for performance; every component that references the context will re-render when the context changes.  This means it should not be used for high frequency updates (e.g. repeated user interactions).  It is fine for low frequency updates, such as setting the theme, or logging in, but otherwise is probably best avoided.

In any event, rather than maintaining the state using a reducer:

*reducers/products.js*

```js
import { TOGGLE_FAV } from '../actions/products';

const initialState = {
  products: [
    {
      id: 'p1',
      title: 'Red Scarf',
      description: 'A pretty red scarf.',
      isFavorite: false
    },
    {
      id: 'p2',
      title: 'Blue T-Shirt',
      description: 'A pretty blue t-shirt.',
      isFavorite: false
    },
    {
      id: 'p3',
      title: 'Green Trousers',
      description: 'A pair of lightly green trousers.',
      isFavorite: false
    },
    {
      id: 'p4',
      title: 'Orange Hat',
      description: 'Street style! An orange hat.',
      isFavorite: false
    }
  ]
};

const productReducer = (state = initialState, action) => {
  switch (action.type) {
    case TOGGLE_FAV:
      const prodIndex = state.products.findIndex(
        p => p.id === action.productId
      );
      const newFavStatus = !state.products[prodIndex].isFavorite;
      const updatedProducts = [...state.products];
      updatedProducts[prodIndex] = {
        ...state.products[prodIndex],
        isFavorite: newFavStatus
      };
      return {
        ...state,
        products: updatedProducts
      };
    default:
      return state;
  }
};

export default productReducer;
```

*index.js*

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { combineReducers, createStore } from 'redux';
import { BrowserRouter } from 'react-router-dom';

import './index.css';
import App from './App';
import productReducer from './store/reducers/products';

const rootReducer = combineReducers({
  shop: productReducer
});

const store = createStore(rootReducer);

ReactDOM.render(
  <Provider store={store}>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </Provider>,
  document.getElementById('root')
);
```

*containers/Products.js*

```js
import React from 'react';
import { useSelector } from 'react-redux';

import ProductItem from '../components/Products/ProductItem';
import './Products.css';

const Products = props => {
  const productList = useSelector(state => state.shop.products);
  return (
    <ul className="products-list">
      {productList.map(prod => (
        <ProductItem
          key={prod.id}
          id={prod.id}
          title={prod.title}
          description={prod.description}
          isFav={prod.isFavorite}
        />
      ))}
    </ul>
  );
};

export default Products;
```

*components/Products/ProductItem.js*

```js
import React from 'react';
import { useDispatch } from 'react-redux';

import Card from '../UI/Card';
import './ProductItem.css';
import { toggleFav } from '../../store/actions/products';

const ProductItem = props => {
  const dispatch = useDispatch();

  const toggleFavHandler = () => {
    dispatch(toggleFav(props.id));
  };

  return (
    <Card style={{ marginBottom: '1rem' }}>
      <div className="product-item">
        <h2 className={props.isFav ? 'is-fav' : ''}>{props.title}</h2>
        <p>{props.description}</p>
        <button
          className={!props.isFav ? 'button-outline' : ''}
          onClick={toggleFavHandler}
        >
          {props.isFav ? 'Un-Favorite' : 'Favorite'}
        </button>
      </div>
    </Card>
  );
};

export default ProductItem;
```

*containers/Favourites.js*

```js
import React from 'react';
import { useSelector } from 'react-redux';

import FavoriteItem from '../components/Favorites/FavoriteItem';
import './Products.css';

const Favorites = props => {
  const favoriteProducts = useSelector(state =>
    state.shop.products.filter(p => p.isFavorite)
  );
  let content = <p className="placeholder">Got no favorites yet!</p>;
  if (favoriteProducts.length > 0) {
    content = (
      <ul className="products-list">
        {favoriteProducts.map(prod => (
          <FavoriteItem
            key={prod.id}
            id={prod.id}
            title={prod.title}
            description={prod.description}
          />
        ))}
      </ul>
    );
  }
  return content;
};

export default Favorites;
```

...the state can be maintained using a context:

*context/products-context.js*

```js
import React, { useState } from 'react';

export const ProductsContext = React.createContext({
  products: [],
  toggleFav: (id) => {},
});

export default (props) => {
  const [productsList, setProductsList] = useState([
    {
      id: 'p1',
      title: 'Red Scarf',
      description: 'A pretty red scarf.',
      isFavorite: false,
    },
    {
      id: 'p2',
      title: 'Blue T-Shirt',
      description: 'A pretty blue t-shirt.',
      isFavorite: false,
    },
    {
      id: 'p3',
      title: 'Green Trousers',
      description: 'A pair of lightly green trousers.',
      isFavorite: false,
    },
    {
      id: 'p4',
      title: 'Orange Hat',
      description: 'Street style! An orange hat.',
      isFavorite: false,
    },
  ]);

  const toggleFavorite = (productId) => {
    setProductsList((currentProductList) => {
      const prodIndex = currentProductList.findIndex((p) => p.id === productId);
      const newFavStatus = !currentProductList[prodIndex].isFavorite;
      const updatedProducts = [...currentProductList];
      updatedProducts[prodIndex] = {
        ...currentProductList[prodIndex],
        isFavorite: newFavStatus,
      };
      return updatedProducts;
    });
  };

  return (
    <ProductsContext.Provider
      value={{ products: productsList, toggleFav: toggleFavorite }}
    >
      {props.children}
    </ProductsContext.Provider>
  );
};
```

*index.js*

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

import './index.css';
import App from './App';
import ProductsProvider from './context/products-context';

ReactDOM.render(
  <ProductsProvider>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </ProductsProvider>,
  document.getElementById('root')
);
```

*containers/Products.js*

```js
import React, { useContext } from 'react';

import ProductItem from '../components/Products/ProductItem';
import { ProductsContext } from '../context/products-context';
import './Products.css';

const Products = (props) => {
  const productList = useContext(ProductsContext).products;
  return (
    <ul className="products-list">
      {productList.map((prod) => (
        <ProductItem
          key={prod.id}
          id={prod.id}
          title={prod.title}
          description={prod.description}
          isFav={prod.isFavorite}
        />
      ))}
    </ul>
  );
};

export default Products;
```

*components/Products/ProductItem.js*

```js
import React, { useContext } from 'react';

import Card from '../UI/Card';
import './ProductItem.css';
import { ProductsContext } from '../../context/products-context';

const ProductItem = (props) => {
  const toggleFav = useContext(ProductsContext).toggleFav;

  const toggleFavHandler = () => {
    toggleFav(props.id);
  };

  return (
    <Card style={{ marginBottom: '1rem' }}>
      <div className="product-item">
        <h2 className={props.isFav ? 'is-fav' : ''}>{props.title}</h2>
        <p>{props.description}</p>
        <button
          className={!props.isFav ? 'button-outline' : ''}
          onClick={toggleFavHandler}
        >
          {props.isFav ? 'Un-Favorite' : 'Favorite'}
        </button>
      </div>
    </Card>
  );
};

export default ProductItem;
```

*containers/Favorites.js*

```js
import React, { useContext } from 'react';

import FavoriteItem from '../components/Favorites/FavoriteItem';
import { ProductsContext } from '../context/products-context';
import './Products.css';

const Favorites = (props) => {
  const favoriteProducts = useContext(ProductsContext).products.filter(
    (p) => p.isFavorite
  );
  let content = <p className="placeholder">Got no favorites yet!</p>;
  if (favoriteProducts.length > 0) {
    content = (
      <ul className="products-list">
        {favoriteProducts.map((prod) => (
          <FavoriteItem
            key={prod.id}
            id={prod.id}
            title={prod.title}
            description={prod.description}
          />
        ))}
      </ul>
    );
  }
  return content;
};

export default Favorites;
```

**Approach 2: Using a Custom Hook**

Here, a custom hook is created that manages a generic state object.  

The state object (`globalState`) is a global variable, which means that it will only be created the first time this hook is imported into a component.  For all subsequent imports, the existing `globalState` will be used.

Within the hook, a local instance of the `setState` function is stored through use of a closure.  This will be specific to the component into which the hook is imported (since it will be re-created everytime the hook is imported).

The `listeners` array is essentially a list of `setState` instances; one for each component into which the hook is imported.

*hooks-store/store.js*
 
```js
import { useState, useEffect } from 'react';

// data is managed outside of hook
let globalState = {};
// all components that are interested in state
let listeners = [];
// actions that can update the state
let actions = {};

// in some instances, a component may only want to update the store, without
// then reacting to the change in state, so a shouldListen props is passed in
// to indicate this (to avoid unnecessary re-renders)
export const useStore = (shouldListen = true) => {
  // use global state
  // this will not be recreated when this file is imported anywhere
  // only interested in update function (since current state is global)
  const setState = useState(globalState)[1];

  // pass an identifier for the action, and any payload the
  // action requires
  const dispatch = (actionIdentifier, payload) => {
    // this is essentially the same concept as a reducer, where
    // an action results in a new state being returned
    const newState = actions[actionIdentifier](globalState, payload);

    // merge updated state with current state
    globalState = { ...globalState, ...newState };

    // update all listeners with updated state
    for (const listener of listeners) {
      // listener = setState
      listener(globalState);
    }
  };

  useEffect(() => {
    if (shouldListen) {
      // this is closure, so value of setState will be captured here
      listeners.push(setState);
    }

    // clean-up function
    // remove captured setState (keep all that are not this setState)
    return () => {
      if (shouldListen) {
        listeners = listeners.filter((li) => li !== setState);
      }
    };
  }, [setState, shouldListen]); // setState and shouldListen should never change, so this will only run when component is first mounted

  // this is the same pattern as useReducer
  return [globalState, dispatch];
};

// need a function to initialise the store with all of the actions, and an initial state
export const initStore = (userActions, initialState) => {
  if (initialState) {
    globalState = { ...globalState, ...initialState };
  }

  actions = { ...actions, ...userActions };
};
```

Once we have the generic store, this can be used to manage specific state:

*hooks-store/products-store.js*

```js
import { initStore } from './store';

const configureStore = () => {
  const actions = {
    TOGGLE_FAV: (curState, productId) => {
      const prodIndex = curState.products.findIndex((p) => p.id === productId);
      const newFavStatus = !curState.products[prodIndex].isFavorite;
      const updatedProducts = [...curState.products];
      updatedProducts[prodIndex] = {
        ...curState.products[prodIndex],
        isFavorite: newFavStatus,
      };

      return { products: updatedProducts };
    },
  };

  initStore(actions, {
    products: [
      {
        id: 'p1',
        title: 'Red Scarf',
        description: 'A pretty red scarf.',
        isFavorite: false,
      },
      {
        id: 'p2',
        title: 'Blue T-Shirt',
        description: 'A pretty blue t-shirt.',
        isFavorite: false,
      },
      {
        id: 'p3',
        title: 'Green Trousers',
        description: 'A pair of lightly green trousers.',
        isFavorite: false,
      },
      {
        id: 'p4',
        title: 'Orange Hat',
        description: 'Street style! An orange hat.',
        isFavorite: false,
      },
    ],
  });
};

export default configureStore;
```

Then, to use the specific store:

*index.js*

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

import './index.css';
import App from './App';
import configureProductStore from './hooks-store/products-store';

configureProductStore();

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```

*containers/Products.js*

```js
import React from 'react';

import ProductItem from '../components/Products/ProductItem';
import { useStore } from '../hooks-store/store';
import './Products.css';

const Products = (props) => {
  // useStore returns [state, dispatch] but in this case we only care about state
  const state = useStore()[0];

  return (
    <ul className="products-list">
      {state.products.map((prod) => (
        <ProductItem
          key={prod.id}
          id={prod.id}
          title={prod.title}
          description={prod.description}
          isFav={prod.isFavorite}
        />
      ))}
    </ul>
  );
};

export default Products;
```

*components/ProductItem.js*

```js
import React from 'react';

import Card from '../UI/Card';
import './ProductItem.css';
import { useStore } from '../../hooks-store/store';

// use React.memo to ensure the component does not get re-rendered
// unless the props change
const ProductItem = React.memo((props) => {
  console.log('RENDERING');
  // useStore returns [state, dispatch] but in this case we only care about dispatch function
  const dispatch = useStore(false)[1];

  const toggleFavHandler = () => {
    dispatch('TOGGLE_FAV', props.id);
  };

  return (
    <Card style={{ marginBottom: '1rem' }}>
      <div className="product-item">
        <h2 className={props.isFav ? 'is-fav' : ''}>{props.title}</h2>
        <p>{props.description}</p>
        <button
          className={!props.isFav ? 'button-outline' : ''}
          onClick={toggleFavHandler}
        >
          {props.isFav ? 'Un-Favorite' : 'Favorite'}
        </button>
      </div>
    </Card>
  );
});

export default ProductItem;
```

*containers/Favorites.js*

```js
import React from 'react';

import FavoriteItem from '../components/Favorites/FavoriteItem';
import { useStore } from '../hooks-store/store';
import './Products.css';

const Favorites = (props) => {
  // useStore returns [state, dispatch] but in this case we only care about state
  const state = useStore()[0];

  const favoriteProducts = state.products.filter((p) => p.isFavorite);

  let content = <p className="placeholder">Got no favorites yet!</p>;
  if (favoriteProducts.length > 0) {
    content = (
      <ul className="products-list">
        {favoriteProducts.map((prod) => (
          <FavoriteItem
            key={prod.id}
            id={prod.id}
            title={prod.title}
            description={prod.description}
          />
        ))}
      </ul>
    );
  }
  return content;
};

export default Favorites;
```

**Further Information**

* [https://www.npmjs.com/package/use-global-hook](use-global-hook) - an NPM package that behaves in a similar manner to the custom store hook described above.

</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="code-examples">
<button type="button" class="collapsible">+ Code Examples</button>   
<div class="content" style="display: none;" markdown="1">

<div id="spinner">
<button type="button" class="collapsible">+ Creating A Simple Spinner</button>   
<div class="content" style="display: none;" markdown="1">

*Spinner.js*

```jsx
import React from 'react';
import classes from './Spinner.module.css';

const Spinner = (props) => <div className={classes.Loader}>Loading...</div>;

export default Spinner;
```

*Spinner.module.css*

Generate the CSS using the following tool:
* [https://projects.lukehaas.me/css-loaders/](https://projects.lukehaas.me/css-loaders/)

*MyPage.js*

```jsx
import React, { Component } from 'react';
import axios from 'axios';

import Input from './Input';
import Button from './Button';
import Spinner from './Spinner';

class MyPage extends Component {
  state = {
    loading: false,
  };

  submitHandler = (event) => {
  
    this.setState({ loading: true });
    
    axios
      .post('https://mydatabase/my-data.json', data)
      .then((response) => {
        this.setState({ loading: false });
        this.props.history.push('/');
      })
      .catch((error) => {
        this.setState({ loading: false });
      });
  };
  
  render() {
    let content = (
      <form onSubmit={this.submitHandler}>
        <Input />
        <Button>
          SUBMIT
        </Button>
      </form>
    );
    
    if (this.state.loading) {
      content = <Spinner />;
    }

    return (
      <div>
        <h4>Enter your Data</h4>
        {content}
      </div>
    );
  }
}

export default MyPage;
```

</div>
</div>

<div id="hamburger">
<button type="button" class="collapsible">+ Creating A Simple Hamburger Icon</button>   
<div class="content" style="display: none;" markdown="1">

A "Hamburger Button" is the nickname given to the icon that is commonly used for toggling a menu, particularly on mobile apps.  The name comes from the resemblance with a hamburger.

*HamburgerButton.js*

```jsx
import React from 'react';
import classes from './HamburgerButton.module.css';

const HamburgerButton = (props) => (
  <div className={classes.HamburgerButton} onClick={props.clicked}>
    <div></div>
    <div></div>
    <div></div>
  </div>
);

export default HamburgerButton;
```

*HamburgerButton.module.css*

```css
.HamburgerButton {
  width: 40px;
  height: 100%;
  display: flex;
  flex-flow: column;
  justify-content: space-around;
  align-items: center;
  padding: 10px 0;
  box-sizing: border-box;
  cursor: pointer;
}

.HamburgerButton div {
  width: 90%;
  height: 3px;
  background-color: white;
}

@media (min-width: 500px) {
  .HamburgerButton {
      display: none;
  }
}
```
</div>
</div>

<div id="backdrop">
<button type="button" class="collapsible">+ Creating A Simple Backdrop</button>   
<div class="content" style="display: none;" markdown="1">

In this context, a backdrop refers to an overlay that is displayed to hide the background while something else is displayed in the foreground (e.g. a message dialog, or a slide-in dialog). 

*Backdrop.js*

```jsx
import React from 'react';
import classes from './Backdrop.module.css';

const Backdrop = (props) =>
  props.show ? <div className={classes.Backdrop} onClick={props.clicked}></div> : null;

export default Backdrop;

```

*Backdrop.module.css*

```css
.Backdrop {
  width: 100%;
  height: 100%;
  position: fixed;
  z-index: 100;
  left: 0;
  top: 0;
  background-color: rgba(0, 0, 0, 0.5);
}

/* If width < 350px or height < 300px  */
@media (max-width: 500px), (max-height: 500px) {
  .Backdrop {
    width: 500px;
    height: 715px;
  }
}
```
</div>
</div>

<div id="modal">
<button type="button" class="collapsible">+ Creating A Simple Modal Pop-Up</button>   
<div class="content" style="display: none;" markdown="1">

*Modal.js*

```jsx
import React, { Component } from 'react';
import classes from './Modal.module.css';
import Wrapper from './Wrapper';
import Backdrop from './Backdrop';

class Modal extends Component {

  shouldComponentUpdate(nextProps, nextState) {
    return nextProps.show !== this.props.show || nextProps.children !== this.props.children;
  }

  render() {
    return (
      <Wrapper>
        <Backdrop show={this.props.show} clicked={this.props.modalClosed} />
        <div
          className={classes.Modal}
          style={ {
            transform: this.props.show ? 'translateY(0)' : 'translateY(-100vh)',
            opacity: this.props.show ? '1' : '0',
          } }
        >
          {this.props.children}
        </div>
      </Wrapper>
    );
  }
}

export default Modal;
```

*Backdrop.module.css*

```css
.Backdrop {
  width: 100%;
  height: 100%;
  position: fixed;
  z-index: 100;
  left: 0;
  top: 0;
  background-color: rgba(0, 0, 0, 0.5);
}

/* If width < 350px or height < 300px  */
@media (max-width: 500px), (max-height: 500px) {
  .Backdrop {
    width: 500px;
    height: 715px;
  }
}
```

*MyPage.js*

```jsx
class MyPage extends Component {
  state = {
    data: {},
    showData: false
  };
  
  modelOpenedHandler = (data) => {
    this.setState({ data: data, showData: true });
  };
  
  modalClosedHandler = () => {
    this.setState({ showData: false });
  };
  
  render() {
    let myData = (
        <MyData data={this.state.data} />
      );
    }

    if (this.state.loading) {
      myData = <Spinner />;
    }

    return (
      <Wrapper>
        <Modal show={this.state.showData} modalClosed={this.modalClosedHandler}>
          {myData}
        </Modal>
        <Content modelOpened={this.modalOpenedHandler} />
      </Wrapper>
    );
  }
}
```

</div>
</div>

<div id="sidedrawer">
<button type="button" class="collapsible">+ Creating A Simple Toolbar And Side Drawer</button>   
<div class="content" style="display: none;" markdown="1">

*Layout.js*

```jsx
import React, { Component } from 'react';

import classes from './Layout.module.css';

import Wrapper from './Wrapper';
import Toolbar from './Toolbar';
import SideDrawer from './SideDrawer';

class Layout extends Component {
  state = {
    showSideDrawer: false,
  };

  sideDrawerToggleHandler = () => {
    this.setState((prevState) => {
      return { showSideDrawer: !prevState.showSideDrawer };
    });
  };

  render() {
    return (
      <Wrapper>
        <Toolbar toggle={this.sideDrawerToggleHandler} />

        <SideDrawer open={this.state.showSideDrawer} closed={this.sideDrawerToggleHandler} />

        <main className={classes.Content}>{this.props.children}</main>
      </Wrapper>
    );
  }
}

export default Layout;
```

*Layout.module.css*

```css
.Content {
  margin-top: 72px;
  width: 100%;
}

/* If width < 350px or height < 300px  */
@media (max-width: 350px), (max-height: 300px) {
  .Content {
    width: 350px;
    height: 600px;
    background-color: red;
  }
}
```

*Toolbar.js*

```jsx
import React from 'react';

import classes from './Toolbar.module.css';

import Logo from './Logo';
import NavigationItems from '../NavigationItems';
import HamburgerButton from './HamburgerButton'

const Toolbar = (props) => (
  <header className={classes.Toolbar}>
    <div className={[classes.HamburgerButton, classes.MobileOnly].join(' ')}>
      <HamburgerButton clicked={props.toggle} />
    </div>
    <div className={classes.Logo}>
      <Logo />
    </div>
    <nav className={classes.DesktopOnly}>
      <NavigationItems/>
    </nav>
  </header>
);

export default Toolbar;
```

*Toolbar.module.css*

```css
.Toolbar {
  height: 56px;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: #703b09;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  box-sizing: border-box;
  z-index: 90;
}

.Toolbar nav {
  height: 100%;
}

.Logo {
  height: 80%;
}

.HamburgerButton {
  height: 100%;
}

/* If width > 500px */
@media (max-width: 500px) {
  .DesktopOnly {
    display: none;
  }
}

/* If width < 499px */
@media (min-width: 499px) {
  .MobileOnly {
    display: none;
  }
}
```

*SideDrawer.js*

```jsx
import React from 'react';

import classes from './SideDrawer.module.css';

import Wrapper from './Wrapper';
import Backdrop from '../Backdrop';
import Logo from './Logo';
import NavigationItems from './NavigationItems';

const SideDrawer = (props) => {
  let attachedClasses = [classes.SideDrawer, classes.Close];
  if (props.open) {
    attachedClasses = [classes.SideDrawer, classes.Open];
  }

  return (
    <Wrapper>
      <Backdrop show={props.open} clicked={props.closed} />
      <div className={attachedClasses.join(' ')}>
        <div className={classes.Logo}>
          <Logo />
        </div>
        <nav>
          <NavigationItems />
        </nav>
      </div>
    </Wrapper>
  );
};

export default SideDrawer;
```

*SideDrawer.module.css*

```css
.SideDrawer {
  position: fixed;
  width: 280px;
  max-width: 70%;
  height: 100%;
  left: 0;
  top: 0;
  z-index: 200;
  background-color: white;
  padding: 32px 16px;
  box-sizing: border-box;
  transition: transform 0.3s ease-out;
}

@media (min-width: 500px) {
  .SideDrawer {
    display: none;
  }
}

.Open {
  transform: translateX(0);
}

.Close {
  transform: translateX(-100%);
}

.Logo {
  position: relative;
  height: 11%;
  width: 45%;
  max-width: 100%;
  margin-bottom: 32px;
}
```

</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="further-reading">
<button type="button" class="collapsible">+ Further Reading/Exploration</button>   
<div class="content" style="display: none;" markdown="1">

<div id="demo-apps">
<button type="button" class="collapsible">+ Demo Projects</button>   
<div class="content" style="display: none;" markdown="1">

Lots of React examples apps, typically with source code:

* [https://react.rocks/](https://react.rocks/)
* [https://madewithreact.com/](https://react.rocks/)

</div>
</div>

<div id="gatsbyjs">
<button type="button" class="collapsible">+ Gatsby.js (static websites from React)</button>   
<div class="content" style="display: none;" markdown="1">

Gatsby.js is a library built on top of React that allows you to build static websites with React.  It automatically generates the HTML+CSS+JS for a website based on the given React code.

* [https://www.gatsbyjs.com/](https://www.gatsbyjs.com/)

</div>
</div>

<div id="react-native">
<button type="button" class="collapsible">+ React Native (mobile apps from React)</button>   
<div class="content" style="display: none;" markdown="1">

React Native is React for mobile apps.  Apps are written using a combination of React & React Native, and then compile for either iOS or Android.

* [https://reactnative.dev/](https://reactnative.dev/)

</div>
</div>

<div id="react-material-ui">
<button type="button" class="collapsible">+ Material-UI (UI components)</button>   
<div class="content" style="display: none;" markdown="1">

Material-UI is a component library that can be imported into a React project and provides beautifully designed UI components.

* [https://material-ui.com/](https://material-ui.com/)

</div>
</div>

<div id="react-bootstrap">
<button type="button" class="collapsible">+ React-Bootstrap (UI components)</button>   
<div class="content" style="display: none;" markdown="1">

React-Bootstrap is another component library that provides UI components.

* [https://react-bootstrap.github.io/](https://react-bootstrap.github.io/)

</div>
</div>

<div id="react-preact">
<button type="button" class="collapsible">+ Preact (lightweight alternative to React)</button>   
<div class="content" style="display: none;" markdown="1">

Preact is a lightweight alternative to React, with a leaner algorithm for DOM diffing.  Generally speaking, Preact is better if initial page load performance is more important than general performance.  For more intensive and/or complex applications, React is generally better.

* [https://preactjs.com/](https://preactjs.com/)

</div>
</div>

</div>
</div>

&nbsp;

-------------------------------------------------------------------------------------------------------

<div id="future">
<button type="button" class="collapsible">+ Future Updates</button>   
<div class="content" style="display: none;" markdown="1">

* [Default Props](https://reactjs.org/docs/react-component.html#defaultprops)
* [Default State](https://reactjs.org/docs/react-without-es6.html#setting-the-initial-state)
* [React Top Level API](https://reactjs.org/docs/react-api.html)
* [dangerouslySetInnerHTML](https://reactjs.org/docs/dom-elements.html#dangerouslysetinnerhtml)
* [componentDidCatch](https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html)
* [Portals](https://reactjs.org/docs/portals.html)
* [Hydration](https://reactjs.org/docs/react-dom.html#hydrate)
* [Strict Mode](https://reactjs.org/docs/strict-mode.html)

</div>
</div>

&nbsp;

&nbsp;

&nbsp;

-------------------------------------------------------------------------------------------------------

**Move along; nothing to see here...**

<script type="text/javascript">

    const loadCSS = (filename) => { 

       const file = document.createElement("link");
       file.setAttribute("rel", "stylesheet");
       file.setAttribute("type", "text/css");
       file.setAttribute("href", filename);
       document.head.appendChild(file);
    };

    const loadJS = (filename) => { 

       const file = document.createElement("script");
       file.setAttribute("type", "text/javascript");
       file.setAttribute("src", filename);
       document.head.appendChild(file);
    };
   
    //just call a function to load your CSS
    //this path should be relative your HTML location
    loadCSS("../collapse.css");
    loadJS("../collapse.js");

</script>

<!-- Default Statcounter code for reactjs-cheat-sheet
https://oclipa.github.io/reactjs-cheat-sheet/ -->
<script type="text/javascript">
var sc_project=12343799; 
var sc_invisible=1; 
var sc_security="1747bed3"; 
</script>
<script type="text/javascript"
src="https://www.statcounter.com/counter/counter.js"
async></script>
<noscript><div class="statcounter"><a title="Web Analytics
Made Easy - StatCounter" href="https://statcounter.com/"
target="_blank"><img class="statcounter"
src="https://c.statcounter.com/12343799/0/1747bed3/1/"
alt="Web Analytics Made Easy -
StatCounter"></a></div></noscript>
<!-- End of Statcounter Code -->
