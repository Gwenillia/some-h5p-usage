# React.JS - H5P usage
This document serves as a guide for using and implementing React.JS within our codebase.

## Table of Contents
- [Prerequisites](#prerequisites)
	- [Some useful Ressources](#some-useful-ressources)
		- [Main ressources](#main-ressources)
		- [Optional ressources](#optional-ressources)
- [Styling](#styling)
- [File Organization](#file-organization)
- [State Management](#state-management)
- [Functional Components and Hooks](#functional-components-and-hooks)
- [Splitting Components](#splitting-components)
- [Testing](#testing)
- [JSX](#jsx)
- [PropTypes - Type Checking](#proptypes---type-checking)
- [Best Practices](#best-practices)
- [Conclusion](#conclusion)

## Prerequisites
Developers with some JavaScript / React knowledge will familiarize very much easier.

### Some useful Ressources
#### Main ressources
- **React.JS documentation:** [Official React.JS Documentation](https://reactjs.org/tutorial/tutorial.html)
- 	- [ ] Complete the starting tic tac toe challenge
- **Thinking in React:** [React Documentation](https://react.dev/learn/thinking-in-react)
- 	- [ ] Step 1 to be understand but check other steps as well
- **ES6 Features:** [ES6 Guide](http://es6-features.org)
- 	- [ ] Get familiar with modern JavaScript Concepts
- **Sass Documentation:** [Official Sass Guide](https://sass-lang.com/guide)
- 	- [ ] Familiarize yourself with mixins
- 	- [ ] Familiarize yourself with variables
- 	- [ ] Familiarize with .module files
- **The Chase:** [The Chase - H5P Content Type](https://github.com/h5p/h5p-chase)
- 	- [ ] Could be checked for some examples

#### Optional ressources
- **JavaScript Documentation:** [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- **Webpack bundler:** [Webpack guide](https://webpack.js.org/guides/getting-started/)
- **`jsconfig.json` Information:** [VSC Documentation about jsconfig](https://code.visualstudio.com/docs/languages/jsconfig)

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

- **`useState`:** [useState Documentation](https://react.dev/reference/react/useState)
- **`useEffect`:** [useEffect Documentation](https://react.dev/reference/react/useEffect)
- **`useContext`:** [useContext Documentation](https://react.dev/reference/react/useContext)
- **`useReducer`:** [useReducer Documentation](https://react.dev/reference/react/useReducer)

## Splitting Components
As your application grows, it might be helpful to start splitting components into smaller, reusable pieces. But how do you decide when to split a component? Here are some guidelines that can help:

- **Single Responsibility Principle:** Each component should ideally do one thing. If it ends up growing, it should be split into smaller subcomponents.

- **Reusability:** If a part of your UI is used in multiple places, it's a good idea to make it a separate component. This allows for code reuse and consistency across your app.

- **Complexity:** If your component has too many lines of code or is becoming hard to understand, consider splitting it into smaller components. A good rule of thumb is if you have to scroll too much in your editor to see the entire component, it may be a sign that your component needs to be broken down.

- **State Logic:** If a portion of your component has its own state or side effects (with hooks like `useState` or `useEffect`), it might be a good idea to split that part into its own component.

Remember, splitting components is an art. And be aware that smaller components are usually easier to maintain and test.

## Testing
Ideally, we should be integrating more testing into our workflow. We use Jest and React Testing Library.

- **Jest:** [Jest Documentation](https://jestjs.io/docs/en/getting-started)
- **React Testing Library:** [React Testing Library Documentation](https://testing-library.com/docs/react-testing-library/intro/)

## JSX
We write our React code in JavaScript and we use the JSX Syntax.
Meaning that JavaScript expressions are embedded inside `{}`. JSX will convert HTML tags into React elements. 

- **JSX:** [JSX Documentation](https://react.dev/learn/writing-markup-with-jsx)

Here are some advantages of using JSX instead of JS:
1. **Readability and Simplicity:** JSX makes our components easier to read and understand. It provides a clear picture of the DOM structure of a component, as it looks like regular HTML.

2. **Easy to Identify:** In our codebase, we use `.jsx` extension for React components. This makes it easy to identify component files as opposed to other JavaScript files such as `index.js` in components folder or utility JavaScript files.

3. **Performance:** JSX compiles into `React.createElement()` calls which is more efficient than creating elements with JavaScript and appending to the DOM.

4. **Components as HTML Elements:** With JSX, we can use our custom components as if they were HTML elements, which makes the composition of our components a lot more intuitive.

> [!warning]
> Remember to import React in every JSX file:
> ```jsx
> import React from 'react';

## PropTypes - Type Checking
To ensure the accuracy of props passed to components, we use PropTypes for type checking in our React codebase. PropTypes exports a range of validators that can be used to make sure the data you receive is valid.

> [!example] Example of Type checking using PropTypes
> ```jsx
> import PropTypes from 'prop-types';
> 
> const Component = ({ name, age }) => {
>   return (
>     <div>
>       <h1>{name}</h1>
>       {age && <p>{age} yo</p>}
>     </div>
>   );
> }
> 
> Component.propTypes = {
>   name: PropTypes.string.isRequired,
>   age: PropTypes.number,
> }
>
> export default Component;

Here, the `Component` expects to receive a `name` and an optional `age`. If `name` prop is not provided or it is of incorrect type, a warning will be shown in the JavaScript console. If `age` is provided but is not a number, a warning will also be shown. This helps us catching and fix problems earlier in development.
	
- **PropTypes Documentation:** [ReactJs PropTypes documentation](https://reactjs.org/docs/typechecking-with-proptypes.html)

## Best Practices
While working with our React.JS codebase, there are certain best practices to follow. Including:

- **One component = one file:**
In React, a component is a reusable piece of code that returns a React element to be rendered to the page. In our codebase, we adhere to the principle of "One Component Per File". This means that each `.jsx` file in our components directory defines exactly one React component. This makes it easy to understand the structure of our application and locate specific components.

- **Choosing `useState` versus `useReducer`:** 
	`useState` is enough for simple state management. For complex state logic such as a state machine, `useReducer` is a better choice.
	
- **Using Context:**
	Context should be used to pass data down to nested components without having to manually pass props at every level.
	
- **Naming Conventions:** 
	- **`PascalCase`:** For the name of our components — both file name and the functional component itself —
	- **`camelCase`:** For the name of our variables.

## Conclusion
This document should give you a better understanding of how we use React.js in our codebase.
