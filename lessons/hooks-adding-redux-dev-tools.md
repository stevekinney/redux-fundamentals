---
path: "/redux-dev-tools"
title: "Adding the Redux Dev Tools"
order: "3C"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

First and foremost, install the Redux Developer Tools in your browser if you haven't already.

- [Chrome](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)
- [Firefox](https://addons.mozilla.org/en-US/firefox/addon/reduxdevtools/)

We're not totally there yet, we still need to hook our application up to the tools.

The extension adds some properties onto the global `window` object. One of these is an _enhancer_ that we can use.

```js
window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__();
```

We can pass this to our store when we create it in `store.js`.

Now, we have some insight into the current state of the store and the actions that are firing through the application.
