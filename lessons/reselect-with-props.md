---
path: "/reselect-with-props"
title: "Using Props with Reselect"
order: "5B"
section: "Reselect and Selectors"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

**Locally**: Clone and install [this repository](https://github.com/stevekinney/jetsetter-redux). We'll be starting from the `basic-functionality` branch.

This works pretty well using hooks, but how do we get access to props when we're using `connect`?

Let's start with

```js
import { connect } from "react-redux";
import { Item } from "./Item";

const mapStateToProps = (state, ownProps) => {
  return {
    ...ownProps,
    items: state.items.filter((item) => item.packed === ownProps.packed),
  };
};

const Component = ({ items = [], title = "Items", packed = true }) => {
  return (
    <section className="Items">
      <h2>
        {title} ({items.length})
      </h2>
      {items.map((item) => (
        <Item key={item.id} item={item} />
      ))}
    </section>
  );
};

export const Items = connect(mapStateToProps)(Component);
```

Okay, so let's write our selectors.

```js
const selectItems = (state) => state.items;
const selectPackedProp = (_, props) => props.packed;

const selectFilteredItems = createSelector(
  [selectItems, selectPackedProp],
  (items, packed) => items.filter((item) => item.packed === packed)
);

const mapStateToProps = (state, ownProps) => {
  return {
    ...ownProps,
    items: selectFilteredItems(state, ownProps),
  };
};
```

## Using Reselect with Hooks

```js
const filteredItems = useSelector((state) =>
  selectFilteredItems(state, { packed })
);
```
