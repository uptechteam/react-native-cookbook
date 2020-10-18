# Folder Structure 

[TODO] - describe more about every folder to clarify the purpose.

<br/>

```
.
├── __tests__
├── .vscode
│   ├── launch.json     // Your local config for "React Native Tools" ext.
│   └── settings.json   // Shared VSCode settings (Spell Checker, formatter, etc.).
│
├── android
├── ios
├── node_modules
├── src
│   ├── assets
│   │   ├── fonts
│   │   ├── icons
│   │   └── images
│   │
│   ├── components
│   ├── constants
│   ├── navigation
│   ├── screens
│   ├── models
│   ├── store
│   │   ├── actions
│   │   ├── reducers
│   │   ├── rootReducer.js
│   │   └── store.js
│   │
│   ├── middlewares
│   ├── theme
│   ├── utils
│   └── App.js
│ 
├── .buckconfig
├── .eslintrc.js
├── .prettierrc.js
├── .gitattributes
├── .gitignore
├── .watchmanconfig
├── app.json
├── babel.config.js
├── tsconfig.json       // or jsconfig.json
├── index.js
├── package.json
└── yarn.lock
```

<br/>
<br/>

# File Naming

We are using `camelCase` for common folder names ('screens', 'components', 'assets', etc.)

For React folders (like components, screens) and theirs files we are using `PascalCase`.


Example:

```
├── components
│   ├── BackButton
│   │   ├── index.js
│   │   ├── BackButton.js
│   │   └── BackButton-styles.js
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
import * as Styles from './BackButton-styles';

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

* _"BackButton-styles.js"_ - separating this file name with "-" makes it easier to rename **_only_** component name (by double-clicking on unique name part or by using key combinations to quickly slide through words) and feels more clear for visibility.

<br/>

## __Cons__ about this component structure:

* _Extra files in your project._ Having both BackButton.js and index.js means managing and juggling additional files. If you’re copying another component, you may forget to open the index.js to rename the export to the new name.