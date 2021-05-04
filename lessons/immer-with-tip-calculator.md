---
path: "/immer"
title: "Mutable Immutable State with Immer"
order: "6A"
section: "Immer"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Immer is a library that allows us to act like mutating state is totally okay—mostly because we're not actually mutating it.

Here is a super simple example.

```js
if (action.type === ITEM_ADDED) {
  return produce(state, (draftState) => {
    const item = {
      uuid: id++,
      quantity: 1,
      name: action.payload.name,
      price: parseInt(action.payload.price, 10),
    };

    draftState.push(item);
  });
}
```

If you look closely, you can see the following:

- It takes the object you want to change and then a function where it passes it in as an object you can mutate.
- After you're done, it returns a new object based on the changes you made the the draft object.

That's not particularly impressive with adding a new item. The spread operator wasn't huring anyone. But, what about, updating the price?

```js
if (action.type === ITEM_PRICE_UPDATED) {
  return produce(state, (draftState) => {
    const item = state.find((item) => item.uuid === action.payload.uuid);
    item.price = parseInt(action.payload.price, 10);
  });
}
```

## Exercise

[This](https://github.com/stevekinney/tip-calculator/commit/a83896158ee15103684139be236b3ab861961525) is where we our now.

Can you implement it for the quantity? (You can fine the solution [here](https://github.com/stevekinney/tip-calculator/commit/9412c41114789c1d66f1cb7193bf23d85b015792).)
