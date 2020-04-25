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
   loadCSS("collapse.css");
   
</script>  

<div>
    
<button type="button" class="collapsible">+ Setup Basic Environment</button>
    
<div class="content" style="display: none;" markdown="1">

1. Install NodeJs: [https://nodejs.org](https://nodejs.org)
2. Install create-react-app: `sudo npm install create-react-app -g`
3. Create a new app: `create-react-app [app-name] [--scripts-version version]`
   * This will create a new sub-directory of the current directory called `app-name`.
   * `--scripts-version version` is optional; if not used, the latest version will be used.
4. In the new app directory, start the development server: `npm start"
   * This actually call a bespoke command defined in package.json.

</div>
</div>
<div>  
<button type="button" class="collapsible">+ Example of a Simple App</button>
    
<div class="content" style="display: none;" markdown="1">

### App.js

```jsx
// imports ///////////////////////////////////////////////////////////

import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import Calculator from './Calculator/Calculator.js';

// App class /////////////////////////////////////////////////////////

class App extends Component {
  
  // application state ///////////////////////////////////////////////

  state = {
    algName: 'None',
    val1: 0,
    val2: 0
  };
  
  // event handlers and functions ////////////////////////////////////

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

  // render ///////////////////////////////////////////////////////////

  render() {
    // local style ////////////////////////////////////////////////////
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
                    onChange={(event) => this.val1ChangedHandler(event)} 
                    value={v1} />
            
            <input type="text" 
                    onChange={(event) => this.val2ChangedHandler(event)} 
                    value={v2} />
            
            <div className = "buttons">
              <button style={style} 
                      onClick={(event) => this.doCalculationHandler(event)}
                      value="add">Add</button>
              <button style={style} 
                      onClick={(event) => this.doCalculationHandler(event)}
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

```
import React from 'react';

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

<script type="text/javascript">

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
