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
│   │   └── styles.js
```

Where index.js will be:

```js
// Libs
import React from 'react';

// Globals
import BackIcon from 'assets/icons/back-icon.svg';

// Locals
import * as Styles from './styles';

const BackButton = ({ onPress }) => (
  <Styles.BackButton onPress={onPress}>
    <BackIcon />
  </Styles.BackButton>
);

export default BackButton;
```

So than you will easily import it like this:

```js
import BackButton from 'components/BackButton';
```