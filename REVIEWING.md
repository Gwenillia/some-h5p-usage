# Code Review Guidelines for React Github Repo

The following guide will assist you in performing effective code reviews on our h5p-editor-layout-builder Github repository. This is a crucial process in maintaining the high quality and reliability of our codebase. 

Always remember the following rules while reviewing:

## Matching Scope

The files in the review should match the scope of the related Jira issue. 

## Code Formatting

- There should be no more than 1 blank line separating code.
- Spaces should be provided after opening brackets `{ text` and before closing brackets `text }`. (only if there is text, otherwise no space `{{ text }}` )
- Trailing commas are preferable. [Trailing commas - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Trailing_commas) 
- Only one component per file

## Import Order

The correct import order should be followed:

```js
import '@/styles/components/Component/File.scss';

import React, { useState, whatever } from 'react';
import PropTypes from 'prop-types';

import ComponentX from './ComponentX';
import { ComponentY } from '@/components/XX';

import { helperFunction } from '@/helpers/helperFile';
```

## File Naming and Types
- Files containing JSX should end with the `.jsx` extension.
- Files not containing JSX should not have a `.jsx` extension.

## Folder Structure
- We dot no use a `utils` folder; we've chose to only use `helpers` in this repo.
- Components should have a capitalized name for both the file and component itself (i.e., `Component.jsx`)

## React Specifics
- Only use hooks / function components

### Imports
- Unused imports should be removed
- Use the `@` alias before imports (we don't want `../../../`) - note: Alias can be used with `~` for sass modules

## Props
- Verify that props are correctly passed and received.
- Check the PropTypes. Always need PropTypes if there are props.
- Verify if PropTypes are required or not, correlating with the props themselves.

## Code Duplication
- There should be no code duplication. If there is a duplicate, it might be sorted out either a common component or helper function, or whatever is suitable depending on the situation.

## TODOs
- Check potential TODO related to the issue in the code by searching  or `TODO` in all files (should be removed and treated because the issue is normally solved).

## Code Suggestions
- If a part of the code seems not optimised or good, or if you have a better suggestion, mention it.

## Code Verification
- Run the code and verify it executes without issues.
- Check console for errors.

## UI Verification
- Verify that the CSS matches the mockup.
- Ensure that the behavior is as expected according to the issue.

## Potential Bugs / Regression
- Quickly check for potential bugs or regression.
