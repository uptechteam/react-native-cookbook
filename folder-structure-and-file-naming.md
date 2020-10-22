# Folder Structure 

<br/>

```
.
├── __tests__                   // Contains automated test files.
├── .vscode                     // Contains configs for VSCode
│   ├── launch.json             // (LOCAL) Your local config for "React Native Tools" ext.
│   └── settings.json           // (SHARED) VSCode settings, that we share across team members (Spell Checker, formatter, etc.).
│
├── android                     // Contains Android-specific files.
├── ios                         // Contains iOS-specific files.
├── node_modules                // Contains Node Modules
├── src                         // Contains source files & folders
│   ├── assets                  // Contains assets files. May be different for each project.
│   │   ├── fonts
│   │   ├── icons
│   │   └── images
│   │
│   ├── components              // Contains React Native components, that we use for creating screens
│   ├── constants               // Contains files, from which we can import constants across the app
│   ├── navigation              // Contains Navigation-specific files.
│   ├── screens                 // Contains screens, that have some logic and builds from components
│   ├── models                  // Contains folders & files that describe TS interfaces
│   ├── store                   // Contains Redux-specific files.
│   │   ├── actions             // Redux Actions
│   │   ├── reducers            // Redux Reducers
│   │   ├── middlewares         // Redux Middlewares
│   │   ├── rootReducer.js      // Combines all reducers
│   │   └── store.js            // Entry-point of the Redux Store
│   │
│   ├── theme                   // Contains theme files for styling the App
│   ├── utils                   // Contains helper function
│   └── App.js                  // Entry-point of the App in src folder
│ 
├── .buckconfig
├── .eslintrc.js
├── .prettierrc.js
├── .gitattributes
├── .gitignore
├── .watchmanconfig
├── app.json
├── babel.config.js
├── tsconfig.json               // or jsconfig.json
├── index.js                    // Entry-point of the App
├── package.json                // Metadata relevant to the project
└── yarn.lock
```

<br/>
<br/>

# File Naming

We are using `camelCase` for common folder names ('screens', 'components', 'assets', etc.)

For React folders (like components, screens) we are using `PascalCase`.

We are don’t use `camelCase/PascalCase` for file names because of:

* readable file names. e.g MyHalfFixedDedupedDirResolver vs my-half-fixed-deduped-dir-resolver 👀
* no more weird git conflicts when renaming/deleting/adding files on various OS file systems (case-sensitive/insensitive)


Example:

```
├── components
│   ├── BackButton
│   │   ├── index.js
│   │   ├── back-button.js
│   │   └── back-button-styles.js
```

Where index.js will be:

```js
import BackButton from './back-button';

export default BackButton;
```

And back-button.js will be:

```js
// Libs
import React from 'react';

// Globals
import BackIcon from 'assets/icons/back-icon.svg';

// Locals
import * as Styles from './back-button-styles';

const BackButton = ({ onPress }) => (
  <Styles.BackButton onPress={onPress}>
    <BackIcon />
  </Styles.BackButton>
);

export default BackButton;
```
<br/>

## __Pros__ about this component structure:

* _Don’t have to be redundant in your import statement_. So to use a BackButton component you would include it like this:

  ```js
  import BackButton from 'components/BackButton';
  ```

* _Cleaner editor environment_ – The editor isn’t junked up by a bunch of directory names and doesn’t look like index.js | index.js | index.js | index.js

* _Makes searching easier._

* _Feels more natural_ to do work on the BackButton component in a file called BackButton.js.

<br/>

## __Cons__ about this component structure:

* _Extra files in your project._ Having both BackButton.js and index.js means managing and juggling additional files. If you’re copying another component, you may forget to open the index.js to rename the export to the new name.