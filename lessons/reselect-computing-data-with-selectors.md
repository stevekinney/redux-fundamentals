---
path: "/reselect"
title: "Computing Data with Reselect"
order: "5A"
section: "Reselect and Selectors"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Reselect allows us to cache data easily and only compute values when the things we care about change.

```js
const getItems = (state) => state.items;
const getTipPercentage = (state) => state.tipPercentage;

const getSubtotal = createSelector([getItems], (items) => {
  return items.reduce((sum, item) => sum + item.price * item.quantity, 0);
});

const getTipAmount = createSelector(
  [getSubtotal, getTipPercentage],
  (subtotal, tipPercentage) => {
    return subtotal * (tipPercentage / 100);
  }
);

const getTotal = createSelector(
  [getSubtotal, getTipAmount],
  (subtotal, tipAmount) => {
    return subtotal + tipAmount;
  }
);

const mapStateToProps = (state) => {
  const subtotal = getSubtotal(state);
  const tipAmount = getTipAmount(state);
  const total = getTotal(state);

  return {
    subtotal,
    tipAmount,
    total,
  };
};
```
