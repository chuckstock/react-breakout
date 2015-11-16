## Background
In this tutorial, we are going to refactor the bootstrap thumbnail component into React components.

## Wire Frame
Here is a basic picture of what we want our end result to be.  We are going to make two thumbnails that show they type of tutorial, an image, and a button with a number of tutorials for that related subject.  From the picture, can you guess how many React components there are? [wireframe](./overview.png)

## Setup
First, you may want to install a React package for your text-editor before we get started.  This will help with syntax highlighting when we start writing JSX files.


Folder structure:

```sh
├── gulpfile.js
├── index.html
├── main.js
├── package.json
└── src
    ├── app.jsx
    ├── badge.jsx
    ├── thumbnail-list.jsx
    └── thumbnail.jsx
```

### Package.json

```json
{
  "name": "thumbnail-gulp",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "browserify": "^12.0.1",
    "gulp": "^3.9.0",
    "gulp-concat": "^2.6.0",
    "gulp-react": "^3.1.0",
    "gulp-util": "^3.0.7",
    "react": "^0.13.3",
    "reactify": "^1.1.1",
    "vinyl-source-stream": "^1.1.0",
    "watchify": "^3.6.0"
  }
}
```
After you have added this code to your package.json, run:

```sh
$ npm i
```

### Gulp
React components are written in JSX.  JSX gives you the ability to write html within javascript files.  This is the life-blood of building React components, however, the JSX files need to be compiled into javascript, therefore, the easiest way to do this is with a gulp build process.  This gulp file will not only compile from JSX to javascript, but will order the files properly and send all the code to a single file, main.js.

```javascript
var gulp = require('gulp');
var gutil = require('gulp-util');
var source = require('vinyl-source-stream');
var browserify = require('browserify');
var watchify = require('watchify');
var reactify = require('reactify');

gulp.task('default', function() {
  var bundler = watchify(browserify({
    entries: ['./src/app.jsx'],
    transform: [reactify],
    extensions: ['.jsx'],
    debug: true,
    cache: {},
    packageCache: {},
    fullPaths: true
  }));

  function build(file) {
    if (file) gutil.log('Recompiling ' + file);
    return bundler
      .bundle()
      .on('error', gutil.log.bind(gutil, 'Browserify Error'))
      .pipe(source('main.js'))
      .pipe(gulp.dest('./'));
  }
  build();
  bundler.on('update', build);
});

```

Run gulp from the console to start your compiler.  Leave the gulp file running and it will automatically update with your main.js whenever you make changes.


### Index

```html
<head>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.3/react.js"></script>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" integrity="sha512-dTfge/zgoMYpP7QbHy4gWMEGsbsdZeCXz7irItjcC3sPUFtf0kuFbDz/ixG7ArTxmDjLXDmezHubeNikyKGVyQ==" crossorigin="anonymous">
</head>
<body>
  <div class="container">
    <div class="row">
      <div class="target">
      </div>
    </div>
  </div>
</body>

<script src="./main.js"></script>
```

### App.jsx
The app jsx is the the platform to launch your JSX files.  For now, we will use it to attach elements to the DOM and as a place to old our sample data.

First we need to require in React and additional components that we want to render. Secondly we will require in thumbnail-list, this is a component we will build later.
```javascript
var React = require('react');
var ThumbnailList = require('./thumbnail-list');
```

Next lets add the sample data that we will use for our thumbnails.
```javascript
var options = {
  thumbnailData: [
    {
      title: "See tutorials",
      number: 32,
      header: 'Learn React',
      description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
      imageUrl: 'http://formatjs.io/img/react.svg'
    },
    {
      title: "See tutorials",
      number: 12,
      header: 'Learn Gulp',
      description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
      imageUrl: 'https://raw.githubusercontent.com/gulpjs/artwork/master/gulp-2x.png'
    }
  ]
};
```

Finally, we will add some react to create our components and append them to the DOM.
```javascript
// React, please render this class
var element = React.createElement(ThumbnailList, options);

// React, after you render this class, please place it in my body tag
React.render(element, document.querySelector('.target'));
```

### Badge

When looking at our thumbnails the first component we are going to want to make is the Badge.  The badge will act as a button on our thumbnail that will have text and show the number of tutorials for that specific subject.  So lets get to it...

First, we will setup, what will be our basic boilerplate for starting every component in React.

```javascript
var React = require('react');

module.exports = React.createClass({
  render: function() {
  }
});
```
You will notice that the entire component will be wrapped in a 'module.exports'.  This will make it much easier to require in this file later, and then simply paste the component where it is needed.  Don't worry if this is confusing, we will go into more detail about this throughout the tutorial.

Next, lets add our code to the render function.
```javascript
var React = require('react');

module.exports = React.createClass({
  render: function() {
    return <button className="btn btn-primary" type="button">
    {this.props.title} <span className="badge">{this.props.number}</span>
    </button>
  }
});
```
Now, we have seen our first example of JSX and passing through information into a component.  Looking at this completed component, three things stand out:

1. className
1. {this.props.title}
1. {this.props.number}
  1. When writing JSX, we call React methods by wrapping them in {}
  1. React components use properties on their JSX elements to pass data through to each component.  Components can then call that data using 'this.props'.  We'll see more of this in our next component.
