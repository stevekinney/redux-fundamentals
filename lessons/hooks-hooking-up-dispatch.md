---
path: "/hooking-up-dispatch"
title: "Hooking Up Dispatch"
order: "3E"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Okay, asking our users to install the developer tools and dispatch actions by hands seems not great. Maybe we should get those buttons working?

In order to do that, we're going to need them to start dispatching some actions.

```js
const dispatch = useDispatch();
```

This is `store.dispatch` from our store.

Let's import our action creators.

```js
import { decrement, increment, set } from "./actions";
```

And now we can dispatch those action creators.

```js
<button onClick={() => dispatch(increment())}>Increment</button>
<button onClick={() => dispatch(set(0))}>Reset</button>
<button onClick={() => dispatch(decrement())}>Decrement</button>
```
