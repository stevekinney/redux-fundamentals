---
path: "/introduction-to-react-redux"
title: "Introductiton to React Redux"
order: "3B"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Okay, so we've looked at Redux and we're working with some assumption that you've seen React before. But, it turns out that there is a bit of a layer in between and it's a library called React Redux.

Luckily, it's another fairly small library as well.

The first—and arguably most important part—is a component called `Provider`. This is a component that takes the store and threads it through your React application using the [Context API](https://reactjs.org/docs/context.html).

First, let's go ahead and create our store in `store.js`.

```js
import { createStore } from "redux";
import { reducer } from "./reducer";

export const store = createStore(reducer);
```

Now, in `index.js`, we'll hook it up to React.

```js
import React from 'react';
import ReactDOM from 'react-dom';

import { Provider } from 'react-redux'; /* 🌝 */

import Application from './Application';
import { store } from './store'; /* 🌝 */

import './index.scss';

ReactDOM.render(
  <Provider store={store}> {/* 🌝 */}
    <React.StrictMode>
      <Application />
    </React.StrictMode>
  </Provider>, {/* 🌝 */}
  document.getElementById('root')
);
```
