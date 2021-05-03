---
path: "/basic-redux-functionality"
title: "Implementing the Basic Logic"
order: "3A"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

So, we'll look at [this sandbox](https://codesandbox.io/s/uo1rb).

We're starting from base principles, so we're going to have to do this from the ground up. So, where to begin?

Well, an interesting thing to think about is the basic state and the actions that can occur.

We have…

- A count.
- The ability to increment that count.
- The ability to decrement that count.
- The ability to set that count to zero.

If we're being intellectually honest, we could handle this in a bunch of ways.

- We could make actions for these three specific use cases (e.g. `INCREMENT`, `DECREMENT`, and `SET`).
- We could make a super generalized called `SET` where we set it a given number every time.
- We could split the difference and have `INCREMENT` and `DECREMENT` and the have an action type that handles the edge cases.

I like the third option. So, what would that look like?

We can make a file called `actions.js`.

```js
export const INCREMENT = "INCREMENT";
export const DECREMENT = "DECREMENT";
export const SET = "SET";

export const increment = () => ({ type: INCREMENT });
export const decrement = () => ({ type: DECREMENT });
export const set = (value) => ({ type: SET, payload: value });
```

That seems fine. What would a `reducer.js` look like?

```js
import { DECREMENT, INCREMENT, SET } from "./actions";

export const initialState = { count: 0 };

export const reducer = (state = initialState, action) => {
  if (action.type === INCREMENT) {
    return { count: state.count + 1 };
  }

  if (action.type === DECREMENT) {
    return { count: state.count - 1 };
  }

  if (action.type === SET) {
    return { count: action.payload };
  }

  return state;
};
```
