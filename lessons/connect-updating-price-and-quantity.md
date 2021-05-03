---
path: "/updating-price-and-quantity"
title: "Updating Price and Quantity"
order: "4E"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

I'm going to look at how to change the price and then you're going to change the quantity.

In `action.js`

```js
export const UPDATE_PRICE = "UPDATE_PRICE";

export const updatePrice = (uuid, price) => {
  return {
    type: UPDATE_PRICE,
    payload: {
      uuid,
      price,
    },
  };
};
```

In `reducer.js`:

```js
if (action.type === UPDATE_PRICE) {
  return state.map((item) => {
    if (item.uuid !== action.payload.uuid) return item;
    return { ...item, price: action.payload.price };
  });
}
```

In `ConnectedMenuItems.js`:

```js
const mapDispatchToProps = (dispatch) => ({
  removeItem(uuid) {
    return dispatch(removeItem(uuid));
  },
  updateItemPrice(uuid) {
    return (price) => dispatch(updatePrice(uuid, price));
  },
});
```

In `MenuItems.js`:

```js
export const MenuItems = ({
  items,
  removeItem,
  updateItemPrice,
  updateItemQuantity,
}) => {
  return (
    <Stack orientation="vertical" spacing="space60">
      {items.map((item) => (
        <MenuItem
          {...item}
          key={item.uuid}
          remove={() => removeItem(item.uuid)}
          updatePrice={updateItemPrice(item.uuid)} {/* 🌝 */}
        />
      ))}
    </Stack>
  );
};
```

**Exercise**: Can you get the quantity to update as well?
