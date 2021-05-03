---
path: "/connect"
title: "mapStateToProps"
order: "4B"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

The name of the game with the Connect API is what we take our presentational components in React and wrap them in a high-order components that passes state and dispatch from Redux in as props.

There are different naming conventions for naming components. Just for clarity, we're going prepend our wrapped components with the word "Connected." So, `MenuItems`—when wrapped with Redux—will be `ConnectedMenuItems`.

Right now our items are just hard-coded in `MenuItems`. Let's go ahead and connect it to Redux. We'll make a new file called `ConnectedMenuItems.js`.

```js
import { connect } from "react-redux";
import { MenuItems } from "./MenuItems";

const mapStateToProps = (state) => {
  return {
    items: state.items,
  };
};

export const ConnectedMenuItems = connect(mapStateToProps)(MenuItems);
```

And now we'll swap our new Redux-connected component in and remove that hard-coded data in `Calculator.js`.

```js
const Calculator = () => {
  return (
    <Card>
      <NewItemForm />
      <ConnectedMenuItems />
      <TipSelect />
      <Stack orientation="vertical" spacing="space30">
        <SummaryLine title="Subtotal">$0.00</SummaryLine>
        <SummaryLine title="Tax">$0.00</SummaryLine>
        <SummaryLine title="Tip Amount">$0.00</SummaryLine>
        <SummaryLine title="Total">$0.00</SummaryLine>
      </Stack>
    </Card>
  );
};
```

`mapStateToProps` is _very_ similar to `useSelector` in this case.
