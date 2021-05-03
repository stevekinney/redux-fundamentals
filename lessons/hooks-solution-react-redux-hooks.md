---
path: "/solution-react-redux-hooks"
title: "Solution: Adding SetCounter"
order: "3G"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

This will get us there:

```js
import { useState } from "react";
import { useDispatch } from "react-redux";
import { set } from "./actions";

export const SetCounter = () => {
  const [count, setCount] = useState(0);
  const dispatch = useDispatch();

  return (
    <section className="controls">
      <form
        onSubmit={(event) => {
          event.preventDefault();
          dispatch(set(count));
        }}
      >
        <label htmlFor="set-to">Set Count</label>
        <input
          id="set-to"
          type="number"
          value={count}
          onChange={(event) => setCount(parseInt(event.target.value, 10))}
        />
        <input type="submit" />
      </form>
    </section>
  );
};
```

**Extension**: If you want to listen to the store and update the temporary state, that's doable.

```js
useEffect(() => {
  setCount(countFromStore);
}, [countFromStore]);
```
