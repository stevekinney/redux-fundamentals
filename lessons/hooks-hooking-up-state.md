---
path: "/hooking-up-state"
title: "Hooking Up State"
order: "3D"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Alright, so we have Redux connected to React in spirit, but the component isn't really using anything here.

We're going to get more into selectors in a bit, but—at a high level—they do what they say they do on the tin: they select pieces from our state tree.

```js
import { useSelector } from 'react-redux'; /* 🌝 */

export const Counter = () => {
  const incident = 'Incident';
  const count = useSelector((state) => state.count); {/* 🌝 */}

  return (
    // …
  );
};

export default Counter;

```

It's zero by default in our state, so our UI hasn't changed much. But, we _could_ trigger this from the developer tools if we wanted. Let's dispatch the following action.

```js
{
  type: 'INCREMENT',
}
```

We can see the count increment, which is good. We can also see the actions logged into the tools. We can even roll back the state if want. (**Hint**: The Redux Dev Tools are using the enhancer to add this functionality to our store.)
