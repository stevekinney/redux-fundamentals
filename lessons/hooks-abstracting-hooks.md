---
path: "/abstracting-hooks"
title: "Abstracting Logic Into a Custom Hook"
order: "3I"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

You could take this one step further if you wanted to completely abstract your dependency on Redux from your React components.

```js
import { useMemo } from "react";
import { useSelector } from "react-redux";
import { decrement, increment, set } from "./actions";
import { useActions } from "./use-actions";

export const useCounter = () => {
  const count = useSelector((state) => state.count);
  const actions = useActions({ increment, decrement, set });
  return useMemo(() => {
    return { count, ...actions };
  }, [count, actions]);
};
```

And then it's as simple as pulling what you need using the hook in your component.

```js
import { SetCounter } from "./SetCounter";
import { useCounter } from "./use-counter";

export const Counter = () => {
  const incident = "Incident";
  const { count, increment, decrement, set } = useCounter(); /* 🌝 */

  return (
    <main className="Counter">
      <h1>Days Since Last {incident}</h1>
      <p className="count">{count}</p>
      <section className="controls">
        <button onClick={() => increment()}>Increment</button>
        <button onClick={() => set(0)}>Reset</button>
        <button onClick={() => decrement()}>Decrement</button>
      </section>
      <SetCounter />
    </main>
  );
};

export default Counter;
```

## Exercise

Can you implement this in `SetCounter`? (You can peek at the solution [here](https://github.com/stevekinney/redux-incident-counter/commit/e25cacd3ac7a1abfefb816484b93dafc8194e9f7?branch=e25cacd3ac7a1abfefb816484b93dafc8194e9f7&diff=split).)
