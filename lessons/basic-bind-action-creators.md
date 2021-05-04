---
path: "/bind-action-creators"
title: "Bind Action Creators"
order: "2E"
section: "Redux Without React"
description: "Creating Stores and Reducers"
---

Let's get back to Redux itself for a moment. So far, we've made functions that create actions (a.k.a. action creators) and we've passed them to `dispatch`.

Well, what if we wanted to wrap that whole process into one nice neat package.

```js
const dispatchIncrement = () => store.dispatch(increment());
const dispatchAdd = (number) => store.dispatch(add(number));

dispatchIncrement();
dispatchAdd();
```

This could be tedious. What else could we do? We _could_ use `compose`.

```js
const dispatchIncrement = compose(store.dispatch, increment);
const dispatchAdd = compose(store.dispatch, add);
```

And if we wanted to a whole bunch, we could get fancy.

```js
const [dispatchIncrement, dispatchAdd] = [increment, add].map((fn) =>
  compose(store.dispatch, fn)
);
```

But, like, React likes its props in objects and then we'd have to get all fussy with `Object.keys` or `Object.entries`. I'm very lazy. We should just have an helper for that. Oh, wait, we do.

```js
const actions = bindActionCreators(
  {
    increment,
    add,
  },
  store.dispatch
);

actions.increment();

console.log(store.getState());
```

There is no rule saying that you have to use `bindActionCreators`. It's there to help you.
