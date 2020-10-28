# Folder Structure 

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

# File Naming

We are using `camelCase` for common folder names ('screens', 'components', 'assets', etc.)

For React folders/files `PascalCase`.

> Note: By default, Mac OS is case-insensitive but case-preserving. This means that as far as macOS is concerned Test.js and test.js are the same file. So be attentive to the case when creating folders/files so that they don't run into that problem.


Example:

```
├── components
│   ├── BackButton
│   │   ├── index.js
│   │   ├── BackButton.js
│   │   └── BackButtonStyles.js
```

Where index.js will be:

```js
import BackButton from './BackButton';

export default BackButton;
```

And BackButton.js will be:

```js
// Libs
import React from 'react';

// Globals
import BackIcon from 'assets/icons/back-icon.svg';

// Locals
import * as Styles from './BackButtonStyles';

const BackButton = ({ onPress }) => (
  <Styles.BackButton onPress={onPress}>
    <BackIcon />
  </Styles.BackButton>
);

export default BackButton;
```

> Note: This guide assumes styled-components library is used for styling, but that is not a requirement and should be changed in future once we make a decision on the way we do styling.

## __Pros__ about this component structure:

* _Don’t have to be redundant in your import statement_. So to use a BackButton component you would include it like this:

  ```js
  import BackButton from 'components/backButton';
  ```

* _Cleaner editor environment_ – The editor isn’t junked up by a bunch of directory names and doesn’t look like index.js | index.js | index.js | index.js

* _Makes searching easier._

* _Feels more natural_ to do work on the BackButton component in a file called BackButton.js.

## __Cons__ about this component structure:

* _Extra files in your project._ Having both BackButton.js and index.js means managing and juggling additional files. If you’re copying another component, you may forget to open the index.js to rename the export to the new name.