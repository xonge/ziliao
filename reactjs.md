1. npm install -g browserify
2. npm install --save react react-dom babelify babel-preset-react
3.      
    ```javascript
    // main.js
    var React = require('react');
    var ReactDOM = require('react-dom');
   
    ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
    );```
3. browserify -t babelify --presets react main.js -o bundle.js
3. npm install --global babel-cli