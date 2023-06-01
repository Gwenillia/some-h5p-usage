# React.JS - H5P usage
This document serves as a guide for using and implementing React.JS within our codebase.

## Table of Contents
- [Prerequisites](#prerequisites)
	- [Some useful Documentations](#some-useful-documentations)
- [Styling](#styling)
- [File Organization](#file-organization)
- [State Management](#state-management)
- [Functional Components and Hooks](#functional-components-and-hooks)
- [Testing](#testing)
- [JSX](#jsx)
- [Best Practices](#best-practices)
- [Conclusion](#conclusion)

## Prerequisites
Developers with some JavaScript / React knowledge will familiarize very much easier.

### Some useful Documentations
- **The Chase:** [The Chase - H5P Content Type](https://github.com/h5p/h5p-chase)
- **JavaScript Documentation:** [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- **React.JS documentation:** [Official React.JS Documentation](https://reactjs.org/tutorial/tutorial.html)
- **ES6 Features:** [ES6 Guide](http://es6-features.org)
- **Sass Documentation:** [Official Sass Guide](https://sass-lang.com/guide)
- **Webpack bundler:** [Webpack guide](https://webpack.js.org/guides/getting-started/)

## Styling
We use Sass modules for styling our components. Each component should have its own Sass file located in the `styles` directory, mirroring the structure of the `components` directory.

## File Organization
Our file tree should look closely to:
```
src
|- assets
|- components
|- context
|- helpers
|- hooks
|- styles
|- utils
```

The folders and files inside `components` and `styles` follow the same structure.

Each component directory should have an `index.js` file to export the component. This approach simplifies imports elsewhere in the application. No need to write the full path of a component to import it.

> [!example] `index.js` structure
> ```jsx
> // One component to export from the folder
> import Component from './Component';
> export default Component
> // Multiple components to export from the folder
> import ComponentA from './ComponentA';
> import ComponentB from './ComponentB';
> export { ComponentA, ComponentB };

> [!example] import in a component
> ```jsx
> // Without index.js
> import Component from './components/Component/ComponentFile';
> // With index.js
> import Component from './components/Component';
> // add {} if it is exported from an index.js exporting multiple component
> import { Component } from './components/Common';

JavaScript will automatically look for an `index.js` file when you specify the path to a directory. This leads to cleaner and more readable code.

Additionnally, we use `@` alias to simplify imports, which is setup through `jsconfig.json` and `webpack.config.js` at the root of the project. This alias represents the `src` directory.

>[!example] import using @ alias
>```jsx
>import { Component } from '@/components/Common'

This prevents to end up with multiple `../../` when you're importing inside a nested component from a totally different folder such as grand parents or uncles.

- **`jsconfig.json` Information:** [VSC Documentation about jsconfig](https://code.visualstudio.com/docs/languages/jsconfig)
- **`webpack.config.js` Information:** [Webpack documentation](https://webpack.js.org/configuration/resolve/)

## State Management
We use Context API and `useReducer` hook for managing state. 

- **Context:**
	allows use to pass data down to nested components without having to manually pass props at every level. This allows us to avoid "prop drilling" and makes our code cleaner and more maintainable
	
- **`useReducer:`**
	For more complex state logic — such as the state machine in [The Chase](https://github.com/h5p/h5p-chase) — we use the `useReducer` hook. This hook lets us manage state transitions in a more predictable way, through the use of actions and a reducer function.
	

## Functional Components and Hooks
We primarily use functional components in conjunction with hooks.

- `useState`: [useState Documentation](https://react.dev/reference/react/useState)
- `useEffect`: [useEffect Documentation](https://react.dev/reference/react/useEffect)
- `useContext`: [useContext Documentation](https://react.dev/reference/react/useContext)
- `useReducer`: [useReducer Documentation](https://react.dev/reference/react/useReducer)

## Testing
Ideally, we should be integrating more testing into our workflow. We use Jest and React Testing Library.

- Jest: [Jest Documentation](https://jestjs.io/docs/en/getting-started)
- React Testing Library: [React Testing Library Documentation](https://testing-library.com/docs/react-testing-library/intro/)

## JSX
We write our React code in JavaScript and we use the JSX Syntax.
Meaning that JavaScript expressions are embedded inside `{}`. JSX will convert HTML tags into React elements. 

- JSX: [JSX Documentation](https://react.dev/learn/writing-markup-with-jsx)

> [!warning]
> Remember to import React in every JSX file:
> ```jsx
> import React from 'react';

## Best Practices
While working with our React.JS codebase, there are certain best practices to follow. Including:

- **Choosing `useState` versus `useReducer`:** 
	`useState` is enough for simple state management. For complex state logic such as a state machine, `useReducer` is a better choice.
	
- **Using Context:**
	Context should be used to pass data down to nested components without having to manually pass props at every level.
	
- **Naming Conventions:** 
	- **`PascalCase`:** For the name of our components — both file name and the functional component itself —
	- **`camelCase`:** For the name of our variables.

## Conclusion
This document should give you a better understanding of how we use React.ks in our codebase.
