---
path: "/immer"
title: "Using Immer with an Entire Reducer"
order: "6B"
section: "Immer"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

It turns out that we can just use immer for an entire reducer.

```js
export const reducer = produce((state = initialItems, action) => {
  if (action.type === ITEM_ADDED) {
    const item = {
      uuid: id++,
      quantity: 1,
      name: action.payload.name,
      price: parseInt(action.payload.price, 10),
    };

    state.push(item);
  }

  if (action.type === ITEM_REMOVED) {
    return state.filter((item) => item.uuid !== action.payload.uuid);
  }

  if (action.type === ITEM_PRICE_UPDATED) {
    const item = state.find((item) => item.uuid === action.payload.uuid);
    item.price = parseInt(action.payload.price, 10);
  }

  if (action.type === ITEM_QUANTITY_UPDATED) {
    const item = state.find((item) => item.uuid === action.payload.uuid);
    item.quantity = parseInt(action.payload.quantity, 10);
  }
}, initialItems);
```

You can see this [here](https://github.com/stevekinney/tip-calculator/commit/8a7b2aeed48af497c181468c521046cb2b7d775c).

## Extension Exercise

Could we simplify these even further by using the `selectItem` selector we made earlier to find the right item in the reducer now?

(You can find the solution [here](https://github.com/stevekinney/tip-calculator/commit/8c5b1ea5733c6780dbab0533799c20a85088baf6).)
