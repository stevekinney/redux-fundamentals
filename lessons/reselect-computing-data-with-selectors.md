---
path: "/reselect"
title: "Computing Data with Reselect"
order: "5A"
section: "Selectors, Reselect, and a Component's Own Properties"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Reselect allows us to cache data easily and only compute values when the things we care about change.

In a new file called `store/items/selectors.js`:

```js
import { createSelector } from "reselect";

export const selectItems = (state) => state.items;
export const selectTipPercentage = (state) => state.tipPercentage;

export const selectSubtotal = createSelector([selectItems], (items) => {
  return items.reduce((sum, item) => sum + item.price * item.quantity, 0);
});

export const selectTipAmount = createSelector(
  [selectSubtotal, selectTipPercentage],
  (subtotal, tipPercentage) => {
    return subtotal * (tipPercentage / 100);
  }
);

export const selectTotal = createSelector(
  [selectSubtotal, selectTipAmount],
  (subtotal, tipAmount) => {
    return subtotal + tipAmount;
  }
);
```

Now in `SummaryContainer.js`:

```js
import { connect } from "react-redux";
import { Summary } from "../components/Summary";
import { selectSubtotal, selectTipAmount } from "../store/items/selectors";

const mapStateToProps = (state) => {
  const subtotal = selectSubtotal(state);
  const tipAmount = selectTipAmount(state);
  const total = selectTipAmount(state);

  return {
    subtotal,
    tipAmount,
    total,
  };
};

export const SummaryContainer = connect(mapStateToProps)(Summary);
```

This is good for a number of reasons.

- We're caching values and calling them only when things we rely on change.
- We're store the functions that get data from our state in one place. If the shape of our state changes, we don't really have to worry about it.
