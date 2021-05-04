---
path: "/stores-and-dispatch"
title: "Redux Stores and Dispatch"
order: "2C"
section: "Redux Without React"
description: "Dispatching to the Store"
---

Alright, so we made a store. Redux stores also have a relatively small API surface area.

- `dispatch`
- `subscribe`
- `getState`
- `replaceReducer`

We'll get to `subscribe` shortly. `getState` and `replaceReducer` should also be somewhat straight-forward as well.

But, right now, `dispatch` is the star of the show.

We made some initial state. We made the outlined some things that could happen to that state. We even defined what should happen to the state when those actions happen.

So, how do we get actions into that reducer to modify the state? Well, we dispatch them.

```js
store.dispatch(action);
```

Our action creators are functions that return actions, so might see something like this:

```js
store.dispatch(increment());
```

Once an action is dispatched, the reducer takes care of the rest.

Let's put this to the test.

```js
const store = createStore(reducer);

console.log(store.getState()); // { value: 0 }
store.dispatch(increment());
console.log(store.getState()); // { value: 1 }
```

The system works. You probably understand most of Redux at this point. Seriously.
