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
export const ITEM_ADDED = "ITEM_ADDED";

export const addNewItem = (name, price) => {
  return {
    type: ITEM_ADDED,
    payload: {
      name,
      price,
    },
  };
};
```

You'll notice what I don't have in here: anything the that we didn't didn't get from the action itself. So, like, we don't know the `uuid` yet. The quantity will be 1 by default. The only things that the user gave us in that form was the `name` and the `price` and our action reflects that.

Next, we'll update the reducer.

```js
export const reducer = (state = initialItems, action) => {
  if (action.type === ITEM_ADDED) {
    const item = { uuid: id++, quantity: 1, ...action.payload };
    return [...state, item];
  }

  return state;
};
```

Now, one thing you'll notice is that I will let the action payload override the default properties. Maybe in the future, we add a quantity field. This will take the quantity from the action and use that if one exists.

Let's try out firing an action from the developer tools.

```js
{
  type: 'ITEM_ADDED',
  payload: { name: 'Braised Seitan', price: 12 }
}
```

Cool, we're most of the way there. Now we just need to wire that up with the `NewItemForm` and we're good to go.

We can't just require the action creator in the component because it's just a function that returns an object and it doesn't know anything about `dispatch`.

What we want to do is pass in an `onSubmit` prop, which the component is already expecting that is bound to Redux's `dispatch`.

Let's start with the simplest possible version in `containers/NewItemFormContainer.js`:

```js
import { connect } from "react-redux";
import { NewItemForm } from "../components/NewItemForm";

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

(We'll also want to swap out `NewItemForm` for `NewItemFormContainer` in `Calculator.js`.)

This approach is a bit flawed. It ties our presentational component to Redux, which is less than optimal. It doesn't create a clear API contract. `NewItemForm` can literally dispatch anything it wants. We can do better.

Just like we can format our state to the props of a presentation component. We can do that with `dispatch` as well.

```js
import { connect } from "react-redux";
import { NewItemForm } from "../components/NewItemForm";
import { addNewItem } from "../store/items/reducer";

const mapDispatchToProps = (dispatch) => {
  return {
    onSubmit: (name, price) => dispatch(addNewItem(name, price)),
  };
};

export const NewItemFormContainer = connect(
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
