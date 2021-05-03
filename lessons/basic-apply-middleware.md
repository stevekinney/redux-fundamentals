---
path: "/apply-middleware"
title: "Apply Middleware"
order: "2G"
section: "Redux Without React"
description: "Creating Stores and Reducers"
---

**Nota Bene**: I'm going to introduce this topic at a high-level right now, but we'll round back to it a few times throughout this course and cover it in greater depth in Production Grade Redux.

`createStore()` takes one, two, or three arguments.

- `reducer`
- `initialState`
- `enhancer`

As we saw, passing in a reducer is required, but everything else is optional. We're going to get way deeper into working with enhancers and middleware in the Production-Grade Redux course, but let's briefly dip our our toes in a bit right now because I both promised you that we'd cover the lion's share of the API surface area of Redux and because we'll see them pop up in this workshop as well.

An enhancer is a function that allows you to add functionality to Redux that it doesn't come with out of the box. We'll see this when we want to hook it up to the developer tools or when we want add some the ability to do asynchronous tasks (e.g. make a server-side HTTP requests).

Enhancers are—amazing—both simple, but also kind of hard to explain.

An enhancer is a function that gets a copy of `createStore` and then a copy of all of the arguments passed to `createStore` before _actually_ passing them to `createStore`. This allows you to create libraries and plugins that will augment how the store works.

We'll see this when we use the Redux Developer Tools and when we want to dispatch asynchronous actions. It's not super common that you'll write your own enhancers, but you'll use them from time to time.

```js
const logEnhancer = (createStore) => (reducer, initialState, enhancer) => {
  // Do stuff like wrap the reducer in a higher-order function.
  const reducerWithConsoleLogs = (previousState, action) => {
    const nextState = reducer(previousState, action);
    console.log({ action, previousState, nextState });
    return nextState;
  };

  return createStore(reducerWithConsoleLogs, initialState, enhancer);
};
```

Now, when you create your store, you can do modify whatever reducer is passed in.

```js
const store = createStore(reducer, logEnhancer);
```

## `applyMiddleware`

`applyMiddleware` is a way to produce an enhancer out of chain of middleware.

```js
const enhancer = applyMiddleware(
  firstMiddleware,
  secondMiddleware,
  thirdMiddleware
);
```

Middleware have the following API:

```js
const someMiddleware = (store) => (next) => (action) => {
  // Do stuff before the action reaches the reducer or the next piece of middleware.
  next(action);
  // Do stuff after the action has worked through the reducer.
};
```

`next` is either the next piece of middleware or it's `store.dispatch`. If you don't call `next`, you will swallow the action and it will never hit the reducer.

Here is a quick example:

```js
const logMiddleware = (store) => (next) => (action) => {
  console.log("Before", store.getState(), { action });
  next(action);
  console.log("After", store.getState(), { action });
};

const store = createStore(reducer, applyMiddleware(logMiddleware));
```

This is a pretty powerful idea.

Our examples are intentionally contrived, but if you wanted to you could use both our enhancer and our middleware. But, if `createStore` only takes one enhancer—then how?

```js
const middlewares = applyMiddleware(logMiddleware);
const enhancer = compose(middleware, logEnhancer);
```

It's kind of ridiculous, but it works.

And with that, we covered all of Redux's API, but you probably want to see how it works with React, right?
