# Code styles guide

We use `Prettier - Code formatter` extension in tandem with `ESLint` rules for Auto-Styling.
Read more about it in "extensions" chapter.

As we extend rules from "Airbnb" in eslintrc, you can read about their [JavaScript Style Guide](https://github.com/airbnb/javascript) and [React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react) 


## General Code Style points

* Code should be simple and explicit
* Embed “is”/”has”/”should” for boolean variable/props
* Embed “on” in front of handler props name to distinguish it with value props



## Code Style rules by examples

### Sorting the imports

``` js
// Libs
import React, { useState, useEffect } from 'react';
import { FlatList, View, RefreshControl } from 'react-native';
import { useDispatch, useSelector } from 'react-redux';
import { useNavigation } from '@react-navigation/native';

// Globals
import Theme from 'theme/Theme';
import ObjectiveCard from 'components/objectiveCard/ObjectiveCard';
import NoObjectives from 'components/noObjectives/NoObjectives';
import { makeCycleItems } from 'utils/cycleUtils';
import { teamForObjective } from 'utils/teamUtils';
import { selectCycle } from 'store/reducers/workspaceReducer';

// Locals
import * as Styles from './ObjectivesStyles';
```

> Note: also try to group Globals by folder (like in the example above)

