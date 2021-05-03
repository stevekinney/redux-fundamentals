---
path: "/removing-an-item"
title: "Removing an Item"
order: "4D"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Okay, we can add items, but we can't remove one just yet. Can we get the ability to remove an item working?

**Exercise**: Can you create the action and reducer logic for removing an item? (You can view the solution [here](https://github.com/stevekinney/tip-calculator/commit/103c3725dbedecf8e6130d44016a34004cb54eed?branch=103c3725dbedecf8e6130d44016a34004cb54eed&diff=split).)

As far as connecting it, you have a few options.

- Make a `ConnectedMenuItem` that has the ability to dispatch an action.
- Allow `ConnectedMenuItems` to pass in an onRemove prop to `MenuItem`.

We're actually going to do it both ways just to see the difference in how we might implement it.

First, we'll pass a method to remove a menu item into `ConnectedMenuItems`.

```js
const mapDispatchToProps = {
  removeItem(uuid) {
    return removeItem(uuid);
  },
};
```

Next, we'll pass that to each individual menu item.

```js
import { Stack } from "@twilio-paste/stack";
import MenuItem from "./MenuItem";

export const MenuItems = ({ items, removeItem }) => {
  return (
    <Stack orientation="vertical" spacing="space60">
      {items.map((item) => (
        <MenuItem
          {...item}
          key={item.uuid}
          remove={() => removeItem(item.uuid)} {/* 🌝 */}
        />
      ))}
    </Stack>
  );
};
```
