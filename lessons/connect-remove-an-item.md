---
path: "/removing-an-item"
title: "Removing an Item"
order: "4E"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Okay, we can add items, but we can't remove one just yet. Can we get the ability to remove an item working?

**Exercise**: Can you create the action and reducer logic for removing an item? Use this [Code Sandbox](https://codesandbox.io/s/df1j4) for the exercise. (You can view the solution [here](https://github.com/stevekinney/tip-calculator/commit/61ea79e4c6ca9ccb434f808ae628b2960c43a24e?branch=61ea79e4c6ca9ccb434f808ae628b2960c43a24e&diff=split).)

As far as connecting it, you have a few options.

- Make a `MenuItemContainer` (singular) that has the ability to dispatch an action.
- Allow `MenuItemsContainer` (plural) to pass in an onRemove prop to `MenuItem`.

We're actually going to do it the first way because it will make us learn a new thing about React Redux along the way.

First, we'll pass a method to remove a menu item into `MenuItemContainer`.

```js
const mapDispatchToProps = (dispatch, ownProps) => {
  return {
    remove: () => dispatch(removeItem(ownProps.uuid)),
  };
};
```

Now, we'll swap in our new container component.

```js
import { Stack } from "@twilio-paste/stack";
import MenuItem from "./MenuItem";

export const MenuItems = ({ items }) => {
  return (
    <Stack orientation="vertical" spacing="space60">
      {items.map((item) => (
        <MenuItemContainer {/* 🌝 */}
          {...item}
          key={item.uuid}
        />
      ))}
    </Stack>
  );
};
```
