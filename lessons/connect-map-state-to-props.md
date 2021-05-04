---
path: "/map-state-to-props"
title: "mapStateToProps"
order: "4B"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

The name of the game with the Connect API is what we take our presentational components in React and wrap them in a high-order components that passes state and dispatch from Redux in as props.

Let's check out the `MenuItems` component:

```js
export const MenuItems = ({ items }) => {
  return (
    <Stack orientation="vertical" spacing="space60">
      {items.map((item) => (
        <MenuItem {...item} key={item.uuid} />
      ))}
    </Stack>
  );
};
```

Look, it's just a React component and it's waiting for some props from us. We should figure out how to hand it those props from Redux.

## Connecting a Regular Ol' React Component to Redux

There are different naming conventions for naming components. Just for clarity, we're going append our wrapped components with the word "Container." So, `MenuItems`—when wrapped with Redux—will be `MenuItemsContainer`.

(You might also see something like "Connected" as a prefix. It doesn't _really_ matter, just be consistent.)

Right now our items are just hard-coded in `MenuItems`. Let's go ahead and connect it to Redux. We'll make a new file called `ConnectedMenuItems.js`.

```js
import { connect } from "react-redux";
import { MenuItems } from "../components/MenuItems";

const mapStateToProps = (state) => {
  return {
    items: state.items,
  };
};

export const MenuItemsContainer = connect(mapStateToProps)(MenuItems);
```

And now we'll swap our new Redux-connected component in and remove that hard-coded data in `Calculator.js`.

```js
const Calculator = () => {
  return (
    <Card>
      <NewItemForm />
      <MenuItemsContainer />
      <TipSelectContainer />
      <Summary />
    </Card>
  );
};
```

`mapStateToProps` is _very_ similar to `useSelector` in this case. It's pulling stuff from the state and passing it into the component.
