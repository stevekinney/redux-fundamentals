---
path: "/updating-price-and-quantity"
title: "Updating Price and Quantity"
order: "4F"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

I'm going to look at how to change the price and then you're going to change the quantity.

In `action.js`

```js
export const ITEM_PRICE_UPDATED = "ITEM_PRICE_UPDATED";

export const updatePrice = (uuid, price) => {
  return {
    type: ITEM_PRICE_UPDATED,
    payload: {
      uuid,
      price,
    },
  };
};
```

In `reducer.js`:

```js
if (action.type === ITEM_PRICE_UPDATED) {
  return state.map((item) => {
    if (item.uuid !== action.payload.uuid) return item;
    return { ...item, price: action.payload.price };
  });
}
```

In `MenuItemContainer.js`:

```js
const mapDispatchToProps = (dispatch, ownProps) => {
  return {
    remove: () => dispatch(removeItem(ownProps.uuid)),
    updatePrice: (price) => dispatch(updatePrice(ownProps.uuid, price)),
  };
};
```

## Exercise

Can you get the quantity to update as well? (You can view the solution [here](https://github.com/stevekinney/tip-calculator/commit/65fb9f2c087b552ee3d347a500b781bd318763e6).)
