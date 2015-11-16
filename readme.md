# [React.JS](https://github.com/reactjs)
## History

  Created by [Jordan Walke](https://github.com/jordwalke), a software engineer at Facebook.

  Influenced by [XHP](https://en.wikipedia.org/wiki/XHP), an HTML components framework for PHP.

## What is it?

  An open-source JavaScript library for creating user interfaces.

  Designed to help developers build large apps where data changes over time. It strives to be simple, [declarative](https://en.wikipedia.org/wiki/Declarative_programming) and [composable](https://en.wikipedia.org/wiki/Composability).

## Key Points

### One-way Data Flow
React embraces one-way data flow where components are automatically re-rendered when the 'props' on a React component are changed.

This removes some of the complexity of two-way data binding.

Reduces boilerplate and can be easier to understand than traditional data binding.

### SPA
Aims to address challenges encountered in developing single-page applications.

### Virtual DOM
React maintains a virtual DOM of its own.

This allows the library to determine which parts of the DOM have changed by 'diffing' the new version with the stored virtual DOM.

It then uses the result to determine how to update the browser's DOM.

This abstraction creates a simpler programming model and better performance.

### Server-Side
Can render on the server using Node, and it can power native apps using [React Native](https://facebook.github.io/react-native/).
