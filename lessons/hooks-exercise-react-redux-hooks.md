---
path: "/exercise-react-redux-hooks"
title: "Exercise: Adding SetCounter"
order: "3F"
section: "Hooking It Up With React"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

We have a component that we're not using: `SetCounter`. Let's pop it into our application.

```js
export const Counter = () => {
  const incident = "Incident";
  const count = useSelector((state) => state.count);
  const dispatch = useDispatch();

  return (
    <main className="Counter">
      <h1>Days Since Last {incident}</h1>
      <p className="count">{count}</p>
      <section className="controls">
        <button onClick={() => dispatch(increment())}>Increment</button>
        <button onClick={() => dispatch(set(0))}>Reset</button>
        <button onClick={() => dispatch(decrement())}>Decrement</button>
      </section>
      <SetCounter /> {/* 🌝 */}
    </main>
  );
};
```

Can you wire it up to make it dispatch the correct actions?

Some tasting notes:

- You might want to use some regular ol' React component state to hold onto the temporary value that we want to set the count to before we hit the submit button.
