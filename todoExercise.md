# Make A Todo List

 Simply clone the react-boilerplate code from [GitHub](https://github.com/StephenGrider/ReactStarter) and navigate into the directory.

# Project Structure
```sh
├── README.md
├── gulpfile.js
├── index.html
├── package.json
├── sass
│   └── style.scss
└── src
    └── app.jsx
```

# Steps
```sh
npm install
```
```sh
gulp
```

# Exploring app.jsx
  Dependencies
  ```js
  var React = require('react');
```
Create a new React Class
```js
var Hello = React.createClass({
  render: function() {
    return <h1 className="red">
      Hello!
    </h1>
  }
});
```
Instantiate Element
```js
var element = React.createElement(Hello, {});
```
Render element to DOM
```js
React.render(element, document.querySelector('.container'));
```

# Creating Components
## ToDo app
```js
/* ToDo App] */
 var TodoApp = React.createClass({ ... });
```
