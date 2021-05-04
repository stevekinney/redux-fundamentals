---
path: "/deriving-data"
title: "Deriving Data"
order: "4G"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

So, keeping the current tip in state is one thing because the user can update it. But, what about all of the stuff that shakes out based on the items and the amount of the tip?

We should _not_ store those in state. Keeping everything in sync could be complicated and we might mess it up. Besides, if we know the items and the tip precentage, we can calculate everything else on the fly—and that's what we _should_ do.

```js
import { connect } from "react-redux";
import { Summary } from "../components/Summary";

const mapStateToProps = (state) => {
  const subtotal = state.items.reduce(
    (sum, item) => sum + item.price * item.quantity,
    0
  );

  const tipAmount = subtotal * (state.tipPercentage / 100);

  const total = subtotal + tipAmount;

  return {
    subtotal,
    tipAmount,
    total,
  };
};

export const SummaryContainer = connect(mapStateToProps)(Summary);
```
