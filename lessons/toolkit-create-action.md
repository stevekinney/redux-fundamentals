---
path: "/create-action"
title: "Creating Actions"
order: "7F"
section: "Redux Toolkit"
description: "Getting started and an introduction to TypeScript && React Workshop"
---

Let's add another reducer action to our `taskSlice`.

```js
export const tasksSlice = createSlice({
  name: "tasks",
  initialState,
  reducers: {
    // …
    toggle: (state, action) => {
      const task = state.find((task) => task.id === action.payload.taskId);
      task.complete = action.payload.complete;
    },
  },
});
```

You can dispatch an action with a more detailed payload. Take this example from

```js
dispatch(
  tasksSlice.actions.toggle({
    taskId,
    complete: event.target.checked,
  })
);
```

Or, you can create more actions using `createAction` and the `prepare` callback.

```js
export const toggleTask = createAction("tasks/toggle", (taskId, complete) => ({
  payload: { taskId, complete },
}));
```

And now you can dispatch it like we did with some of the earlier actions in this workshop.

```js
dispatch(toggleTask(taskId, event.target.checked));
```
