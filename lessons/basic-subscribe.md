---
path: "/subscribing-to-the-store"
title: "Subscring to Store Changes"
order: "2D"
section: "Redux Without React"
description: "Creating Stores and Reducers"
---

If we think about this in terms of React, we're probably not expecting that our components call `store.getState()` all the time. Rather, we would think that our store would know that its state has changed and pass different props to the components.

That's a good thought acutally. In the last section, we noticed that the store has a `subscribe` method. This method takes a function dictates what should happen whenever the state in the store is updated.

`subscribe` also returns a function that you can call to unsubscribe.

```js
const subscriber = () => console.log('Subscriber!' store.getState().value);

const unsubscribe = store.subscribe(subscriber);

store.dispatch(increment()); // "Subscriber! 1"
store.dispatch(add(4)); // "Subscriber! 5"

unsubscribe();

store.dispatch(add(1000)); // (Silence)
```

Now, it's silent, but the action was still dispatched and the reducer still updated the state. We just turned off our notifcations.
