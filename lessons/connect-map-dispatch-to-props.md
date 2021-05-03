---
path: "/map-dispatch-to-props"
title: "mapDispatchToProps"
order: "4C"
section: "Connecting Redux to React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Okay, so we have our replacement for `useSelector`, how do we pass `dispatch` in?

In order to update the state—and subsequently the UI, we're going to need to do a few things.

- We need an action to dispatch.
- We need the reducer to deal with that action.
- We need the `NewItemForm` to dispatch that action.

We'll use the aciton creator pattern to format our action for us in `action.js`.

```js
export const ADD_NEW_ITEM = "ADD_NEW_ITEM";

export const addNewItem = (name, price) => {
  return {
    type: ADD_NEW_ITEM,
    payload: {
      uuid: Date.now(),
      name,
      price,
      quantity: 1,
    },
  };
};
```

Next, we'll update the reducer.

```js
export const reducer = (state = initialState, action) => {
  if (action.type === ADD_NEW_ITEM) {
    return [...state, action.payload];
  }

  return state;
};
```

Let's try out firing an action from the developer tools.

```js
{
  type: 'ADD_NEW_ITEM',
  payload: { uuid: 3, name: 'Braised Seitan', price: 12, quantity: 1 }
}
```

Cool, we're most of the way there. Now we just need to wire that up with the `NewItemForm` and we're good to go.

We can't just require the action creator in the component because it's just a function that returns an object and it doesn't know anything about `dispatch`.

What we want to do is pass in an `onSubmit` prop, which the component is already expecting that is bound to Redux's `dispatch`.

Let's start with the simplest possible version:

```js
import { connect } from "react-redux";
import { NewItemForm } from "./NewItemForm";

export const ConnectedNewItemForm = connect()(NewItemForm);
```

Connect components received `dispatch` out of the box. So, now we _can_ do something like this:

```js
export const NewItemForm = ({ onSubmit, dispatch }) => {
  // …

  const handleSubmit = (event) => {
    event.preventDefault();

    if (typeof onSubmit === "function") {
      onSubmit(event, { name, price });
    }

    dispatch(addNewItem(name, price));

    setName("");
    setPrice(0);
  };

  // …
};
```

(We'll also want to swap out `NewItemForm` for `ConnectedNewItemForm` in `Calculator.js`.)

This approach is a bit flawed. It ties our presentational component to Redux, which is less than optimal. It doesn't create a clear API contract. `NewItemForm` can literally dispatch anything it wants. We can do better.

Just like we can format our state to the props of a presentation component. We can do that with `dispatch` as well.

```js
import { connect } from "react-redux";
import { NewItemForm } from "./NewItemForm";
import { addNewItem } from "./reducer";

const mapDispatchToProps = (dispatch) => {
  return {
    onSubmit: (name, price) => dispatch(addNewItem(name, price)),
  };
};

export const ConnectedNewItemForm = connect(
  null,
  mapDispatchToProps
)(NewItemForm);
```

We can rip out that fun stuff we did with `dispatch` and put the component back to the way we found it.

Let's say we had a whole bunch of actions. We probably don't need to call each one with `dispatch` by hand. We can use `bindActionCreators` in order to take an object of action creators and spit out an object with all of those aciton creators bound to `dispatch`.

```js
const mapDispatchToProps = (dispatch) => {
  return bindActionCreators(
    {
      onSubmit: addNewItem,
    },
    dispatch
  );
};
```

For simple things, we can also use a simpler syntax.

```js
const mapDispatchToProps = {
  onSubmit: addNewItem,
};
```

If `connect` receives an object, it will automatically pass it to `bindActionCreators` and pass it through to the component.
